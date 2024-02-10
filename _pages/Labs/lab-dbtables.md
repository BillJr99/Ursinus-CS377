---
layout: assignment
permalink: /Labs/DatabaseTables
title: "CS377: Database Design - Database Tables"


info:
  coursenum: CS377
  points: 100
  goals:
    - To design referential database tables, and to work with them in the SQL language using Sqlite
  rubric:
    - weight: 60
      description: Algorithm Implementation
      preemerging: The algorithm fails on the test inputs due to major issues, or the program fails to compile and/or run
      beginning: The algorithm fails on the test inputs due to one or more minor issues
      progressing: The algorithm is implemented to solve the problem correctly according to given test inputs, but would fail if executed in a general case due to a minor issue or omission in the algorithm design or implementation
      proficient: A reasonable algorithm is implemented to solve the problem which correctly solves the problem according to the given test inputs, and would be reasonably expected to solve the problem in the general case
    - weight: 30
      description: Database Modeling and Design
      preemerging: The database design is not conducive to implementing the system proposed or intended
      beginning: The database design is not appropriate or well justified to the application pursued, but a functional solution is provided
      progressing: The database design is slightly denormalized, but could be improved easily, or the document structure of a NoSQL approach is slightly disorganized in ways that can be easily improved.
      proficient: The database design is appropriately chosen and justified, with normalization and/or transactional models utilized to create a well-organized database system.
    - weight: 10
      description: Writeup and Submission
      preemerging: An incomplete submission is provided
      beginning: The program is submitted, but not according to the directions in one or more ways (for example, because it is lacking a readme writeup or missing answers to written questions)
      progressing: The program is submitted according to the directions with a minor omission or correction needed, including a readme writeup describing the solution and answering nearly all questions posed in the instructions
      proficient: The program is submitted according to the directions, including a readme writeup describing the solution and answering all questions posed in the instructions
  readings:
    - rtitle: "Database Table Aggregation Activity"
      rlink: "../Activities/RDS/Aggregating" 
    - rtitle: "File I/O Activity"
      rlink: "../Activities/FileIO"    
    - rtitle: "Database Introduction"
      rlink: "https://comptoolsres.github.io/Database_Introduction.html"
tags:
  - tables
  
---

In this lab, you will diagram a table structure using primary and foreign keys, and use Sqlite to construct, populate, and query that database.

Begin by sketching an ER diagram of your proposed database tables.  You should have at least three tables, each with primary and foreign key dependencies.  You should provide at least one aggregate query (*i.e.,* an average), and mechanisms to insert, update, delete, and query data across multiple tables.  When a deletion is made to a dependent table (which should occur at least once), an immediate deletion/update should be made on the parent table to ensure referential integrity.

The application domain is your choice, so feel free to be creative here!

## Exporting your Project for Submission

When you're done, write a README for your project, and save all your files, before exporting your project to ZIP.  In your README, answer any bolded questions presented on this page.  