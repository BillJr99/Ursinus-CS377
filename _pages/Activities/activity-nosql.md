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
        <img src="https://docs.mongodb.com/manual/_images/crud-annotated-collection.bakedsvg.svg" alt="MongoDB Collections from mongodb.com" />
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


