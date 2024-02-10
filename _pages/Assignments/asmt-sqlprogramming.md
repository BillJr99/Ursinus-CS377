---
layout: assignment
permalink: /Assignments/SQLProgramming
title: "CS377: Database Design - SQL Programming"


info:
  coursenum: CS377
  points: 100
  goals:
    - To implement a program to create and populate a database using fundamental programming constructs
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
    - rtitle: "The Entity Relational (ER) Model Activity"
      rlink: "../Activities/ERModel"
    - rtitle: "The Structured Query Language (SQL) Activity"
      rlink: "../Activities/SQL"    
      
tags:
  - sql
  - programming
  
---

In this assignment, you will write a program to implement the [insurance database](https://replit.com/@BillJr99/Sql-ERModels) we considered in class.  Specifically, you may have noticed that it was difficult to create a dependent insurance entry into the `DEPENDENTCOVERAGE` table for every dependent of a given employee.  

## Implementing a SQL-based Database Program

Using the [sqlite3](https://docs.python.org/3/library/sqlite3.html) Python library, write a program to create the insurance coverage database schema, and insert records into that schema.  This time, write a function to add an employee's dependents into the database.  Look up the employee's dependents, and in a loop, add a row for each of them into the `DEPENDENTCOVERAGE` table.

## Exporting your Project for Submission

When you're done, write a README for your project, and save all your files, before exporting your project to ZIP.  In your README, answer any bolded questions presented on this page.  