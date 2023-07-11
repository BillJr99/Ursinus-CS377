---
layout: notes
permalink: /Activities/Modeling/Normalization/Notes
title: "CS377: Database Design - Data Modeling and Normalization"
excerpt: "CS377: Database Design - Data Modeling and Normalization"
        
tags:
  - normalization
  - modeling
  
---

# Database Normalization

Database normalization is a process used to organize a database into tables and columns. The main idea with this is that a table should be about a specific topic and only supporting topics included. The purpose of normalization is to:

1. Eliminate redundant data
2. Ensure data dependencies make sense

There are three common forms of database normalization: 1st, 2nd, and 3rd normal form. They are also abbreviated as 1NF, 2NF, and 3NF respectively.

## First Normal Form (1NF)

For a table to be in the First Normal Form, it should follow the following 4 rules:

1. It should only have single (atomic) valued attributes/columns.
2. Values stored in a column should be of the same domain.
3. All the columns in a table should have unique names.
4. And the order in which data is stored, does not matter.

### Example

Original Table (Not Normalized):

| Order_ID | Product_ID | Product_Name | Customer_ID | Customer_Name | Country | Country_Code |
|----------|------------|--------------|-------------|---------------|---------|--------------|
| 1        | 101        | Product1     | 201         | Alice         | USA     | +1           |
| 2        | 102        | Product2     | 202         | Bob           | UK      | +44          |
| 3        | 103        | Product3     | 201         | Alice         | USA     | +1           |

After applying 1NF:

#### Orders Table

| Order_ID | Product_ID | Customer_ID |
|----------|------------|-------------|
| 1        | 101        | 201         |
| 2        | 102        | 202         |
| 3        | 103        | 201         |

#### Products Table

| Product_ID | Product_Name |
|------------|--------------|
| 101        | Product1     |
| 102        | Product2     |
| 103        | Product3     |

#### Customers Table

| Customer_ID | Customer_Name | Country |
|-------------|---------------|---------|
| 201         | Alice         | USA     |
| 202         | Bob           | UK      |

## Second Normal Form (2NF)

For a table to be in the Second Normal Form,

1. It should be in the First Normal form.
2. And, it should not have Partial Dependency.

A partial dependency occurs when a non-prime attribute (an attribute that doesn't belong to any candidate key) is dependent on a part of a candidate key.

### Example

After applying 2NF:

#### Orders Table

| Order_ID | Product_ID | Customer_ID |
|----------|------------|-------------|
| 1        | 101        | 201         |
| 2        | 102        | 202         |
| 3        | 103        | 201         |

#### Products Table

| Product_ID | Product_Name |
|------------|--------------|
| 101        | Product1     |
| 102        | Product2     |
| 103        | Product3     |

#### Customers Table

| Customer_ID | Customer_Name | Country |
|-------------|---------------|---------|
| 201         | Alice         | USA     |
| 202         | Bob           | UK      |

## Third Normal Form (3NF)

A table is said to be in the Third Normal Form when,

1. It is in the Second Normal form.
2. And, it does not have Transitive Dependency.

A transitive dependency occurs when a non-prime attribute is dependent on another non-prime attribute.

### Example

After applying 3NF:

#### Orders Table

| Order_ID | Product_ID | Customer_ID |
|----------|------------|-------------|
| 1        | 101        | 201         |
| 2        | 102        | 202         |
| 3        | 103        | 201         |

#### Products Table

| Product_ID | Product_Name |
|------------|--------------|
| 101        | Product1     |
| 102        | Product2     |
| 103        | Product3     |

#### Customers Table

| Customer_ID | Customer_Name | Country |
|-------------|---------------|---------|
| 201         | Alice         | USA     |
| 202         | Bob           | UK      |

#### Countries Table

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