---
layout: activity
permalink: /Activities/Modeling/Join
title: "CS377: Database Design - Data Modeling and the Join"


info:
  goals: 
    - To model table joins
    - To differentiate between the different type of joins
    - To identify potential anomalies in data schemas
    - To take steps to normalize data schemas to avoid anomalies
  additional_reading:
    - title: "SQL Joins"
      link: "https://en.wikipedia.org/wiki/Join_(SQL)"
  
  models:
    - model: |
        <img src="https://opentextbc.ca/wp-content/uploads/sites/11/2013/12/Bank-Accounts-1-300x197.jpg" alt="Bank Accounts Table from Database Design 2nd Ed by Watt and Eng">
      title: Relational Design
      questions:
        - "What data redundancies do you see in this table, and how can you fix each?"
        - "How would you change the address of a bank?  Remove a bank?  Insert a new account an an existing back, but with an updated address?  These are <strong>update anomalies</strong>, <strong>deletion anomalies</strong>, and <strong>insertion anomalies</strong>."
        - "Design a schema that eliminates data redundancy in this table."
    - model: |
        <img src="https://opentextbc.ca/wp-content/uploads/sites/11/2013/12/Ch-10-ProjectEmp-table.jpg" alt="Flawed Projects Table from Database Design 2nd Ed by Watt and Eng">
        <br>
        <img src="https://opentextbc.ca/wp-content/uploads/sites/11/2013/12/Ch-10-Project-to-Emp-ERD-300x114.jpg" alt="An Improved Projects Schema from Database Design 2nd Ed by Watt and Eng">
        <br>
        <img src="https://opentextbc.ca/wp-content/uploads/sites/11/2013/12/Ch-10-Project-and-Emp-tables-300x89.jpg" alt="The Improved Projects Table from Database Design 2nd Ed by Watt and Eng">
      title: Case Study
      questions:
        - "Induce as many anomalies as you can in the flawed table above!"
        - "How does the improved (<strong>normalized</strong>) schema help prevent the anomalies you were able to identify?"
    - model: |
        <h3>Inner Join</h3>
        <a title="GermanX, CC BY-SA 4.0 &lt;https://creativecommons.org/licenses/by-sa/4.0&gt;, via Wikimedia Commons" href="https://commons.wikimedia.org/wiki/File:SQL_Join_-_07_A_Inner_Join_B.svg"><img width="128" alt="SQL Join - 07 A Inner Join B" src="https://commons.wikimedia.org/w/index.php?title=Special:Redirect/file/SQL_Join_-_07_A_Inner_Join_B.svg"></a>
        <br>
        <h3>Left Outer Join</h3>
        <a title="GermanX, CC BY-SA 4.0 &lt;https://creativecommons.org/licenses/by-sa/4.0&gt;, via Wikimedia Commons" href="https://commons.wikimedia.org/wiki/File:SQL_Join_-_01_A_Left_Join_B.svg"><img width="128" alt="SQL Join - 01 A Left Join B" src="https://commons.wikimedia.org/w/index.php?title=Special:Redirect/file/SQL_Join_-_01_A_Left_Join_B.svg"></a>
      title: The SQL Join
      questions:
        - "Joins are classified by which records are included if a corresponding match is not found in one table.  An <strong>inner join</strong> includes only records that match across both tables.  A <strong>left outer</strong> join includes all rows from the first table and their corresponding match from the second table (or <code>NULL</code> if no match exists from the second table.  What do you think a <strong>right outer join is</strong>, and a <strong>full outer join</strong>?"
        - "What records are included in an inner join, a left outer join, a right outer join, and a full outer join, for <a href=\"https://en.wikipedia.org/wiki/Join_(SQL)\">this data table</a>?  Write the SQL <code>JOIN</code> statements required to implement each join by linking the <code>DepartmentID</code> column."
        
tags:
  - join
  - sql
  
---

## Facilitating Integrity with Modeling and the SQL Join

In the field of database management, ensuring data integrity is of utmost importance. Data integrity refers to the accuracy, consistency, and reliability of data stored in a database. One of the ways to facilitate data integrity is through the use of modeling and the SQL Join operation.

### SQL Joins

A SQL Join is a powerful operation that combines rows from two or more tables based on a related column between them. It allows data from multiple tables to be retrieved and combined in a meaningful way. The result of a join is a new table, also known as a result set, that combines rows from the joined tables based on a specified condition. The condition is typically the equality between the values in the related columns.

The Wikipedia article on [SQL Joins](https://en.wikipedia.org/wiki/Join_(SQL)) provides a comprehensive introduction to the topic. It explains various types of joins, including inner join, left join, right join, and outer join, along with their semantics and practical examples. This article serves as an excellent starting point for understanding SQL joins and their applications.

### A Step-by-Step Join Walkthrough

Joins are easiest to understand by tracing them by hand on tiny tables.  We'll use two tables throughout: an `Employee` table and a `Department` table, related through the `DeptID` column.  Notice the deliberate mismatches: Grace has no department (`NULL`), and no employee works in Marketing (`DeptID` 40).

**Employee** (the "left" table):

| Name  | DeptID |
|-------|--------|
| Ada   | 10     |
| Grace | NULL   |
| Alan  | 20     |
| Edsger| 20     |

**Department** (the "right" table):

| DeptID | DeptName    |
|--------|-------------|
| 10     | Engineering |
| 20     | Research    |
| 40     | Marketing   |

The mental procedure for *any* join is the same three steps:

1. **Pair up rows.** For each row of the left table, scan the right table for rows whose join column matches (`Employee.DeptID = Department.DeptID`).
2. **Keep the matches.** Every matching pair becomes one output row containing columns from *both* tables.
3. **Decide what to do with the leftovers.** Rows that matched nothing are where the join types differ — this is the *only* place they differ.

#### Inner Join: matches only

```sql
SELECT e.Name, e.DeptID, d.DeptName
FROM Employee e
INNER JOIN Department d ON e.DeptID = d.DeptID;
```

Trace it row by row: Ada (10) matches Engineering — keep.  Grace (`NULL`) matches nothing (`NULL` never equals anything, not even `NULL`!) — **discard**.  Alan (20) and Edsger (20) each match Research — keep both.  Marketing never matched — **discard**.

| Name   | DeptID | DeptName    |
|--------|--------|-------------|
| Ada    | 10     | Engineering |
| Alan   | 20     | Research    |
| Edsger | 20     | Research    |

#### Left Outer Join: matches, plus every left row

```sql
SELECT e.Name, e.DeptID, d.DeptName
FROM Employee e
LEFT JOIN Department d ON e.DeptID = d.DeptID;
```

Same three matched rows as before, but now the leftover *left* row (Grace) is kept, padded with `NULL` for the right table's columns:

| Name   | DeptID | DeptName    |
|--------|--------|-------------|
| Ada    | 10     | Engineering |
| Grace  | NULL   | NULL        |
| Alan   | 20     | Research    |
| Edsger | 20     | Research    |

Use a left join when the question is "show me every employee, with their department *if they have one*."

#### Right Outer Join: matches, plus every right row

```sql
SELECT e.Name, e.DeptID, d.DeptName
FROM Employee e
RIGHT JOIN Department d ON e.DeptID = d.DeptID;
```

Now the unmatched *right* row (Marketing) is kept instead, padded with `NULL` on the employee side:

| Name   | DeptID | DeptName    |
|--------|--------|-------------|
| Ada    | 10     | Engineering |
| Alan   | 20     | Research    |
| Edsger | 20     | Research    |
| NULL   | NULL   | Marketing   |

A right join is just a left join with the tables swapped: `A RIGHT JOIN B` returns the same rows as `B LEFT JOIN A`.  (Older versions of SQLite — before 3.39, released in 2022 — had no `RIGHT JOIN` *or* `FULL OUTER JOIN`, for exactly this reason: a right join can always be rewritten as a swapped left join, and a full outer join can be emulated by `UNION`ing a left join with the right side's unmatched rows.  If a join keyword errors out in your environment, check the dialect version before checking your syntax.)

#### Full Outer Join: matches, plus every leftover from both sides

```sql
SELECT e.Name, e.DeptID, d.DeptName
FROM Employee e
FULL OUTER JOIN Department d ON e.DeptID = d.DeptID;
```

| Name   | DeptID | DeptName    |
|--------|--------|-------------|
| Ada    | 10     | Engineering |
| Grace  | NULL   | NULL        |
| Alan   | 20     | Research    |
| Edsger | 20     | Research    |
| NULL   | NULL   | Marketing   |

#### One Table to Rule Them All

The four join types differ only in which unmatched rows survive:

| Join type | Matched pairs | Unmatched left rows (Grace) | Unmatched right rows (Marketing) |
|-----------|:-------------:|:---------------------------:|:--------------------------------:|
| `INNER JOIN` | kept | dropped | dropped |
| `LEFT JOIN`  | kept | kept (NULL-padded) | dropped |
| `RIGHT JOIN` | kept | dropped | kept (NULL-padded) |
| `FULL OUTER JOIN` | kept | kept (NULL-padded) | kept (NULL-padded) |

### Reasoning About Join Order

With two tables, order only matters for *outer* joins (which side is "kept"?).  With three or more tables, joins are evaluated left to right — each join's result becomes the left input of the next — and the order in which you introduce outer joins can change the answer.  Consider adding a `Building` table and asking for every employee, their department, and that department's building:

```sql
SELECT e.Name, d.DeptName, b.BuildingName
FROM Employee e
LEFT JOIN Department d ON e.DeptID = d.DeptID
LEFT JOIN Building b ON d.BuildingID = b.BuildingID;
```

Step through it:

1. `Employee LEFT JOIN Department` keeps all four employees; Grace's department columns are `NULL`.
2. That intermediate result is then left-joined with `Building`.  Grace's `d.BuildingID` is `NULL`, so she matches no building — but the *left* join keeps her anyway, with a `NULL` building.

Had we written `INNER JOIN Building` in step 2, Grace would be silently dropped even though the first join carefully preserved her — a classic pitfall: **an inner join later in the chain can undo an outer join earlier in the chain**.  When mixing join types, ask of each unmatched row: "does the next join keep me or drop me?"

For *inner* joins, order does not change the result (joins are associative and commutative in that case) — but it can change *performance*.  Query optimizers reorder inner joins to start with the smallest intermediate results; we will revisit this when we discuss query planning and indexing.

### Common Pitfalls

- **Forgetting the join condition** (`ON ...`) produces a *cross join*: every left row paired with every right row (4 × 3 = 12 rows here) — usually a bug, and enormous on real tables.
- **`NULL` never matches.**  Grace's `NULL` DeptID does not join to anything, even another `NULL`.  Filtering an outer join's `NULL`-padded columns in a `WHERE` clause (e.g., `WHERE d.DeptName = 'Research'`) silently turns it back into an inner join; put such conditions in the `ON` clause if you mean to keep unmatched rows.
- **Duplicate matches multiply.**  If two rows on each side share a key, you get 2 × 2 = 4 output rows.  Joining on a non-key column is the usual culprit when a query "invents" rows.
