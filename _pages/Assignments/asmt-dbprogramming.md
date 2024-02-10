---
layout: assignment
permalink: /Assignments/DatabaseProgramming
title: "CS377: Database Design - Database Programming"


info:
  coursenum: CS377
  points: 100
  goals:
    - To manipulate databases through a programmatic interface
    - To utilize SQL libraries in a programming language
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
    - rtitle: "Relational Database Model Activity"
      rlink: "../Activities/RelationalModel" 
    - rlink: https://pypi.org/project/PyMySQL/
      rtitle: PyMySQL Python Library
    - rlink: https://docs.python.org/3/library/sqlite3.html
      rtitle: Sqlite3 Python Library
    - rlink: https://www.tutorialspoint.com/postgresql/postgresql_python.htm
      rtitle: PostgreSQL Python Library
      
tags:
  - tables
  - programming
  
---

In this assignment, you will connect to a web or local database engine and write a program to execute SQL commands on that engine.

### Connecting to the Database

You can either [install the MySQL database engine](https://dev.mysql.com/doc/mysql-installation-excerpt/5.7/en/) locally, [use a web-based database engine like Fauna](https://fauna.com/), or [connect to a database on a web-based data repository such as bit.io](https://bit.io/).  Each option will provide you with connection details for the database, including a username, password, hostname, port number, and possibly a connection string that includes all of this information in a single URI.  You may also use sqlite using the [`sqlite3` library](https://docs.python.org/3/library/sqlite3.html)

Import the appropriate library for the database engine you are using (for example, [bit.io](https://bit.io) uses PostgreSQL), and write a program that implements a database schema of your choosing.  You can be creative here!  Your schema should have at least three tables with relationships to other tables via foreign keys, and at least one of those relationships should be 1:many.  Draw you schema before implementing it.

Your implementation should use a class structure to model each table, and that class should include a method that returns a string with SQL code including the field values you wish to insert into your database.  

Execute each statement to create and insert records into your database.  I recommend reading the data to insert from a text file so that you can test repeatedly very quickly!

Finally, include at least three aggregated queries (mathematical aggregations, joins, *etc*) across your tables.  Use a loop to iterate over the result set and print the results to the screen in a meaningful way.

## Exporting your Project for Submission

When you're done, write a README for your project, and save all your files, before exporting your project to ZIP.  In your README, answer any bolded questions presented on this page.  