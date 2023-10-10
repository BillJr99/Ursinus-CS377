---
layout: activity
permalink: /Activities/RelationalModel2
title: "CS377: Database Design - Relational Data Model"
excerpt: "CS377: Database Design - Relational Data Model"

info:
  prev: ./RelationalModel
  
  goals: 
    - To implement database schemas into programming constructs using libraries and database engines
    - To describe and implement strategies for data provenance
  additional_reading:
    - link: https://pypi.org/project/PyMySQL/
      title: PyMySQL Python Library
    - link: https://docs.python.org/3/library/sqlite3.html
      title: Sqlite3 Python Library
    - link: https://www.tutorialspoint.com/postgresql/postgresql_python.htm
      title: PostgreSQL Python Library
  models:
    - model: |
        <script src="https://gist.github.com/BillJr99/53c92b77f465ba1f7259beeec31f50cb.js"></script>
        <br>
        <script src="https://gist.github.com/BillJr99/138231874d9d1c00bab4d20d1ff4267e.js"></script>
      title: Database Programming and SQL Library Support
      questions:
        - "Sketch the database schema implemented with the two programs (they are the same!)"
        - "What basic aggregation operations can you find in each program?"
        - "Why do you think there are two versions of this program, one for the Sqlite database engine, and one for the MySQL database engine?"
        
tags:
  - relational
  - programming  
---

## RDS Data Provenance

Relational Database Service (RDS) data provenance involves tracking and managing your data's origin, where it moves, and how it gets transformed over time. This is crucial for auditing, compliance, and data integrity.

### Storing Date Stamps and User History

To track changes in data over time, we can use date stamps and user history logging. Here's an example of how you might structure your SQL table to accommodate this:

```sql
CREATE TABLE example_table (
    id INT PRIMARY KEY,
    data VARCHAR(255),
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,
    created_by VARCHAR(255),
    updated_by VARCHAR(255)
);
```

In this table:

- `created_at` is the timestamp when the record was created.
- `updated_at` is the timestamp when the record was last updated.
- `created_by` is the user who created the record.
- `updated_by` is the user who last updated the record.

When inserting or updating data, you would include the user making the change:

```sql
INSERT INTO example_table (id, data, created_by, updated_by) VALUES (1, 'example', 'user1', 'user1');
UPDATE example_table SET data = 'new data', updated_by = 'user2' WHERE id = 1;
```

### Soft Deletes with "is_deleted" Flag

Instead of permanently deleting records with a SQL DELETE statement, you can use a "soft delete" approach. This involves adding an `is_deleted` flag to your table:

```sql
ALTER TABLE example_table ADD COLUMN is_deleted BOOLEAN DEFAULT 0;
```

To "delete" a record, you would set `is_deleted` to 1:

```sql
UPDATE example_table SET is_deleted = 1 WHERE id = 1;
```

The record remains in the database, but you treat it as deleted for all practical purposes. When querying data, you would typically exclude "deleted" records:

```sql
SELECT * FROM example_table WHERE is_deleted = 0;
```

This approach allows you to recover "deleted" data if necessary and provides a history of all data changes, including deletions.

Remember to consider the implications for your database's performance and storage, as "deleted" records will continue to occupy space.

## Evolving Data in RDS: Storing Medical Insurance Information

In the healthcare industry, it's crucial to track changes in a patient's insurance coverage over time. This report discusses the design of a relational database schema to store and manage this evolving data in an Amazon RDS instance.

### Database Design

The database design includes two main tables: `Person` and `Insurance`. The `Person` table stores information about individuals, while the `Insurance` table stores information about each person's insurance coverage over time.

#### Person Table

| Column Name | Data Type | Description |
|-------------|-----------|-------------|
| person_id   | INT       | Unique identifier for each person. Primary Key. |
| first_name  | VARCHAR   | First name of the person. |
| last_name   | VARCHAR   | Last name of the person. |

#### Insurance Table

| Column Name | Data Type | Description |
|-------------|-----------|-------------|
| insurance_id   | INT       | Unique identifier for each insurance record. Primary Key. |
| person_id      | INT       | Identifier for the person. Foreign Key referencing Person.person_id. |
| insurance_provider | VARCHAR | Name of the insurance provider. |
| start_date    | DATE      | Start date of the insurance coverage. |
| end_date      | DATE      | End date of the insurance coverage. Null if the insurance is currently active. |

### SQL Code Examples

#### Creating Tables

```sql
CREATE TABLE Person (
    person_id INT PRIMARY KEY,
    first_name VARCHAR(50),
    last_name VARCHAR(50),
    age INT,
    CHECK(age >= 0) -- what does this do?
);

CREATE TABLE Insurance (
    insurance_id INT PRIMARY KEY,
    person_id INT,
    insurance_provider VARCHAR(50),
    start_date DATE DEFAULT NOW,
    end_date DATE,
    FOREIGN KEY (person_id) REFERENCES Person(person_id)
);
```

#### Inserting Data

```sql
INSERT INTO Person (person_id, first_name, last_name)
VALUES (1, 'John', 'Doe');

INSERT INTO Insurance (insurance_id, person_id, insurance_provider, start_date, end_date)
VALUES (1, 1, 'Provider A', '2022-01-01', '2022-12-31');
```

#### Updating Data

```sql
UPDATE Insurance
SET end_date = '2023-12-31'
WHERE insurance_id = 1;
```

```sql
BEGIN TRANSACTION; -- what do you think this does?

UPDATE Insurance 
	SET end_date = current_timestamp()
	WHERE ID = (SELECT ID FROM Person WHERE last_name = "Smith");

INSERT INTO INSURANCE (PersonID, Provider) VALUES ((SELECT ID FROM Person WHERE last_name = "Smith"), "Acme Insurance");

COMMIT; -- ... and this?
```

#### Querying Data

To find a person's current active insurance coverage:

```sql
SELECT P.first_name, P.last_name, I.insurance_provider
FROM Person P
JOIN Insurance I ON P.person_id = I.person_id
WHERE I.end_date IS NULL;
```
