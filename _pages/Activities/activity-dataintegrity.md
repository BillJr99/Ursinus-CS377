---
layout: activity
permalink: /Activities/DataIntegrity
title: "CS377: Database Design - Data Integrity"


info:
  goals: 
    - To differentiate between domain and integrity constraints
    
  models:
    - model: |
        <script type="syntaxhighlighter" class="brush: sql"><![CDATA[        
        -- Employees Table
        CREATE TABLE EMPLOYEE (
            ID INTEGER NOT NULL PRIMARY KEY AUTOINCREMENT, 
            FirstName TEXT NOT NULL, 
            LastName TEXT NOT NULL, 
            Age INTEGER,
            SMOKER INTEGER DEFAULT 0
        );
        
        -- Spouse Table
        CREATE TABLE SPOUSE (
            ID INTEGER NOT NULL PRIMARY KEY AUTOINCREMENT, 
            EmployeeID INTEGER NOT NULL,
            FirstName TEXT NOT NULL, 
            LastName TEXT NOT NULL, 
            Age INTEGER,
            SMOKER INTEGER DEFAULT 0,
            FOREIGN KEY(EmployeeID) REFERENCES EMPLOYEES(ID)
        );

        -- Child Table
        CREATE TABLE CHILD (
            ID INTEGER NOT NULL PRIMARY KEY AUTOINCREMENT, 
            EmployeeID INTEGER NOT NULL,
            FirstName TEXT NOT NULL, 
            LastName TEXT NOT NULL, 
            Age INTEGER,
            SMOKER INTEGER DEFAULT 0,
            FOREIGN KEY(EmployeeID) REFERENCES EMPLOYEES(ID)
        );        
        ]]></script>
      title: Domain and Integrity Constraints
      questions:
        - "The <strong>domain</strong> of the <code>SMOKER</code> attribute is all positive integers, but it is really intended to be <code>0</code> or <code>1</code>.  This is an <code>integrity constraint</code> since it cannot be restricted syntactically by the domain (although some SQL engines do support boolean data types!).  What other integrity constraints do you see in this table?"
        - "Describe a potential <strong>referential integrity</strong> violation that could occur within this database if records can be deleted from the <code>EMPLOYEE</code> table without checking the <code>SPOUSE</code> table first."
        - "What should be done in the <code>EMPLOYEE</code> table if an entry is deleted in the <code>SPOUSE</code> table?"
        - "Draw this schema, and indicate the cardinality of each relationship (1:1, 1:many, optional)."
        - "What inefficiency exists within this table?  Could someone be a spouse of one person and a child of another?  Re-design this schema to eliminate redundant data storage."
        - "What do you think a <a href=https://www.w3schools.com/sql/sql_check.asp>CHECK Constraint</a> does?"
        
tags:
  - integrity
  
---

## Data Integrity

Data integrity refers to the accuracy, completeness, consistency, and reliability of data throughout its lifecycle. It ensures that data remains unchanged, complete, and valid from creation to deletion. Maintaining data integrity is crucial as it supports data quality, enhances decision-making, and promotes trust in the data.

Data integrity is essential in various domains, including finance, healthcare, e-commerce, and scientific research. Here are some reasons why data integrity is important:

1. **Trustworthiness**: Ensuring data integrity builds trust among users who rely on the accuracy and consistency of data for decision-making.
2. **Compliance**: Many industries have regulatory requirements for data integrity, such as HIPAA in healthcare or Sarbanes-Oxley Act in finance.
3. **Efficiency**: Accurate and reliable data streamlines business processes, reduces errors, and improves efficiency.
4. **Data Analysis**: High data integrity enables accurate and meaningful analysis, leading to more informed decisions and insights.

### Maintaining Data Integrity

To maintain data integrity, several techniques and practices can be employed:

1. **Data Validation**: Validate data during entry to ensure it meets predefined criteria. This can involve techniques such as data type checks, format validations, and range validations.
2. **Access Controls**: Implement access controls and user permissions to prevent unauthorized modifications to data.
3. **Backup and Recovery**: Regularly backup data and establish recovery procedures to restore data in case of accidental or intentional corruption.
4. **Version Control**: Use version control systems to track changes made to data and provide mechanisms for reverting to previous versions if necessary.
5. **Hash Functions**: Utilize cryptographic hash functions to generate a unique hash value for data. Comparisons of hashes can be used to verify data integrity.

## Elementary Data Integrity

### Profiling and Summarizing Data in Python Using Pandas

We can search for missing values per the following example:

```python
import pandas as pd

# Load dataset
df = pd.read_csv("dataset.csv")

# Data profiling
print("Data Shape:", df.shape)
print("Data Summary:")
print(df.describe())
print("Missing Values:")
print(df.isnull().sum())
```

### Data Cleansing in Python Using Pandas

We can remove duplicate data from a pandas dataframe as follows:

```python
import pandas as pd

# Load dataset
df = pd.read_csv("dataset.csv")

# Remove duplicate entries
df.drop_duplicates(inplace=True)

# Save cleansed dataset
df.to_csv("cleansed_dataset.csv", index=False)
```

## Ensuring Data Integrity with Python

Python offers various libraries and techniques to maintain data integrity. Here are a few examples:

### Data Validation with `pydantic`

`pydantic` is a lightweight library that provides runtime data validation and parsing for Python.

Example:
```python
from pydantic import BaseModel

class User(BaseModel):
    name: str
    age: int

user_data = {"name": "John", "age": "25"}
user = User(**user_data)  # Raises a validation error due to an invalid age field
```

### Hash Functions with the `hashlib` Module

The `hashlib` module in Python provides access to various secure hash and message digest algorithms.

Example:
```python
import hashlib

def calculate_hash(data):
    hasher = hashlib.sha256()
    hasher.update(data.encode())
    return hasher.hexdigest()

original_data = "Hello, World!"
hash_value = calculate_hash(original_data)  # Calculate hash value
print(hash_value)

modified_data = "Hello, World!!"
modified_hash_value = calculate_hash(modified_data)  # Calculate hash value
print(modified_hash_value)

print(hash_value == modified_hash_value)  # False, indicating data modification
```
