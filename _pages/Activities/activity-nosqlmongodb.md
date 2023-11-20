---
layout: activity
permalink: /Activities/NoSQL
title: "CS377: Database Design - NoSQL"
excerpt: "CS377: Database Design - NoSQL"

info:
  goals: 
    - To explain the difference between a relational table and a NoSQL Collection
    - To utilize MongoDB to store unstructured records
    
  models:
    - model: |
        <img src="https://web.archive.org/web/20210303013947/https://docs.mongodb.com/manual/_images/crud-annotated-collection.bakedsvg.svg" alt="MongoDB Collections from mongodb.com" />
      title: Unstructured Data Stores
      embed: <iframe height="400px" width="100%" src="https://repl.it/@BillJr99/PythonMongoDBExample?lite=true" scrolling="no" frameborder="no" allowtransparency="true" allowfullscreen="true" sandbox="allow-forms allow-pointer-lock allow-popups allow-same-origin allow-scripts allow-modals"></iframe>        
      questions:
        - "Create a Cluster at <a href=\"http://mongodb.com\">MongoDB.com</a>, and a user to access it.  Allow network access, and click the <code>Connect</code> button to obtain a database connection string.  The repl.it example code comments contain instructions on how to pass the database parameters (like the password) as environment variables, so that you do not have to embed them in your program code.  Run the given example against your collection."
        - What is the format of the data being stored in a NoSQL collection?
        - Do you think you could lookup relational data in a NoSQL collection?  Why or why not?
        - How might a NoSQL collection make things easier when dealing with a web service that communicates JSON between the browser and the server?
        - "How might a <strong>collection</strong> compare to a table, and what is a <strong>document</strong> in this model?"
        - "Are collections typically normalized?  How can you tell?"
        - "What are the implications of denormalized, unstructured data stores?"
        - "In the code example, what is the collection and what is the document?"
        - "Which <strong>field</strong> do you think is indexed in the collection?"
        - "Try inserting an additional document in the code example above, but with a different set of fields.  Does it work?  Based on this, do NoSQL collections have schemas?"
        
tags:
  - nosql
  
---

## A Non-Relational SQL Model - NoSQL

In recent years, there has been a significant increase in the volume and complexity of data being generated. This surge in data has led to the development of new database models that can handle the challenges posed by such large-scale datasets. One of these models is NoSQL, which stands for "not only SQL". NoSQL databases offer a flexible and scalable approach to data storage and retrieval, without the strict schema requirements of traditional relational databases. In this report, we will explore the concepts and characteristics of NoSQL databases, and provide examples and references to enhance understanding.

### Characteristics of NoSQL Databases

NoSQL databases are built upon different data models and have several key characteristics that distinguish them from traditional relational databases:

1. **Flexible and dynamic schema**: NoSQL databases offer a schema-less approach, allowing for the storage of data without a predefined schema. This flexibility enables developers to handle evolving data structures and make faster iterations in database design.

2. **Scalability**: NoSQL databases are designed to scale horizontally, meaning that they can handle increasing amounts of data by adding more servers to a distributed system. This makes NoSQL databases suitable for big data applications with high scalability requirements.

3. **High availability**: NoSQL databases often provide built-in replication and fault-tolerance mechanisms that ensure data availability even in the face of hardware failures or other system disruptions.

4. **Performance**: NoSQL databases are optimized for high-performance operations, such as read and write operations, by adopting various techniques like in-memory caching, parallel processing, and optimized storage formats.

5. **Support for unstructured, semi-structured, and structured data**: NoSQL databases can handle different types of data, including unstructured data like documents, semi-structured data like JSON, and structured data.

### Types of NoSQL Databases

There are several types of NoSQL databases, each designed to handle specific use cases and data models. The main types are:

1. **Key-value stores**: These databases store data as a collection of key-value pairs. They provide simple and fast operations for retrieving and updating values using a unique key.

2. **Document databases**: Document databases store semi-structured or unstructured data as documents, typically in formats like JSON or XML. They provide flexible schema support, allowing for nested structures and dynamic updates.

3. **Column-family stores**: These databases store data in columns rather than rows, and they allow for the storage and retrieval of data in a flexible and scalable manner.

4. **Graph databases**: Graph databases are designed to store and query highly connected data. They represent entities as nodes and relationships between entities as edges, enabling efficient traversal and analysis of complex relationships.

### Examples and Use Cases

#### Key-value stores

One popular example of a key-value store is Redis. Redis provides fast, in-memory storage with support for data persistence and various data structures like lists, sets, and sorted sets. Here is an example of how Redis can be used in Python:

```python
import redis

# Connect to Redis server
r = redis.Redis(host='localhost', port=6379, db=0)

# Set a key-value pair
r.set('my_key', 'my_value')

# Get the value for a key
value = r.get('my_key')
print(value)
```

#### Document databases

MongoDB is a widely-used document database that stores data in BSON (Binary JSON) format. It provides a rich set of query capabilities and supports flexible schema designs. Here's an example of using MongoDB with Python:

```python
from pymongo import MongoClient

# Connect to MongoDB
client = MongoClient()

# Access a database
db = client['my_database']

# Access a collection (similar to a table in relational databases)
collection = db['my_collection']

# Insert a document
document = {'name': 'John', 'age': 30}
result = collection.insert_one(document)

# Find documents matching a query
query = {'age': {'$gt': 25}}
results = collection.find(query)

# Print the matching documents
for result in results:
    print(result)
```

#### Column-family stores

Apache Cassandra is a widely-used column-family store that provides high scalability and flexibility for handling large-scale datasets. It is designed to support fault-tolerant and highly available distributed databases. Here's an example of using Cassandra with Python:

```python
from cassandra.cluster import Cluster

# Connect to Cassandra cluster
cluster = Cluster(['127.0.0.1'])
session = cluster.connect()

# Create a keyspace
session.execute("CREATE KEYSPACE my_keyspace WITH replication = {'class': 'SimpleStrategy', 'replication_factor': 1};")

# Use the keyspace
session.set_keyspace('my_keyspace')

# Create a table
session.execute("CREATE TABLE my_table (id UUID PRIMARY KEY, name TEXT);")

# Insert data into the table
session.execute("INSERT INTO my_table (id, name) VALUES (uuid(), 'John');")

# Select data from the table
results = session.execute("SELECT * FROM my_table;")
for result in results:
    print(result)
```

#### Graph databases

Neo4j is a popular graph database that provides efficient query and manipulation capabilities for highly interconnected data. It allows for the storage and analysis of relationships and is widely used in domains like social networking, recommendation systems, and fraud detection. Here's an example of using Neo4j with Python:

```python
from neo4j import GraphDatabase

# Connect to Neo4j database
driver = GraphDatabase.driver("bolt://localhost:7687", auth=("neo4j", "password"))

# Create a session
session = driver.session()

# Create a node
session.run("CREATE (p:Person {name: 'John'})")

# Create a relationship between two nodes
session.run("MATCH (p:Person {name: 'John'}) "
            "CREATE (p)-[:FRIEND_OF]->(friend:Person {name: 'Jane'})")

# Query the graph
result = session.run("MATCH (p:Person)-[:FRIEND_OF]->(friend:Person) "
                     "RETURN p.name AS person, friend.name AS friend")
for record in result:
    print(record)
```

## Using MongoDB Offline

You can use the `pymongo` library offline using the `tinymongo` library, by running `pip install tinymongo` to install the library.  On some versions of Python, you'll need to override one of the classes to explicitly use a JSON backend store to write your data locally, but otherwise, the library can be used as a drop-in replacement to a MongoDB cloud instance.

```python
import tinymongo as tm
import tinydb

# per https://github.com/schapman1974/tinymongo/issues/58
class TinyMongoClient(tm.TinyMongoClient):
  @property
  def _storage(self):
      return tinydb.storages.JSONStorage
    
# you can include a folder name or absolute path
# as a parameter if not it will default to "tinydb"
client = TinyMongoClient()

# create your db and collection as before...
```
