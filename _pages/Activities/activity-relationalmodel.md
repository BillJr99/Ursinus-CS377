---
layout: activity
permalink: /Activities/RelationalModel
title: "CS377: Database Design - Relational Data Model"


info:
  next: ./RelationalModel2
  
  goals: 
    - To express database table relationships through mathematical abstraction
    - To describe the advantages and disadvantages of different database engines
  additional_reading:
    - link: https://github.com/comptoolsres/Jupyter_content/blob/main/py4e_ch15_databases.ipynb
      title: Databases and SQL
  models:
    - model: |
        <table style="border-collapse:collapse;border-spacing:0" class="tg"><thead><tr><th style="background-color:#000000;border-color:inherit;border-style:solid;border-width:1px;color:#ffffff;font-family:Arial, sans-serif;font-size:14px;font-weight:normal;overflow:hidden;padding:10px 5px;text-align:center;vertical-align:top;word-break:normal">FirstName</th><th style="background-color:#000000;border-color:inherit;border-style:solid;border-width:1px;color:#ffffff;font-family:Arial, sans-serif;font-size:14px;font-weight:normal;overflow:hidden;padding:10px 5px;text-align:center;vertical-align:top;word-break:normal">LastName</th><th style="background-color:#000000;border-color:inherit;border-style:solid;border-width:1px;color:#ffffff;font-family:Arial, sans-serif;font-size:14px;font-weight:normal;overflow:hidden;padding:10px 5px;text-align:center;vertical-align:top;word-break:normal">Age</th></tr></thead><tbody><tr><td style="border-color:inherit;border-style:solid;border-width:1px;font-family:Arial, sans-serif;font-size:14px;overflow:hidden;padding:10px 5px;text-align:left;vertical-align:top;word-break:normal">Alex</td><td style="border-color:inherit;border-style:solid;border-width:1px;font-family:Arial, sans-serif;font-size:14px;overflow:hidden;padding:10px 5px;text-align:left;vertical-align:top;word-break:normal">Smith</td><td style="border-color:inherit;border-style:solid;border-width:1px;font-family:Arial, sans-serif;font-size:14px;overflow:hidden;padding:10px 5px;text-align:left;vertical-align:top;word-break:normal">20</td></tr><tr><td style="border-color:inherit;border-style:solid;border-width:1px;font-family:Arial, sans-serif;font-size:14px;overflow:hidden;padding:10px 5px;text-align:left;vertical-align:top;word-break:normal">Lee</td><td style="border-color:inherit;border-style:solid;border-width:1px;font-family:Arial, sans-serif;font-size:14px;overflow:hidden;padding:10px 5px;text-align:left;vertical-align:top;word-break:normal">Jones</td><td style="border-color:inherit;border-style:solid;border-width:1px;font-family:Arial, sans-serif;font-size:14px;overflow:hidden;padding:10px 5px;text-align:left;vertical-align:top;word-break:normal">21</td></tr><tr><td style="border-color:inherit;border-style:solid;border-width:1px;font-family:Arial, sans-serif;font-size:14px;overflow:hidden;padding:10px 5px;text-align:left;vertical-align:top;word-break:normal">Brian</td><td style="border-color:inherit;border-style:solid;border-width:1px;font-family:Arial, sans-serif;font-size:14px;overflow:hidden;padding:10px 5px;text-align:left;vertical-align:top;word-break:normal">McMullen</td><td style="border-color:inherit;border-style:solid;border-width:1px;font-family:Arial, sans-serif;font-size:14px;overflow:hidden;padding:10px 5px;text-align:left;vertical-align:top;word-break:normal">18</td></tr><tr><td style="border-color:inherit;border-style:solid;border-width:1px;font-family:Arial, sans-serif;font-size:14px;overflow:hidden;padding:10px 5px;text-align:left;vertical-align:top;word-break:normal">Samantha</td><td style="border-color:inherit;border-style:solid;border-width:1px;font-family:Arial, sans-serif;font-size:14px;overflow:hidden;padding:10px 5px;text-align:left;vertical-align:top;word-break:normal">Johnson</td><td style="border-color:inherit;border-style:solid;border-width:1px;font-family:Arial, sans-serif;font-size:14px;overflow:hidden;padding:10px 5px;text-align:left;vertical-align:top;word-break:normal">22</td></tr><tr><td style="border-color:black;border-style:solid;border-width:1px;font-family:Arial, sans-serif;font-size:14px;overflow:hidden;padding:10px 5px;text-align:left;vertical-align:top;word-break:normal">Lee</td><td style="border-color:black;border-style:solid;border-width:1px;font-family:Arial, sans-serif;font-size:14px;overflow:hidden;padding:10px 5px;text-align:left;vertical-align:top;word-break:normal">Jones</td><td style="border-color:black;border-style:solid;border-width:1px;font-family:Arial, sans-serif;font-size:14px;overflow:hidden;padding:10px 5px;text-align:left;vertical-align:top;word-break:normal">24</td></tr></tbody></table>
        <br>
        <span>\(FirstName \times LastName \times Age = \{(firstname, lastname, age) : firstname \in \{a-zA-Z\}+, lastname \in \{a-zA-Z\}+, age \in \mathbb{Z}^{+}\}\)</span>
      title: Domains and Relations
      questions:
        - "If the <strong>domain</strong> of the <code>Age</code> field is all positive numbers <code>Age > 0</code>, what is the domain of <code>FirstName</code>?"
        - "Translate the cartesian product formula into your own words describing the nature of the table it defines."
        - "This table relation has degree 3.  What do you think that means?"
        - "Is it ever appropriate to have the same row in a table more than once?  What is the alternative if such a situation is needed?"
        - "Suppose you wish to track the history and provenance of a record.  For example, if someone changes their name, a record of both names and the dates during which each name was valid would be included.  What tables and fields might you add to do this?"
        
tags:
  - relational
  - programming  
---

## Relational Database Model

The relational database model is a popular and widely used approach to structuring and organizing data. It consists of tables that store data in rows and columns, where each row represents a record or tuple, and each column represents a specific attribute or field. The relationships between tables are established using primary and foreign keys.  Relational databases provide a structured way to store, retrieve, and manage large amounts of data. This report serves as course notes for understanding the relational database model and database programming using Python.

### Key Concepts
The relational database model is based on the principles of logic and set theory. It organizes data into tables, where each table represents an entity, and each row represents a specific instance of that entity. The relationships between entities are established through keys, such as primary and foreign keys.

- **Tables**: A table represents a specific entity and consists of columns (attributes) and rows (records).
- **Keys**: Keys are used to uniquely identify records in a table. Primary keys are unique identifiers for a table, while foreign keys establish relationships with other tables.
- **Relationships**: Relationships define how tables are linked together using keys. Common relationships include one-to-one, one-to-many, and many-to-many.

## Database Programming with Python
To manipulate and interact with relational databases programmatically in Python, we can utilize various libraries and APIs. Here are some key resources that provide useful information on this topic:

- **PyMySQL Python Library**: PyMySQL is a pure-Python MySQL client library that provides a straightforward way to connect to and interact with MySQL databases. It offers a comprehensive set of functions and methods for executing SQL statements, managing transactions, and handling errors. More information can be found in the [PyMySQL documentation](https://pypi.org/project/PyMySQL/).

- **Sqlite3 Python Library**: Sqlite3 is a built-in Python library that provides an interface for working with SQLite databases. SQLite is a serverless, file-based database engine that allows for easy implementation and usage of relational databases. The Sqlite3 library offers functions for creating, querying, and modifying SQLite databases. Detailed documentation is available in the [Python documentation](https://docs.python.org/3/library/sqlite3.html).

- **PostgreSQL Python Library**: PostgreSQL is a powerful and feature-rich open-source relational database system. There are multiple Python libraries available for interacting with PostgreSQL databases. One of the most commonly used libraries is psycopg2, which provides a simple and efficient way to connect to and work with PostgreSQL databases in Python. A tutorial on using psycopg2 can be found at [TutorialsPoint](https://www.tutorialspoint.com/postgresql/postgresql_python.htm).

### PyMySQL Python Library
[PyMySQL](https://pypi.org/project/PyMySQL/) is a pure Python client library for MySQL databases. It provides a convenient way to interact with MySQL databases using Python.

**Example:**
```python
import pymysql

# Connect to the MySQL database
connection = pymysql.connect(host='localhost', user='username', password='password', database='dbname')

# Execute a SQL query
cursor = connection.cursor()
cursor.execute("SELECT * FROM users")

# Fetch all records
results = cursor.fetchall()

# Close the connection
connection.close()
```

### Sqlite3 Python Library
[Sqlite3](https://docs.python.org/3/library/sqlite3.html) is a built-in Python library that provides a lightweight and self-contained SQLite database module. It allows Python programs to access the SQLite database files.

**Example:**
```python
import sqlite3

# Connect or create a SQLite database
connection = sqlite3.connect('database.db')

# Create a cursor object
cursor = connection.cursor()

# Execute a SQL query
cursor.execute("SELECT * FROM users")

# Fetch all records
results = cursor.fetchall()

# Close the connection
connection.close()
```

### PostgreSQL Python Library
[psycopg2](https://www.tutorialspoint.com/postgresql/postgresql_python.htm) is a PostgreSQL adapter for the Python programming language. It allows Python programs to interact with PostgreSQL databases.

**Example:**
```python
import psycopg2

# Connect to the PostgreSQL database
connection = psycopg2.connect(host='localhost', user='username', password='password', database='dbname')

# Create a cursor object
cursor = connection.cursor()

# Execute a SQL query
cursor.execute("SELECT * FROM users")

# Fetch all records
results = cursor.fetchall()

# Close the connection
connection.close()
```
