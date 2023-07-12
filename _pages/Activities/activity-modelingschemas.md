---
layout: activity
permalink: /Activities/Modeling/Schemas
title: "CS377: Database Design - Data Modeling and Schemas"
excerpt: "CS377: Database Design - Data Modeling and Schemas"

info:
  goals: 
    - To identify use cases appropriate to the relational, network, and hierarchical database model
    - To create database schemas in standardized formats
    
  models:
    - model: |
        <img src="https://opentextbc.ca/wp-content/uploads/sites/11/2013/12/Network-data-model-300x244.jpg" alt="The Network Data Model from Database Design 2nd Ed by Watt and Eng">
        <br>
        <img src="https://opentextbc.ca/wp-content/uploads/sites/11/2013/12/Hierarchical-Data-Model-300x116.jpg" alt="The Hierarchical Data Model from Database Design 2nd Ed by Watt and Eng">
      title: Network and Hierarchical Data Models
      questions:
        - "What do edges (or vertices) represent in each model?"
        - "Do these edges represent 1:1 or 1:many relationships?"
        - "How might you implement each of these models using the traditional relational database model?"
        - "Sketch a model of the student enrollment tables we made previously in the hierarchical model."
        - "Design tables and keys to represent the manager-employee hierarchical model."
    - model: |
        <a title="Timo Tijhof, CC BY 4.0 &lt;https://creativecommons.org/licenses/by/4.0&gt;, via Wikimedia Commons" href="https://commons.wikimedia.org/wiki/File:MediaWiki_1.28.0_database_schema.svg"><img width="512" alt="MediaWiki 1.28.0 database schema" src="https://upload.wikimedia.org/wikipedia/commons/thumb/9/94/MediaWiki_1.28.0_database_schema.svg/512px-MediaWiki_1.28.0_database_schema.svg.png"></a>
      title: Database Schemas 
      questions:
        - "Draw lines between the foreign keys that you find and their primary keys.  What do you notice about these lines, with respect to the clusters of tables?"
        - "Which tables need to be modified to add a log message to the database?  Do any records need to be modified elsewhere?  How might you define the concept of <strong>physical data independence</strong> based on this idea?"
        - "How might you define <strong>logical independence</strong> (independence within the schema itself), given our definition of physical independence?"

  additional_reading:
    - link: https://dbdiagram.io/home
      title: "dbdiagram.io"  
    - link: https://dev.to/techschoolguru/design-db-schema-and-generate-sql-code-with-dbdiagram-io-4ko5
      title: "Design DB Schema and Generate SQL Code with dbdiagram"
      
tags:
  - models
  - schemas  
---

## Data Modeling
Data modeling is the process of structuring and organizing data to effectively represent the real-world entities and relationships it represents. A schema is a blueprint or a plan that describes the structure and organization of a database system. This report will explore the fundamentals of data modeling, various types of schemas, and their importance in the context of database design.

### Definition
Data modeling is the process of creating a conceptual representation of data objects, their attributes, and the relationships between them. It helps in creating a clear understanding of the data requirements and aids in effective communication among stakeholders.

### Types of Data Models
1. **Conceptual Data Model**: This model represents high-level entities, their attributes, and the relationships between them. It focuses on understanding and documenting concepts rather than implementation details.
2. **Logical Data Model**: The logical data model focuses on translating the conceptual model into a more detailed structure that can be implemented in a specific database management system (DBMS). It defines the tables, columns, relationships, and constraints.
3. **Physical Data Model**: The physical data model specifies how the logical data model will be implemented within a specific DBMS. It includes details such as data types, indexes, partitions, and storage details.

### Benefits of Data Modeling
- **Structural Clarity**: Data modeling provides a clear structure for organizing and understanding data, improving the overall quality and consistency of the database.
- **Data Integrity**: By defining relationships and constraints, data modeling ensures the integrity of the data, preventing inconsistencies and errors.
- **Efficient Querying**: Well-designed data models enable efficient querying, as they optimize the use of indexes, partitions, and other database features.
- **Scalability and Flexibility**: Data modeling helps in designing databases that can scale and adapt to changing requirements without major restructuring or data loss.

### Implementing Data Models with Python
Python provides several libraries and frameworks that facilitate data modeling and database design. One such popular library is SQLAlchemy. SQLAlchemy is an Object-Relational Mapping (ORM) tool that enables developers to work with databases using Python classes and objects. It provides a high-level, expressive approach to working with databases, making data modeling and schema design more convenient and intuitive.

Here's a simple example of creating a data model using SQLAlchemy:

```python
from sqlalchemy import create_engine, Column, Integer, String
from sqlalchemy.ext.declarative import declarative_base

# Create a database engine
engine = create_engine('sqlite:///mydatabase.db', echo=True)

# Define the base class for data models
Base = declarative_base()

# Define a data model class
class User(Base):
    __tablename__ = 'users'
    id = Column(Integer, primary_key=True)
    name = Column(String)
    email = Column(String)

# Create the tables in the database
Base.metadata.create_all(engine)
```

This example demonstrates the creation of a simple "User" data model with SQLAlchemy, defining the table name, column names, and their data types. The `create_all` method creates the corresponding table in the database specified by the engine.

## Schemas
### Definition
A schema is a logical structure that represents the organization and design of a database system. It defines the tables, columns, relationships, constraints, and other elements that constitute the database.

### Types of Schemas
1. **Physical Schema**: The physical schema defines how the data is physically stored and organized on disk. It includes details such as file structures, indices, and storage methods.
2. **Logical Schema**: The logical schema represents the structure and organization of data at a higher level of abstraction, independent of the physical storage details. It focuses on the relationships and constraints between tables and provides a conceptual view of the data.
3. **External Schema**: An external schema is a subset of the logical schema, providing a view of the database tailored to the requirements of specific user groups or applications. It defines the tables and columns accessible to the user or application.

### Benefits of Schemas
- **Data Organization**: Schemas provide a structured and organized way to store and access data, enabling efficient data retrieval and management.
- **Data Security**: Schemas can be used to control access to specific tables or columns, ensuring data security and privacy.
- **Data Consistency**: By enforcing relationships and constraints, schemas maintain data consistency and integrity across the database.
- **Modularity and Scalability**: Schemas allow for modular design, where changes can be made to specific schema components without impacting the entire database. This also enables scalability by allowing for distributed and parallel processing.

### Research and Further Reading

1. Codd, E. F. (1970). **A Relational Model of Data for Large Shared Data Banks**. *Communications of the ACM, 13(6)*. [Link](https://dl.acm.org/doi/10.1145/362384.362685)
2. Batini, C., & Navathe, S. B. (1986). **Conceptual Database Design: An Entity-Relationship Approach**. *Addison-Wesley*.
3. Oracle. **Database Concepts**. *Oracle Database Documentation*. [Link](https://docs.oracle.com/en/database/oracle/oracle-database/12.2/cncpt/introduction-to-the-oracle-database.html)
4. Chong, F. W. K., Lee, M. L., Ling, T. W., & J. S. (2001). **A Multi-Relational Extension to UML Class Diagram for Advanced Database Schema Design**. *Proceedings of the 4th International Conference on the Entity-Relationship Approach*. [Link](https://dl.acm.org/doi/10.5555/780225.780235)

Data modeling and schemas are essential components of database design. By creating clear, structured representations of data, data modeling enables effective communication, data integrity, and efficient querying. Schemas, on the other hand, provide a logical and physical structure to organize and manage data. Properly designed data models and schemas are crucial for building scalable, maintainable, and secure databases.