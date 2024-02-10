---
layout: activity
permalink: /Activities/Modeling/Normalization
title: "CS377: Database Design - Data Modeling and Normalization"


info:
  goals: 
    - To model database dependencies using a formal notation
    - To normalize database schemas at varying degrees (first, second, and third normal forms)
        
  models:
    - model: |
        <span>\(SSN \longrightarrow Name\)</span>
        <br>
        <span>\(SSN, PhoneNumber \longrightarrow Name, PhoneNumber\)</span>
        <br>
        <span>\(SSN \longrightarrow Name\)</span>, <span>\(Name \longrightarrow Address\)</span>
      title: "Determinant / Dependent Relationships"
      questions:
        - "What is the <strong>determinant</strong> attribute and the <strong>dependent</strong> attribute above?  In other words, if you know the determinant, you can look up the dependent value?"
        - "What determinant / dependent relationships can you find from the data schema in the <a href=\"../ERModel\">ER Modeling Activity</a>?"
        - "Is a primary key a determinant or a dependent?  How about records with a foreign key?"
        - "Describe, in your own words, the axiom of augmentation from the second rule above."
        - "The <code>Phone Number</code> field should not be part of the primary key; how can we break up this relationship to create a normalized schema?" 
        - "Describe the axiom of transitivity, showing that <code>Address</code> ultimately depends upon <code>SSN</code> from the third relationship above."         
    - model: |
        <img src="../../images/unnormalized.png" alt="Unnormalized data schema from https://en.wikipedia.org/wiki/Database_normalization under a Creative Commons Attribution-ShareAlike License">
        <br>
        There are many normal forms, and you have been following <strong>unnormalized form</strong> already because you incorporate a primary key in your tables!  We will explore first, second, and third normal forms.
      title: Normalization and Normal Forms
      questions:
        - "The database contains multiple values within one column (<code>Subject</code>).  Normalize to first normal form (1NF) by re-designing this schema to make Subject a dependency in another table, and thus make the <code>Subject</code> value <strong>atomic</strong> (singular valued)."
        - "What is the composite primary key of this table?  To establish second normal form (2NF), establish a single column primary key.  Move the composite key columns into their own table that you can link via a foreign key."
        - "To establish third normal form (3NF), identify any transitive dependencies, and create separate tables for each group of related columns.  This way, no non-key field values depend on one another within the same table."
        - "Sixth normal form (6NF) states that each row contains a primary key and just one additional column!  What is the major drawback that precludes 6NF in practice?  What benefit might be obtained if 6NF were achieved?"
        - "Suppose you have a table with a person's entire postal address in a single column.  How would you normalize this to 1NF?"
        
tags:
  - normalization
  - modeling
  
---

## Overview of Normalization

Normalization is a process of organizing data in a database to eliminate redundancy and dependencies. It ensures that each attribute in a table depends only on the table's primary key and not on any other non-key attributes. Normalization is divided into several normal forms, each addressing a specific type or level of data redundancy.

The following are the commonly used normalization forms:

- **First Normal Form (1NF):** In this form, the data is organized into tables where each column has a single value, and each row is unique. There should be no repeating groups or arrays of data within a table.

- **Second Normal Form (2NF):** In addition to the requirements of 1NF, this form eliminates partial dependencies. A partial dependency occurs when a non-key attribute depends on only a part of the primary key.

- **Third Normal Form (3NF):** In addition to the requirements of 2NF, this form eliminates transitive dependencies. A transitive dependency occurs when a non-key attribute depends on another non-key attribute, which itself depends on the primary key.

Normalization helps in improving database performance, reducing data duplication, and maintaining data consistency. By eliminating redundancy, it minimizes the chances of data inconsistency and update anomalies.

### ER Modeling in Python Example

We can define entities, relationships, and attributes using Python classes and demonstrate normalization techniques.

```python
from sqlalchemy import Column, Integer, String, ForeignKey
from sqlalchemy.orm import relationship
from sqlalchemy.ext.declarative import declarative_base

Base = declarative_base()

class Author(Base):
    __tablename__ = 'authors'
    id = Column(Integer, primary_key=True)
    name = Column(String)

class Book(Base):
    __tablename__ = 'books'
    id = Column(Integer, primary_key=True)
    title = Column(String)
    author_id = Column(Integer, ForeignKey('authors.id'))
    author = relationship('Author', backref='books')

class Order(Base):
    __tablename__ = 'orders'
    id = Column(Integer, primary_key=True)
    book_id = Column(Integer, ForeignKey('books.id'))
    book = relationship('Book')

class Customer(Base):
    __tablename__ = 'customers'
    id = Column(Integer, primary_key=True)
    name = Column(String)
    order_id = Column(Integer, ForeignKey('orders.id'))
    order = relationship('Order')

# Create tables and relationships
Base.metadata.create_all()
```

In the above example, we defined the entities `Author`, `Book`, `Order`, and `Customer` using Python classes. We also defined relationships between entities using foreign keys and established associations using SQLAlchemy.

## Database Normalization

Database normalization is a process used to organize a database into tables and columns. The main idea with this is that a table should be about a specific topic and only supporting topics included. The purpose of normalization is to:

1. Eliminate redundant data
2. Ensure data dependencies make sense

There are three common forms of database normalization: 1st, 2nd, and 3rd normal form. They are also abbreviated as 1NF, 2NF, and 3NF respectively.  There are additional levels of normalization as well, which apply stricter rules to establish "normality."

The tables below can be expressed in ER modeling tools such as SQLAlchemy; however, we will visualize them at a high level to explore how tables, relationships, and keys should be organized at each normalization level.

### First Normal Form (1NF)

For a table to be in the First Normal Form, it should follow the following 4 rules:

1. It should only have single (atomic) valued attributes/columns.
2. Values stored in a column should be of the same domain.
3. All the columns in a table should have unique names.
4. And the order in which data is stored, does not matter.

#### Example

Original Table (Not Normalized):

| Order_ID | Product_ID | Product_Name | Customer_ID | Customer_Name | Country | Country_Code |
|----------|------------|--------------|-------------|---------------|---------|--------------|
| 1        | 101        | Product1     | 201         | Alice         | USA     | +1           |
| 2        | 102        | Product2     | 202         | Bob           | UK      | +44          |
| 3        | 103        | Product3     | 201         | Alice         | USA     | +1           |

After applying 1NF:

##### Orders Table

| Order_ID | Product_ID | Customer_ID |
|----------|------------|-------------|
| 1        | 101        | 201         |
| 2        | 102        | 202         |
| 3        | 103        | 201         |

##### Products Table

| Product_ID | Product_Name |
|------------|--------------|
| 101        | Product1     |
| 102        | Product2     |
| 103        | Product3     |

##### Customers Table

| Customer_ID | Customer_Name | Country |
|-------------|---------------|---------|
| 201         | Alice         | USA     |
| 202         | Bob           | UK      |

### Second Normal Form (2NF)

For a table to be in the Second Normal Form,

1. It should be in the First Normal form.
2. And, it should not have Partial Dependency.

A partial dependency occurs when a non-prime attribute (an attribute that doesn't belong to any candidate key) is dependent on a part of a candidate key.

#### Example

After applying 2NF:

##### Orders Table

| Order_ID | Product_ID | Customer_ID |
|----------|------------|-------------|
| 1        | 101        | 201         |
| 2        | 102        | 202         |
| 3        | 103        | 201         |

##### Products Table

| Product_ID | Product_Name |
|------------|--------------|
| 101        | Product1     |
| 102        | Product2     |
| 103        | Product3     |

##### Customers Table

| Customer_ID | Customer_Name | Country |
|-------------|---------------|---------|
| 201         | Alice         | USA     |
| 202         | Bob           | UK      |

### Third Normal Form (3NF)

A table is said to be in the Third Normal Form when,

1. It is in the Second Normal form.
2. And, it does not have Transitive Dependency.

A transitive dependency occurs when a non-prime attribute is dependent on another non-prime attribute.

#### Example

After applying 3NF:

##### Orders Table

| Order_ID | Product_ID | Customer_ID |
|----------|------------|-------------|
| 1        | 101        | 201         |
| 2        | 102        | 202         |
| 3        | 103        | 201         |

##### Products Table

| Product_ID | Product_Name |
|------------|--------------|
| 101        | Product1     |
| 102        | Product2     |
| 103        | Product3     |

##### Customers Table

| Customer_ID | Customer_Name | Country |
|-------------|---------------|---------|
| 201         | Alice         | USA     |
| 202         | Bob           | UK      |

##### Countries Table

| Country | Country_Code |
|---------|--------------|
| USA     | +1           |
| UK      | +44          |

Python example that creates the 3NF tables:

```python
import sqlite3

# Connect to the SQLite database
conn = sqlite3.connect('orders.db')

# Create a cursor object
c = conn.cursor()

# Create table Orders
c.execute('''
    CREATE TABLE Orders(
        Order_ID INT PRIMARY KEY NOT NULL,
        Product_ID INT NOT NULL,
        Customer_ID INT NOT NULL);
''')

# Create table Products
c.execute('''
    CREATE TABLE Products(
        Product_ID INT PRIMARY KEY NOT NULL,
        Product_Name TEXT NOT NULL);
''')

# Create table Customers
c.execute('''
    CREATE TABLE Customers(
        Customer_ID INT PRIMARY KEY NOT NULL,
        Customer_Name TEXT NOT NULL,
        Country TEXT NOT NULL);
''')

# Create table Countries
c.execute('''
    CREATE TABLE Countries(
        Country TEXT PRIMARY KEY NOT NULL,
        Country_Code TEXT NOT NULL);
''')

# Insert data into Orders table
orders = [(1, 101, 201), (2, 102, 202), (3, 103, 201)]
c.executemany('INSERT INTO Orders VALUES (?,?,?)', orders)

# Insert data into Products table
products = [(101, 'Product1'), (102, 'Product2'), (103, 'Product3')]
c.executemany('INSERT INTO Products VALUES (?,?)', products)

# Insert data into Customers table
customers = [(201, 'Alice', 'USA'), (202, 'Bob', 'UK')]
c.executemany('INSERT INTO Customers VALUES (?,?,?)', customers)

# Insert data into Countries table
countries = [('USA', '+1'), ('UK', '+44')]
c.executemany('INSERT INTO Countries VALUES (?,?)', countries)

# Commit the transaction
conn.commit()

# Close the connection
conn.close()
```
