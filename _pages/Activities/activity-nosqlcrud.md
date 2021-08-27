---
layout: activity
permalink: /Activities/NoSQL/CRUD
title: "CS377: Database Design - Create, Read, Update, and Delete (CRUD) with NoSQL"
excerpt: "CS377: Database Design - Create, Read, Update, and Delete (CRUD) with NoSQL"

info:
  goals: 
    - "To explore the core operations on an unstructured data store: create, update, read, and delete (CRUD)"
    - "To be able to implement each of the CRUD operations on a NoSQL database in Python"
  additional_reading:
    - title: "PyMongo Tutorial"
      link: "https://pymongo.readthedocs.io/en/stable/tutorial.html"
    
  models:
    - model: |
        <script type="syntaxhighlighter" class="brush: python"><![CDATA[    
        # TODO: create the MongoDB pymongo client 
        # ... with a variable called client
        
        # give your database a name
        db = client.somedb
        
        # give your collection a name
        collection = db.somecollection
        
        doc = { "key1": "val1", "key2": 42 }
        id = collection.insert_one(doc).inserted_id
        
        docs = [{ "key1": "val1", "key2": 42 }, { "key1": "val1", "key2": 1 }]
        ids = collection.insert_many(docs).inserted_ids # ids is an array
        ]]></script>
      title: Create
      questions:
        - "Investigate how to create an index in a MongoDB collection using PyMongo."
        - "What kind of data do you think is best suited for a relational database, and what kind might be better suited for this non-relational approach?  As a group, write down three examples of each.  Let's compare with the class and see who has the most unique ideas!"
    - model: |
        <script type="syntaxhighlighter" class="brush: python"><![CDATA[    
        # TODO: retrieve your collection in a variable called collection
        
        # returns only one result
        doc = collection.find_one({"key1": "val1"})
        
        # if the id is known:
        doc = collection.find_one({"_id": id})
        
        # for multiple results
        cursor = collection.find({"key1": "val1"}).sort("key2": -1)
        for doc in cursor:
            print(doc['key2'])
                
        docs = collection.find({"val1": {$in: [0, 100]}})
        docs = collection.find({"val1": {$gt: -1, $lt: 101}})
        ]]></script>
      title: Read
      embed: <iframe height="400px" width="100%" src="https://repl.it/@BillJr99/PythonMongoDBExample?lite=true" scrolling="no" frameborder="no" allowtransparency="true" allowfullscreen="true" sandbox="allow-forms allow-pointer-lock allow-popups allow-same-origin allow-scripts allow-modals"></iframe>    
      questions:
        - "Modify the above program to insert records into a datastore and query them, iterating over the results."
        - "Which statements search for items according to their value?"
        - "How is the sorted cursor sorted?"
        - "Investigate how to search for records that contain a key called <code>val3</code> in your collection.  <strong>Hint: consider the <code>$exists</code> clause.</strong>"
        - "By default, multiple items in a <code>find</code> are combined using a boolean <code>AND</code> operation.  Investigate how to search by combining search terms with an <code>OR</code>.  <strong>Hint: Consider the <code>$or</code> clause.</strong>"
    - model: |
        <script type="syntaxhighlighter" class="brush: python"><![CDATA[        
        # TODO: retrieve your collection in a variable called collection
        
        collection.update({"key1": "val1"}, {$set: {"val2": 0}})
        collection.update({"key1": "val1"}, {$unset: {"val2": ''}}, {multi: true})
        collection.update({"key1": "val1"}, {$push: {"val3": 100}})
        collection.update({"key1": "val1"}, {$rename: {"val3": "value"}})
        
        collection.findAndModify({query: {"val1" {$gt: 10}}, update: {$inc, {"val1": 1}}})
        ]]></script>
      title: Update
      questions:
        - "What do you think <code>$set</code> and <code>$unset</code> do?"
        - "What would the <code>update</code> without the <code>multi</code> modifier do?"
        - "What does <code>$push</code> and <code>$rename</code> do?"
        - "What does the <code>findAndModify</code> statement do in this example?"
        - "What do you think would happen if the <code>query</code> parameter is set to <code>{}</code> in the <code>find</code> and <code>update</code> statements above?"
    - model: |
        <script type="syntaxhighlighter" class="brush: python"><![CDATA[        
        # TODO: retrieve your collection in a variable called collection
        
        collections.remove({"key1": "val1"})
        ]]></script>
      title: Delete
      questions:
        - "What is an alternative to removing items from a datastore so that you never actually delete anything, while omitting &quot;removed&quot; records from your queries?"
        - "Do you think the <code>query</code> parameter works with <code>remove</code>?  Try it out, and remove all items from the collection whose <code>val1</code> value is greater than 42!"
    - model: |
        <script src="https://gist.github.com/javierarilos/015e2ce27cecdea63564.js"></script>
        <br>
        <script src="https://gist.github.com/michaeltreat/d3bdc989b54cff969df86484e091fd0c.js"></script>
        <br>
        <script src="https://gist.github.com/leommoore/6751647.js"></script>
      title: Putting it All Together with Examples      
        
tags:
  - nosql  
---

