---
layout: activity
permalink: /Activities/Triggers
title: "CS377: Database Design - SQL Triggers"


info:
  goals: 
    - To explain how a trigger automates integrity constraints and audit logging inside the database
    - To write a CREATE TRIGGER statement that fires before or after an INSERT, UPDATE, or DELETE
    - To trace, row by row, what a trigger does to a database when a statement fires it
  additional_reading:
    - title: "SQLite CREATE TRIGGER Documentation"
      link: "https://www.sqlite.org/lang_createtrigger.html"
    - title: "SQL Triggers Slides"
      link: "../files/cosc_304/topics/15_triggers/304_15_Triggers.pdf"
    - title: "The pubs Sample Database Schema"
      link: "../files/mspubs/pubs.pdf"
    
  models:
    - model: |
        <table border="1" cellpadding="4">
          <caption>An event/condition/action rule, and its SQL trigger equivalent</caption>
          <tr><th>Plain language</th><th>Trigger clause</th></tr>
          <tr><td>"Whenever a new sale is recorded..."</td><td><code>AFTER INSERT ON sales</code></td></tr>
          <tr><td>"...if the book actually exists..."</td><td><code>WHEN (a condition on the new row)</code></td></tr>
          <tr><td>"...add its quantity to that book's year-to-date total."</td><td><code>UPDATE titles SET ytd_sales = ...</code></td></tr>
        </table>
      title: "Anatomy of a Trigger"
      questions:
        - "A trigger is a rule stored <em>inside</em> the database: <strong>when</strong> some event happens (an <code>INSERT</code>, <code>UPDATE</code>, or <code>DELETE</code> on a table), the database automatically runs some SQL of yours.  Why might it be safer to enforce a rule like &quot;keep the year-to-date total up to date&quot; inside the database, rather than trusting every application program to remember to do it?"
        - "Triggers can fire <code>BEFORE</code> or <code>AFTER</code> the triggering statement.  Which would you use to <em>reject</em> a bad row, and which would you use to <em>react</em> to a row that was just saved?  Why?"
        - "Inside the trigger body, <code>NEW</code> refers to the row being inserted or the new version of an updated row, and <code>OLD</code> refers to the row being deleted or the old version of an updated row.  Which of <code>NEW</code> and <code>OLD</code> are available in an <code>INSERT</code> trigger?  A <code>DELETE</code> trigger?  An <code>UPDATE</code> trigger?"
    - model: |
        <pre>
        CREATE TRIGGER update_ytd_sales
        AFTER INSERT ON sales
        FOR EACH ROW
        BEGIN
            UPDATE titles
            SET ytd_sales = COALESCE(ytd_sales, 0) + NEW.qty
            WHERE title_id = NEW.title_id;
        END;
        </pre>
      title: "A Trigger on the pubs Database"
      questions:
        - "In the <a href=\"../files/mspubs/pubs.pdf\">pubs bookstore database</a>, the <code>sales</code> table records each order (<code>stor_id</code>, <code>ord_num</code>, <code>qty</code>, <code>title_id</code>), and the <code>titles</code> table caches a running <code>ytd_sales</code> total for each book.  Walk through what happens, step by step, when a store inserts a sale of 20 copies of title <code>BU1032</code>.  Which table changes first?  Which row of <code>titles</code> is touched, and why only that one?"
        - "What could go wrong if <code>ytd_sales</code> were instead updated by every cash-register application on its own?  Which anomaly from our data integrity discussions does the trigger prevent?"
        - "Write a <code>BEFORE INSERT</code> trigger on <code>sales</code> that raises an error (in SQLite: <code>SELECT RAISE(ABORT, 'quantity must be positive');</code>) when <code>NEW.qty &lt;= 0</code>.  Test it with a bad insert: what does the database report, and does the bad row appear in the table?"
        - "Design an <strong>audit log</strong>: create a table <code>price_history(title_id, old_price, new_price, changed_on)</code> and write an <code>AFTER UPDATE</code> trigger on <code>titles</code> that records every price change.  Why is a trigger a natural home for provenance data like this?"
        
tags:
  - sql
  - triggers
  - integrity
  
---

## Why Triggers?

So far, when we wanted two pieces of data to stay consistent — a running total, a log of changes, a rule like "quantity must be positive" — we relied on every *program* that touches the database to remember to enforce it.  That works right up until someone writes a new program (or opens an interactive SQL shell) and forgets.  A **trigger** moves the rule into the database itself: it is a saved piece of SQL that the database runs *automatically* whenever a particular event happens on a particular table.  No application can forget to run it, because no application runs it — the database does.

Triggers are the enforcement half of the data integrity story: constraints (`NOT NULL`, `UNIQUE`, `FOREIGN KEY`, `CHECK`) declare simple rules, and triggers handle everything richer — cross-table bookkeeping, audit trails, and validations that need a little logic.

## The Shape of a CREATE TRIGGER Statement

Every trigger answers three questions — *when*, *on what event*, and *do what*:

```sql
CREATE TRIGGER trigger_name        -- 1. a name, so you can DROP it later
BEFORE INSERT ON tablename         -- 2. when (BEFORE/AFTER) and which event (INSERT/UPDATE/DELETE) on which table
FOR EACH ROW                       -- 3. run once per affected row
BEGIN
    -- 4. the SQL to run; NEW.column and OLD.column refer to the row involved
END;
```

| Clause | Choices | What it means |
|--------|---------|---------------|
| `BEFORE` / `AFTER` | before or after the row change is applied | `BEFORE` can inspect and *veto* the change; `AFTER` reacts to a change that already happened |
| `INSERT` / `UPDATE` / `DELETE` | the triggering event | which statement type wakes the trigger up |
| `FOR EACH ROW` | once per row | a statement that changes 10 rows fires the trigger 10 times |
| `NEW` / `OLD` | pseudo-rows | `NEW` = the incoming row (INSERT/UPDATE); `OLD` = the prior row (UPDATE/DELETE) |

A helpful mental model: `NEW` and `OLD` are temporary one-row "variables" the database hands your trigger, holding the row that caused the trigger to fire.

## A Worked Example, End to End

Let's keep a running year-to-date sales total on the pubs bookstore database.  Suppose `titles` starts like this (abbreviated):

| title_id | title | ytd_sales |
|----------|-------------------------------------|-----------|
| BU1032 | The Busy Executive's Database Guide | 4095 |
| BU1111 | Cooking with Computers | 3876 |

**Step 1 — install the trigger** (this runs once, like `CREATE TABLE`; nothing fires yet):

```sql
CREATE TRIGGER update_ytd_sales
AFTER INSERT ON "dbo.sales"
FOR EACH ROW
BEGIN
    UPDATE "dbo.titles"
    SET ytd_sales = COALESCE(ytd_sales, 0) + NEW.qty
    WHERE title_id = NEW.title_id;
END;
```

(`COALESCE(ytd_sales, 0)` guards against a `NULL` total: `NULL + 20` would be `NULL`, a classic pitfall.  And why the quotes?  The SQLite conversion of pubs keeps the SQL Server schema prefix in each table's name — the table is literally named `dbo.sales` — so we quote it to keep the dot from being read as a `schema.table` separator.)

**Step 2 — a store records a sale:**

```sql
INSERT INTO "dbo.sales" (stor_id, ord_num, ord_date, qty, payterms, title_id)
VALUES ('7066', 'QA7442.3', '2023-09-13', 20, 'Net 30', 'BU1032');
```

**Step 3 — trace what the database does, in order:**

1. The row is inserted into `"dbo.sales"` (it's an `AFTER` trigger, so the insert happens first).
2. The insert event fires `update_ytd_sales`, with `NEW.qty = 20` and `NEW.title_id = 'BU1032'`.
3. The trigger body runs its `UPDATE`, matching only the row `WHERE title_id = 'BU1032'`.
4. That row's `ytd_sales` becomes `4095 + 20 = 4115`.

**Step 4 — verify the result:**

```sql
SELECT title_id, ytd_sales FROM "dbo.titles" WHERE title_id = 'BU1032';
```

| title_id | ytd_sales |
|----------|-----------|
| BU1032 | 4115 |

`BU1111` is untouched — the `WHERE` clause in the trigger body scoped the update to the one book that was sold.  Notice that the application only issued a single `INSERT`; the consistency bookkeeping came for free.

> **Try it yourself:** download [pubs.db](../files/mspubs/pubs.db) and run this in the `sqlite3` shell or from Python's `sqlite3` module — the snippets above run as-written against it.  If you build your own database instead, drop the `dbo.` prefixes and use plain `sales`/`titles` names; only the pubs conversion carries them.

## Vetoing Bad Data with a BEFORE Trigger

`AFTER` triggers react; `BEFORE` triggers can refuse.  In SQLite, `RAISE(ABORT, message)` cancels the triggering statement entirely:

```sql
CREATE TRIGGER check_positive_qty
BEFORE INSERT ON "dbo.sales"
FOR EACH ROW
WHEN NEW.qty <= 0
BEGIN
    SELECT RAISE(ABORT, 'sales quantity must be positive');
END;
```

Now `INSERT INTO "dbo.sales" (...) VALUES (..., -5, ...)` fails with `sales quantity must be positive`, and the bad row never lands in the table.  The optional `WHEN` clause is a filter: the body only runs for rows that match it.

## Common Pitfalls

- **Forgetting the trigger exists.**  Triggers run silently; when a table seems to "change by itself," check `SELECT name, sql FROM sqlite_master WHERE type = 'trigger';`.
- **Trigger cascades.**  A trigger's body can change tables that have their own triggers.  Keep bodies small, and be wary of a trigger updating the table it fires on (recursion!).
- **Doing application logic in triggers.**  Triggers are for *integrity* (totals, logs, validations) — not for sending emails or calling web services.  If a rule belongs to one application rather than to the data itself, keep it in the application.
- **Dialect differences.**  The event/`NEW`/`OLD` model is standard, but the veto syntax varies: SQLite uses `RAISE(ABORT, ...)`, MySQL uses `SIGNAL SQLSTATE '45000'`, and PostgreSQL attaches a trigger *function*.  Check your engine's documentation before porting a trigger.

## Cleaning Up

Triggers persist like tables do.  To remove one:

```sql
DROP TRIGGER IF EXISTS update_ytd_sales;
```
