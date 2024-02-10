---
layout: assignment
permalink: /Labs/Schemas
title: "CS377: Database Design - Schemas"


info:
  coursenum: CS377
  points: 100
  goals:
    - To create a database schema that handles relational references
  rubric:
    - weight: 60
      description: Algorithm Implementation
      preemerging: The algorithm fails on the test inputs due to major issues, or the program fails to compile and/or run
      beginning: The algorithm fails on the test inputs due to one or more minor issues
      progressing: The algorithm is implemented to solve the problem correctly according to given test inputs, but would fail if executed in a general case due to a minor issue or omission in the algorithm design or implementation
      proficient: A reasonable algorithm is implemented to solve the problem which correctly solves the problem according to the given test inputs, and would be reasonably expected to solve the problem in the general case
    - weight: 30
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
    - rtitle: "Data Modeling and Schemas Activity"
      rlink: "../Activities/Modeling/Schemas" 
      
tags:
  - schemas
  - programming
  
---

In this lab, you will create a database schema design including hierarchical relationships.  

Consider the problem of planning your graduation requirements.  Certain courses meet various requirements within your major, both for the major itself and for the college.  You might be required to take a certain number of those courses, but it may also be the case that one course satisfies multiple requirements simultaneously.  

Design a database schema including tables and keys that helps to satisfy these requirements.  You may find it helpful to create a table just for handling requirements, mapping a single course ID to a single requirement ID, but allowing several entries for the same course ID (this implements the 1:many relationship of a hierarchical model!).

### Implementing the Database in SQL
Once you have created your design, create the tables using SQL `CREATE TABLE` statements.  Insert data into each of the tables with `INSERT INTO` commands.

## Exporting your Project for Submission

When you're done, write a README for your project, and save all your files, before exporting your project to ZIP.  In your README, answer any bolded questions presented on this page.  