---
layout: activity
permalink: /Activities/Redis
title: "CS377: Database Design - Redis: In-Memory Data Structures and Caching"


info:
  goals: 
    - To describe the Redis key-value data model and its core data structures (strings, hashes, lists, sets, sorted sets)
    - To apply caching patterns (cache-aside, expiration with TTL) using Redis alongside a relational database
    - To decide when an in-memory key-value store is a better fit than a relational database, and when it is not
  additional_reading:
    - title: "Redis Data Types Documentation"
      link: "https://redis.io/docs/latest/develop/data-types/"
    - title: "redis-py Client Library"
      link: "https://redis-py.readthedocs.io/en/stable/"
    - title: "Setting up Redis"
      link: "https://dev.to/ramko9999/host-and-use-redis-for-free-51if"
    
  models:
    - model: |
        <table border="1" cellpadding="4">
          <caption>Redis core data structures: every value in Redis is one of these, looked up by a single string key</caption>
          <tr><th>Structure</th><th>Looks like (Python)</th><th>Example key</th><th>Example value</th><th>Typical use</th></tr>
          <tr><td>String</td><td><code>str</code> / <code>int</code></td><td><code>page:home:hits</code></td><td><code>"5821"</code></td><td>counters, cached HTML/JSON</td></tr>
          <tr><td>Hash</td><td><code>dict</code></td><td><code>user:1001</code></td><td><code>{name: "Ada", role: "admin"}</code></td><td>one record's fields</td></tr>
          <tr><td>List</td><td><code>list</code> (deque)</td><td><code>queue:emails</code></td><td><code>[job3, job2, job1]</code></td><td>queues, recent-items feeds</td></tr>
          <tr><td>Set</td><td><code>set</code></td><td><code>post:42:likers</code></td><td><code>{1001, 1002, 1017}</code></td><td>uniqueness, membership tests</td></tr>
          <tr><td>Sorted set</td><td><code>dict</code> of member&rarr;score, kept ordered</td><td><code>leaderboard</code></td><td><code>{ada: 980, alan: 870}</code></td><td>rankings, priority queues</td></tr>
        </table>
      title: "The Redis Data Model"
      questions:
        - "Redis has no tables, no columns, and no joins: just keys mapped to values.  Colons in key names (like <code>user:1001</code>) are only a naming convention.  How would you store the <em>employees and departments</em> data from our join activity in Redis?  What operation replaces the join?"
        - "Which Redis structure would you choose for each of the following, and why: a view counter for each page of a site; the set of students enrolled in a course; a game's top-10 high score list; a work queue of thumbnails to generate?"
        - "Each structure supports operations that are atomic on the server (e.g., <code>INCR</code>, <code>SADD</code>, <code>ZINCRBY</code>).  Why does it matter that <code>INCR</code> is a single atomic operation rather than a <code>GET</code> followed by a <code>SET</code> from your program?"
    - model: |
        <pre>
        def get_user(user_id):
            key = "user:" + str(user_id)
            cached = r.hgetall(key)          # 1. try the cache
            if cached:
                return cached                # 2. hit: microseconds, no DB touched
            row = query_relational_db(user_id)   # 3. miss: ask the database
            r.hset(key, mapping=row)         # 4. fill the cache for next time
            r.expire(key, 300)               # 5. ...but only for 300 seconds (TTL)
            return row
        </pre>
      title: "The Cache-Aside Pattern and TTL"
      embed: |
        <iframe
          height="600px"
          width="100%"
          src="https://www.billmongan.com/Ursinus-CS377/assets/code-viewer.html?zip=https%3A%2F%2Fraw.githubusercontent.com%2FBillJr99%2FUrsinus-CS377%2Fgh-pages%2Ffiles%2Freplit%2FPythonRedisExample.zip&title=Python%20Redis%20Example"
          scrolling="yes"
          frameborder="no"
          allowfullscreen="true"
          sandbox="allow-scripts allow-same-origin">
        </iframe>
      questions:
        - "Trace two consecutive calls to <code>get_user(1001)</code>: which steps run on the first call, and which on the second?  Where did the second call's answer come from?"
        - "Step 5 sets a <strong>time-to-live (TTL)</strong>: Redis deletes the key automatically after 300 seconds.  What could go wrong if we cached forever (no TTL) and someone updated the user's name in the relational database?  This is the classic <strong>stale cache</strong> problem."
        - "Suppose the user is updated <em>through our own application</em>.  Besides waiting for the TTL to expire, what could the update code do to the cache to keep readers consistent?  (Hint: <code>DEL user:1001</code> &mdash; this is called <strong>cache invalidation</strong>.)"
        - "Redis keeps data in memory, so a crash can lose recent writes (unless persistence is configured).  Why is that an acceptable risk for a <em>cache</em>, but not for the <em>system of record</em>?"
        
tags:
  - nosql
  - redis
  - keyvalue
  - caching
  
---

## Why Redis?

A relational database keeps your data safe, consistent, and richly queryable — but every query pays for that power: parsing SQL, planning, reading pages from disk, checking transactions.  Many real workloads ask the *same simple question thousands of times per second* ("what's user 1001's profile?", "how many likes does this post have?").  [Redis](https://redis.io/) (REmote DIctionary Server) attacks exactly that case: it is a **key-value store that keeps everything in memory**, answering simple lookups in well under a millisecond.  Think of it as a giant, shared, network-accessible Python dictionary — with superpowers.

Redis is one of the NoSQL data models from our [NoSQL Data Models activity](./NoSQL/DataModels) (the key-value model, with graph extensions used in the [Redis lab](../Labs/Redis)).  This activity focuses on its two most common day-job roles: a *data-structure server* and a *cache in front of a relational database*.

## Redis as a Data-Structure Server

Unlike a plain key-value store, a Redis value is not just a blob — it can be a string, hash, list, set, or sorted set, each with atomic server-side operations.  A quick tour in Python using [redis-py](https://redis-py.readthedocs.io/en/stable/) (`pip install redis`):

```python
import redis
r = redis.Redis(host="localhost", port=6379, decode_responses=True)

# Strings: values and counters
r.set("page:home:hits", 0)
r.incr("page:home:hits")            # atomic increment -> 1

# Hashes: a record's fields under one key (like a small dict)
r.hset("user:1001", mapping={"name": "Ada", "role": "admin"})
r.hget("user:1001", "name")         # -> "Ada"

# Lists: push/pop from either end (queues and feeds)
r.lpush("queue:emails", "job1", "job2")
r.rpop("queue:emails")              # -> "job1"  (FIFO with LPUSH+RPOP)

# Sets: uniqueness for free
r.sadd("post:42:likers", 1001, 1002, 1001)
r.scard("post:42:likers")           # -> 2 (the duplicate was ignored)

# Sorted sets: members ordered by a numeric score
r.zincrby("leaderboard", 100, "ada")
r.zrevrange("leaderboard", 0, 9, withscores=True)   # top ten
```

The expected output of the annotated lines, run in order:

| Call | Result |
|------|--------|
| `r.incr("page:home:hits")` | `1` |
| `r.hget("user:1001", "name")` | `"Ada"` |
| `r.rpop("queue:emails")` | `"job1"` |
| `r.scard("post:42:likers")` | `2` |
| `r.zrevrange("leaderboard", 0, 9, withscores=True)` | `[("ada", 100.0)]` |

Notice what's *missing*: no schema declaration, no types, no relationships.  Structure lives in your key-naming conventions (`user:1001`, `post:42:likers`) and in your program's discipline — the flexibility and the danger of the key-value model in one stroke.

## Redis as a Cache: The Cache-Aside Pattern

The most common production use of Redis is as a **cache** in front of a slower system of record:

```
             hit (fast path, ~0.1 ms)
  client ---> Redis ------------------------------.
                |  miss                            \
                v                                   v
          relational DB --(row)--> store in Redis --> client
             (system of record, ~10-100 ms)
```

The recipe, called **cache-aside**, is always the same five numbered steps shown in the model above: *try the cache; on a hit, return it; on a miss, query the database; fill the cache; set a TTL.*

### Expiration (TTL) in Practice

```python
r.set("weather:collegeville", '{"tempF": 71}', ex=600)  # expire in 10 minutes
r.ttl("weather:collegeville")   # -> 600 (seconds remaining)
# ...ten minutes later...
r.get("weather:collegeville")   # -> None: Redis deleted it for us
```

The TTL is your freshness dial: shorter TTLs mean fresher data but more database traffic; longer TTLs mean faster responses but staler reads.  When your own application performs the update, it can do better than waiting: **invalidate** (`r.delete("user:1001")`) or overwrite the cached entry as part of the write path.  As the saying goes, cache invalidation is one of the two hard problems in computer science — always ask "who deletes this key when the truth changes?"

## When Redis, and When a Relational Database?

| Question to ask | Points to Redis | Points to relational |
|-----------------|-----------------|----------------------|
| Is losing recent writes tolerable? | Yes (cache, session data, counters) | No (orders, grades, money) |
| Access pattern? | Lookup by known key | Ad-hoc queries, joins, aggregation |
| Consistency needs? | Eventual freshness is fine | Transactions and constraints required |
| Data size vs. memory? | Hot subset fits in RAM | Full dataset, disk-sized |
| Latency budget? | Sub-millisecond | Milliseconds acceptable |

The punchline: **it is rarely either/or.**  The standard architecture keeps the relational database as the durable system of record and uses Redis for the hot, simple, high-frequency reads — the best of both worlds, at the price of managing staleness.

### Common Pitfalls

- **Treating the cache as the source of truth.**  If a key might have been evicted, expired, or lost in a restart, your code must be able to rebuild it from the database.
- **Caching without a TTL.**  A key with no expiration and no invalidation path serves stale data forever.
- **Unbounded keys.**  A list or set that only ever grows (e.g., `LPUSH` with no trim) eventually exhausts memory; pair feeds with `LTRIM` and let TTLs reap idle keys.
- **Storing secrets in code.**  A hosted Redis instance has a hostname, port, and password: keep them in a `.env` file, not in your source (see [Keeping Credentials Out of Your Code with dotenv](./SQL#keeping-credentials-out-of-your-code-with-dotenv)).
