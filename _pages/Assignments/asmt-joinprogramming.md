---
layout: assignment
permalink: /Assignments/JoinProgramming
title: "CS377: Database Design - SQL Join Programming with the Lahman Baseball Database"
excerpt: "CS377: Database Design - SQL Join Programming with the Lahman Baseball Database"

info:
  coursenum: CS377
  points: 100
  goals:
    - To implement join statements to query an existing nontrivial database
    - To read and interpret relational models for database systems according to specifications
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
    - rtitle: "SQL Join Activity"
      rlink: "../Activities/Modeling/Join" 
      
tags:
  - sql
  - programming
  
---

In this assignment, you will query an existing large database to answer meaningful questions.

## Written Assignment

Complete Exercise 8 in Chapter 12 on Database Normalization of the Database Design textbook.

## Programming Assignment

Write a program that uses the [`sqlite3` database library](https://docs.python.org/3/library/sqlite3.html) to connect to [this database](
https://github.com/WebucatorTraining/lahman-baseball-mysql/raw/master/lahmansbaseballdb.sqlite) and to execute your queries.

### About the Dataset
The [Baseball Archive](http://www.seanlahman.com/baseball-archive/statistics/) database is maintained by Sean Lahman \[[^1]\], and contains a number of statistics about players and teams up to and including the current baseball season.  We will use the database for the 2019 season.  It is not important that you are familiar with the game of baseball to query this data; rather, that you use the links shown in the database schema to connect relevant tables together.  This is often helpful when we are called upon to answer questions about data with queries in application domains about which we are less familiar!  The schema for this database is provided below:

![Lahman Baseball Database Schema](../images/asmt-joinprogramming/lahmansbaseballdb.sqlite.png)

### What to Do
Answer the following questions using the dataset (feel free to write these queries for any year if you'd like to explore!):

1. How many wins did the Philadelphia Phillies have in 2019?  You will use the `teams` table to find this.
2. Which team had the most hits in 2019?  The `teams` table has this as well.
3. Who was the highest paid player in 2016?  To find this, you will connect the `salaries` table with the `people` table .  Recall that `MAX` is an aggregating function that can be used in a `SELECT` statement.
4. What players played in the all-star game in 2019?  You will connect the `allstarfull` table with the `people` table to find this.
5. For each player in the major leagues in 2019 that also played in college, what is the name of the school(s) they attended?  You will connect the `people`, `appearances`, `collegeplaying`, and `schools` table to find this.
6. Make up any question you'd like and answer it.  If you're not a baseball fan, you can keep this relatively simple, but a little data exploration can be fun and we will compare our questions and queries (anonymously if you prefer!) in class.

## Exporting your Project for Submission

When you're done, write a README for your project, and save all your files, before exporting your project to ZIP.  In your README, answer any bolded questions presented on this page.  

[^1]: The database is copyright 1996-2021 by Sean Lahman and licensed under a Creative Commons Attribution-ShareAlike 3.0 Unported License.  For details see: [http://creativecommons.org/licenses/by-sa/3.0/](http://creativecommons.org/licenses/by-sa/3.0/)
