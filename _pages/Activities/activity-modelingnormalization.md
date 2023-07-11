---
layout: activity
permalink: /Activities/Modeling/Normalization
title: "CS377: Database Design - Data Modeling and Normalization"
excerpt: "CS377: Database Design - Data Modeling and Normalization"

info:
  goals: 
    - To model database dependencies using a formal notation
    - To normalize database schemas at varying degrees (first, second, and third normal forms)
    
  notes: "./Normalization/Notes"
    
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

