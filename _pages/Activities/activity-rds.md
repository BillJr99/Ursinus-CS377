---
layout: activity
permalink: /Activities/RDS
title: "CS173: Intro to Computer Science - Text and File Management"
excerpt: "CS173: Intro to Computer Science - Text and File Management"

info:
  goals: 
    - To define the various components of a typical Relational Database System (RDS)
    - To differentiate between the benefits and costs of various indexing structures to improve search performance
    - To select between memory and disk structures for backing a database
    
  models:
    - model: |
        <a title="Scifipete, CC BY-SA 3.0 &lt;https://creativecommons.org/licenses/by-sa/3.0&gt;, via Wikimedia Commons" href="https://commons.wikimedia.org/wiki/File:RDBMS_structure.png"><img width="512" alt="RDBMS structure" src="https://upload.wikimedia.org/wikipedia/commons/5/57/RDBMS_structure.png"></a>
      title: Structure of a Relational Database Management (RDBMS) System
      questions:
        - "Some items are stored in memory as well as on disk; how is this reconciled?"
        - "What would happen to the in-memory data if the database system was shut down prior to writing to disk?  How might this data be recovered?"
    - model: |
        <img src="https://opentextbc.ca/dbdesign01/wp-content/uploads/sites/11/2014/08/MemFormAug2014.jpg" alt="An example database from Database Design 2nd Ed by Watt and Eng">
        <br>
        <a title="Jorge Stolfi, Public domain, via Wikimedia Commons" href="https://commons.wikimedia.org/wiki/File:Hash_table_4_1_1_0_0_1_0_LL.svg"><img width="256" alt="Hash table 4 1 1 0 0 1 0 LL" src="https://upload.wikimedia.org/wikipedia/commons/thumb/5/58/Hash_table_4_1_1_0_0_1_0_LL.svg/256px-Hash_table_4_1_1_0_0_1_0_LL.svg.png"></a>
      title: Indexing
      questions:
        - "What are some strategies you might use to allow a person to look up the location of a record in a database more quickly than by linear search?"
        - "Can you have more than one index on the same table?  What might this mean?"
        - "Given a person's name, how might you use a hash table to quickly identify the row that contains the corresponding record?"
        - "How might you change the hash if you wanted to search by date-of-birth rather than by name?"
        - "If the hash table isn't big enough to hold every possible record hash, what could happen?  What would the drawback be?"
        - "Given that some indices enable <code>O(1)</code> constant time lookups, while others are <code>O(log n)</code> logarithmic time lookup with respect to the number of records <code>n</code>, what might you speculate is the underlying data structure used to create an index?"        
        
tags:
  - rds
  - indexing  
---

