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

