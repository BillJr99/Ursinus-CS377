---
layout: activity
permalink: /Activities/NoSQL/DataModels
title: "CS377: Database Design - NoSQL Data Models"


info:
  goals: 
    - "To distinguish between four types of NoSQL database models: document, key-value, columnar, and graph"
  additional_reading:
    - title: "Types of NoSQL Databases"
      link: "https://www.mongodb.com/scale/types-of-nosql-databases"
    - title: "Setting up Redis"
      link: "https://dev.to/ramko9999/host-and-use-redis-for-free-51if"
      
  models:
    - model: |
        <a title="JuliaL0313, CC BY-SA 4.0 &lt;https://creativecommons.org/licenses/by-sa/4.0&gt;, via Wikimedia Commons" href="https://commons.wikimedia.org/wiki/File:Database-document.png"><img width="256" alt="Database-document" src="https://upload.wikimedia.org/wikipedia/commons/e/ec/Database-document.png"></a>
      title: Document Database
      questions:
        - "What does this model remind you of, that you have seen before?"
        - "What types of applications are best suited to this model?"
    - model: |
        <a title="Clescop, CC BY-SA 4.0 &lt;https://creativecommons.org/licenses/by-sa/4.0&gt;, via Wikimedia Commons" href="https://commons.wikimedia.org/wiki/File:KeyValue.PNG"><img width="256" alt="KeyValue" src="https://upload.wikimedia.org/wikipedia/commons/5/5b/KeyValue.PNG"></a>
      title: Key-Value Database
      questions:
        - "How does this model relate to a normalized relational database?"
        - "How is this model similar to a document model?  How is it different?"
        - "What types of applications are best suited to this model?"
    - model: |
        <a title="Scifipete, CC BY-SA 3.0 &lt;https://creativecommons.org/licenses/by-sa/3.0&gt;, via Wikimedia Commons" href="https://commons.wikimedia.org/wiki/File:Oracle_Table_in_a_Tablespace.jpg"><img width="512" alt="Oracle Table in a Tablespace" src="https://upload.wikimedia.org/wikipedia/commons/thumb/2/2c/Oracle_Table_in_a_Tablespace.jpg/512px-Oracle_Table_in_a_Tablespace.jpg"></a>
      title: Columnar Database
      questions:
        - "What does this model remind you of, that you have seen before?"
        - "What types of applications are best suited to this model?"
    - model: |
        <a title="Originally uploaded by Ahzf (Transferred by Obersachse), CC0, via Wikimedia Commons" href="https://commons.wikimedia.org/wiki/File:GraphDatabase_PropertyGraph.png"><img width="512" alt="GraphDatabase PropertyGraph" src="https://upload.wikimedia.org/wikipedia/commons/3/3a/GraphDatabase_PropertyGraph.png"></a>
        <br>
        <p><a href="https://commons.wikimedia.org/wiki/File:Rdf-graph3.png#/media/File:Rdf-graph3.png"><img src="https://upload.wikimedia.org/wikipedia/commons/f/fd/Rdf-graph3.png" alt="Rdf-graph3.png"></a><br>Public Domain, <a href="https://commons.wikimedia.org/w/index.php?curid=17096">Link</a></p>
      title: Graph Database
      embed: <iframe height="400px" width="100%" src="https://repl.it/@BillJr99/PythonRedisExample?lite=true" scrolling="no" frameborder="no" allowtransparency="true" allowfullscreen="true" sandbox="allow-forms allow-pointer-lock allow-popups allow-same-origin allow-scripts allow-modals"></iframe> 
      questions:
        - "What types of applications are best suited to this model?"
        - "Using <a href=\"https://www.redislabs.com\">redis</a>, set up a graph database of the groups in class, and print out each group.  Here is the <a href=\"https://github.com/RedisGraph/redisgraph-py\">Redis for Python API Documentation for reference</a>."
        
tags:
  - nosql
  - modeling
  
---

## NoSQL Data Models: Key-Value, Document, Columnar, and Graph
NoSQL databases have gained popularity due to their ability to handle vast amounts of unstructured and semi-structured data. Unlike traditional relational databases, which use a structured schema, NoSQL databases offer flexible data models that can adapt to changing requirements. This report provides an overview of the four major types of NoSQL data models: key-value, document, columnar, and graph. It also includes summaries and analysis of relevant readings and additional scholarly references.

### Key-Value Data Model
In a key-value data model, data is stored as a collection of key-value pairs. The key is unique and used to retrieve the associated value. This model is simple and efficient, making it suitable for scenarios that require fast read and write operations. It is commonly used for caching, session management, and storing user profiles.

One popular key-value database is Redis, which is an open-source, in-memory data store. Redis can be easily configured and hosted for free. Below is a Python code example demonstrating how to connect to a Redis server and perform basic operations:

```python
import redis

# Connect to Redis
r = redis.Redis(host='localhost', port=6379, db=0)

# Set a key-value pair
r.set('myKey', 'myValue')

# Get the value associated with a key
value = r.get('myKey')
print(value)  # Output: b'myValue'

# Delete a key-value pair
r.delete('myKey')
```

### Document Data Model
In a document data model, data is stored as self-contained documents, typically in a format like JSON or BSON (Binary JSON). Each document can have a different structure, allowing for flexibility. Documents are grouped into collections, similar to tables in relational databases. Common use cases for document databases include content management, user profiles, and real-time analytics.

One prominent document database is MongoDB. MongoDB offers rich querying capabilities, scalability, and automatic sharding. It also provides an intuitive API for interacting with the database. Below is an example of using the MongoDB Python library to insert and query documents:

```python
from pymongo import MongoClient

# Connect to MongoDB
client = MongoClient('mongodb://localhost:27017/')

# Get the database and collection
db = client['mydb']
collection = db['mycollection']

# Insert a document
doc1 = {"name": "John", "age": 25}
result = collection.insert_one(doc1)

# Find documents matching a query
query = {"age": {"$gt": 20}}
docs = collection.find(query)
for doc in docs:
    print(doc)
```

### Columnar Data Model
The columnar data model stores data in columns rather than rows, promoting efficient storage and retrieval. It is often used for analytical workloads that involve aggregations and complex queries. Columnar databases excel in scenarios where a subset of columns is frequently accessed or when dealing with large volumes of data.

Apache Cassandra is a popular columnar database. Below is an example of using the Cassandra Python driver to create a table and insert data:

```python
from cassandra.cluster import Cluster

# Connect to Cassandra
cluster = Cluster(['127.0.0.1'])
session = cluster.connect()

# Create a keyspace and table
session.execute("CREATE KEYSPACE mykeyspace WITH REPLICATION = {'class' : 'SimpleStrategy', 'replication_factor' : 1}")
session.execute("CREATE TABLE mytable (id UUID PRIMARY KEY, name TEXT)")

# Insert data
session.execute("INSERT INTO mykeyspace.mytable (id, name) VALUES (uuid(), 'John')")
```

### Graph Data Model
The graph data model represents data as nodes and the relationships between them as edges. This model is highly suitable for scenarios involving complex relationships, such as social networks, recommendation systems, and fraud detection. Graph databases provide powerful traversal and query capabilities to analyze these relationships efficiently.

Neo4j is a widely used graph database. Neo4j leverages a property graph model where nodes, relationships, and properties can be easily represented. Below is an example of using the Neo4j Python driver to create nodes, relationships, and perform a query:

```python
from neo4j import GraphDatabase

# Connect to Neo4j
driver = GraphDatabase.driver("bolt://localhost:7687", auth=("neo4j", "password"))

# Create a session
with driver.session() as session:
    # Create nodes
    session.run("CREATE (p:Person {name: 'John'}), (c:City {name: 'London'})")

    # Create a relationship
    session.run("MATCH (p:Person), (c:City) WHERE p.name = 'John' AND c.name = 'London' CREATE (p)-[:LIVES_IN]->(c)")

    # Query relationships
    result = session.run("MATCH (p:Person)-[:LIVES_IN]->(c:City) RETURN p, c")
    for record in result:
        print(record)
```