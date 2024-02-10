---
layout: assignment
permalink: /Labs/DatabaseDesign
title: "CS377: Database Design - Database Design"


info:
  coursenum: CS377
  points: 100
  goals:
    - To design a database that is atomic, consistent, isolated, and durable (ACID)
    - To implement a database system in the SQL language using a programming language and SQL library
  rubric:
    - weight: 30
      description: Algorithm Implementation
      preemerging: The algorithm fails on the test inputs due to major issues, or the program fails to compile and/or run
      beginning: The algorithm fails on the test inputs due to one or more minor issues
      progressing: The algorithm is implemented to solve the problem correctly according to given test inputs, but includes only a single class, or would fail if executed in a general case due to a minor issue or omission in the algorithm design or implementation
      proficient: A reasonable algorithm with multiple classes is implemented to solve the problem which correctly solves the problem according to the given test inputs, and would be reasonably expected to solve the problem in the general case
    - weight: 40
      description: Database Modeling and Design
      preemerging: The database design is not conducive to implementing the system proposed or intended
      beginning: The database design is not appropriate or well justified to the application pursued, but a functional solution is provided
      progressing: The database design is slightly denormalized, but could be improved easily, or the document structure of a NoSQL approach is slightly disorganized in ways that can be easily improved.
      proficient: The database design is appropriately chosen and justified, with normalization and/or transactional models utilized to create a well-organized database system.
    - weight: 20
      description: Code Quality and Documentation
      preemerging: Code commenting and structure are absent, or code structure departs significantly from best practice, and/or the code departs significantly from the style guide
      beginning: Code commenting and structure is limited in ways that reduce the readability of the program, and/or there are minor departures from the style guide
      progressing: Code documentation is present that re-states the explicit code definitions, and/or code is written that mostly adheres to the style guide
      proficient: Code is documented at non-trivial points in a manner that enhances the readability of the program, and code is written according to the style guide
    - weight: 10
      description: Writeup and Submission
      preemerging: An incomplete submission is provided
      beginning: The program is submitted, but not according to the directions in one or more ways (for example, because it is lacking a readme writeup)
      progressing: The program is submitted according to the directions with a minor omission or correction needed
      proficient: The program is submitted according to the directions, including a readme writeup describing the solution
  readings:
    - rtitle: "Database Integrity Activity"
      rlink: "../Activities/DataIntegrity" 
    - rtitle: "Structured Query Language (SQL) Activity"
      rlink: "../Activities/SQL"    
    - rtitle: "The Relational Database Model Activity"
      rlink: "../Activities/RelationalModel"
      
tags:
  - modeling
  - programming
  
---

In this lab, you will create (or use an existing design of your own creation) a database schema, and implement that design using a programming language and database library.  Your schema should utilize primary and foreign keys, and use Python and a SQL library to construct, populate, and query that database.

Begin by sketching an ER diagram of your proposed database tables.  You should have at least three tables, each with primary and foreign key dependencies.  You should provide at least one aggregate query (*i.e.,* an average), and mechanisms to insert, update, delete, and query data across multiple tables.  When a deletion is made to a dependent table (which should occur at least once), an immediate deletion/update should be made on the parent table to ensure referential integrity.

The application domain is your choice, so feel free to be creative here!

## Exporting your Project for Submission

When you're done, write a README for your project, and save all your files, before exporting your project to ZIP.  In your README, answer any bolded questions presented on this page.  