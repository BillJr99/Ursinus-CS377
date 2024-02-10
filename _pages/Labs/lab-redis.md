---
layout: assignment
permalink: /Labs/Redis
title: "CS377: Database Design - Graph Databases with Redis"


info:
  coursenum: CS377
  points: 100
  goals:
    - To create a graph database schema and implementation with an appropriate application domain
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
    - rtitle: "NoSQL Modeling Activity"
      rlink: "../Activities/NoSQL/DataModels" 
      
tags:
  - nosql
  - graph
  - programming
  
---

In this lab, you will create a graph database schema design including graph-based relationships.  

Using [Redis](https://redis.com/), create a graph database and connect to it from a Python program using the [redis-py](https://redis-py.readthedocs.io/en/stable/) library.  When you create your database, enable the RedisGraph module!

Read a GEDCOM file, and create a node for each person that you identify.  For each relationship, create an edge.  Write a query to output a particular set of relationships.  You can choose the relationship, but it should include at least two links.  For example, aunts and uncles, grandparents, or cousins, as opposed to parents or siblings.

### The GEDCOM File Format and Specification

The [FamilySearch GEDCOM Specification](https://gedcom.io/specifications/FamilySearchGEDCOMv7.html) was developed by the Family History Department of The Church of Jesus Christ of Latter-day Saints, and released under the [Apache 2.0](http://www.apache.org/licenses/LICENSE-2.0) license.

#### Reading the Records File

The GEDCOM file format uses a line-based hierarchical structure to represent individuals and relationships.  Each line has roughly the same format, with each field separated by spaces:

```
NUM TYPE DATA
```

For example:

```
0 @I1@ INDI
1 NAME Kelly /Lee/
2 SURN Lee
2 GIVN Kelly
1 SEX F
1 BIRT
2 DATE 1 Jan 1990
2 PLAC Collegeville, Pennsylvania, United States of America
1 FAMC @F1@
0 @I2@ INDI
1 NAME Chris /Lee/
2 SURN Lee
2 GIVN Chris
1 SEX M
1 FAMC @F1@
0 @F1@ FAM
1 WIFE @I1@
1 CHIL @I2@
```

In this example, Kelly Lee has one child named Chris.  On each line, the number represents the level in the hierarchy; higher numbers represent data within the umbrella of the higher number that came above.  You might think of this example according to that hierarchy:

- 0 @I1@ INDI
  - 1 NAME Kelly /Lee/
    - 2 SURN Lee
    - 2 GIVN Kelly
  - 1 SEX F
  - 1 BIRT
    - 2 DATE 1 Jan 1990
    - 2 PLAC Collegeville, Pennsylvania, United States of America
  - 1 FAMC @F1@
- 0 @I2@ INDI
  - 1 NAME Chris /Lee/
    - 2 SURN Lee
    - 2 GIVN Chris
  - 1 SEX M
  - 1 FAMC @F1@
- 0 @F1@ FAM
  - 1 WIFE @I1@
  - 1 CHIL @I2@
  
The first line (`0 @I1@ INDI`) specifies that an individual is being defined.  The `1 NAME Kelly /Lee/` line indicates that the person's name is Kelly Lee (the slashes indicate the person's surname, as opposed to their given name; keep in mind that this is not always the person's "last name").  Specifically, Kelly Lee is the name of the person referred to by `@I1@`, because it appears below that line in the hierarchy.  In general, if you read the file one-line-at-a-time, each time you encounter a `0` line, you're defining a new person or family structure.  You can read the first two tokens of each line, after tokenizing by space, to determine the hierarchy number and record type/identifier.  The rest of the line is the data associated with the record, which you can de-tokenize (or append, or extract from the text of the line) and store in a variable.

Example files can be found on the [GEDCOM website](https://www.gedcom.org/samples.html).  The GEDCOM file format specification is large and detailed; it is not necessary to process every type of relationship.  At a minimum, you should extract the names of individuals and their familial relationships (*i.e.*, spouse, children, *etc*).  You are welcome, and encouraged, to extract additional information as your creativity allows!

## Exporting your Project for Submission

When you're done, write a README for your project, and save all your files, before exporting your project to ZIP.  In your README, answer any bolded questions presented on this page.  
