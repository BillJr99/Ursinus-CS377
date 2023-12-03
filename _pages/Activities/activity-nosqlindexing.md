---
layout: activity
permalink: /Activities/NoSQL/Indexing
title: "CS377: Database Design - Indexing a Denormalized NoSQL Datastore"
excerpt: "CS377: Database Design - Indexing a Denormalized NoSQL Datastore"

info:
  goals: 
    - To create an index in a NoSQL database
    
  models:
    - model: |
        <script type="syntaxhighlighter" class="brush: python"><![CDATA[    
        # TODO: obtain the collection as usual
        # ... in a variable called collection
        
        collection.ensureIndex({"airport": 1})
        
        # you can have more than one index 
        # ... depending on the values you intend to query together!
        collection.ensureIndex({"student": 1, "grade": -1})
        ]]></script>
      title: Indexes in NoSQL databases
      questions:
        - "Look up which sort order is specified by <code>1</code> and which by <code>-1</code>."
        - "Insert many records with a loop into a MongoDB database, and query it with and without an index.  What speedup do you observe for varying numbers of <code>N</code> documents in your collection?  You can use the <code>.explain()</code> method on the cursor returned by your call to <code>find()</code> to obtain information about the time required to execute the query, as well as whether an index (<code>BtreeCursor</code>) was used or not (<code>BasicCursor</code>)."

  additional_reading:
    - link: https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/GSI.html
      title: Global Secondary Indices in DynamoDB
    - link: https://shopify.engineering/read-consistency-database-replicas
      title: Database Consistency
      
tags:
  - nosql
  - normalization
  
---

## Indexing a Denormalized NoSQL Datastore
In this report, we will explore the concept of indexing a denormalized NoSQL datastore. Denormalization is a technique used to optimize data retrieval in NoSQL databases by reducing joins and improving query performance. However, without proper indexing, denormalized data can result in slower queries and increased storage requirements. Indexing plays a crucial role in optimizing query performance in denormalized NoSQL datastores.

### Indexing in NoSQL Datastores
NoSQL databases are designed for high scalability and performance, and they employ various indexing techniques to improve query efficiency. In a denormalized NoSQL datastore, where data is intentionally duplicated to avoid joins, indexing becomes even more important to ensure fast query execution.

#### Types of Indexes
There are several types of indexes commonly used in NoSQL databases, including:

1. **B-tree indexes**: B-tree indexes are widely used in NoSQL databases due to their efficient performance characteristics. They allow efficient range queries and support sorting. B-tree indexes can be used for both primary and secondary key-based lookups.

2. **Hash indexes**: Hash indexes use a hashing function to map keys to their corresponding values. They are fast for exact match queries but do not support range queries or sorting.

3. **Bitmap indexes**: Bitmap indexes are well-suited for databases with low cardinality attributes. They maintain a bitmap for each possible attribute value, allowing for efficient filtering and aggregations.

#### Indexing Strategies for Denormalized Datastores
In denormalized NoSQL datastores, where data duplication is intentionally performed, indexes should be carefully chosen and created to optimize query performance. Here are some indexing strategies commonly used in denormalized datastores:

1. **Composite indexes**: Composite indexes combine multiple attributes into a single index, enabling efficient querying on multiple attributes simultaneously. This can significantly improve performance in denormalized datastores.

2. **Covering indexes**: Covering indexes store all the columns required by a query in the index itself, eliminating the need to access the actual data rows. This helps reduce disk I/O and improves query performance.

3. **Partial indexes**: Partial indexes index a subset of the data to reduce the size of the index and improve query performance. This can be useful when working with large denormalized datastores.

## Python Examples

### Creating an Index in MongoDB
```python
import pymongo

# Connect to MongoDB
client = pymongo.MongoClient("mongodb://localhost:27017")

# Get reference to database and collection
db = client["mydatabase"]
collection = db["mycollection"]

# Create index on "name" attribute
collection.create_index("name")

# Create compound index on "name" and "age" attributes
collection.create_index([("name", pymongo.ASCENDING), ("age", pymongo.ASCENDING)])
```

### Creating an Index in Apache Cassandra
```python
from cassandra.cluster import Cluster
from cassandra.query import SimpleStatement

# Connect to Cassandra
cluster = Cluster(['127.0.0.1'])
session = cluster.connect()

# Create index on "name" attribute
create_index_query = "CREATE INDEX ON mykeyspace.mytable (name)"
session.execute(create_index_query)

# Create compound index on "name" and "age" attributes
create_compound_index_query = "CREATE INDEX ON mykeyspace.mytable (name, age)"
session.execute(create_compound_index_query)
```
