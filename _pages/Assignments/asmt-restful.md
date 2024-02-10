---
layout: assignment
permalink: /Assignments/RESTful
title: "CS377: Database Design - RESTful Web Services with Database Backends"


info:
  coursenum: CS377
  points: 100
  goals:
    - To implement a RESTful web service interface to expose database functionality to users, in both the relational and NoSQL models
  rubric:
    - weight: 40
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
    - weight: 20
      description: Code Quality and Documentation
      preemerging: Code commenting and structure are absent, or code structure departs significantly from best practice, and/or the code departs significantly from the style guide
      beginning: Code commenting and structure is limited in ways that reduce the readability of the program, and/or there are minor departures from the style guide
      progressing: Code documentation is present that re-states the explicit code definitions, and/or code is written that mostly adheres to the style guide
      proficient: Code is documented at non-trivial points in a manner that enhances the readability of the program, and code is written according to the style guide
    - weight: 10
      description: Writeup and Submission
      preemerging: An incomplete submission is provided
      beginning: The program is submitted, but not according to the directions in one or more ways (for example, because it is lacking a readme writeup or missing answers to written questions)
      progressing: The program is submitted according to the directions with a minor omission or correction needed, including a readme writeup describing the solution and answering nearly all questions posed in the instructions
      proficient: The program is submitted according to the directions, including a readme writeup describing the solution and answering all questions posed in the instructions
  readings:
    - rtitle: "Web Services Activity"
      rlink: "../Activities/WebServices"
      
tags:
  - sql
  - nosql
  - restful
  - programming
  
---

In this assignment, you will create a database design in a relational model, and in a NoSQL model (they can be the same design, implemented in both models, or two different designs as appropriate to each model).  Implement a RESTful web service interface, tested with curl or a client program, that implements the database and creates, reads, updates, and deletes data within each database.

## Exporting your Project for Submission

When you're done, write a README for your project, and save all your files, before exporting your project to ZIP.  In your README, answer any bolded questions presented on this page.  