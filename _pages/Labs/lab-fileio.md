---
layout: assignment
permalink: /Labs/FileIO
title: "CS377: Database Design - File I/O"
excerpt: "CS377: Database Design - File I/O"

info:
  coursenum: CS377
  points: 100
  goals:
    - To use file I/O to read and process records in a flat file format
  rubric:
    - weight: 30
      description: File Format Writer Implementation
      preemerging: The algorithm fails on the test inputs due to major issues, or the program fails to compile and/or run
      beginning: The algorithm fails on the test inputs due to one or more minor issues
      progressing: The algorithm is implemented to solve the problem correctly according to given test inputs, but would fail if executed in a general case due to a minor issue or omission in the algorithm design or implementation
      proficient: A reasonable algorithm is implemented to solve the problem which correctly solves the problem according to the given test inputs, and would be reasonably expected to solve the problem in the general case
    - weight: 30
      description: Partner File Reader Implementation
      preemerging: The algorithm fails on the test inputs due to major issues, or the program fails to compile and/or run
      beginning: The algorithm fails on the test inputs due to one or more minor issues
      progressing: The algorithm is implemented to solve the problem correctly according to given test inputs, but would fail if executed in a general case due to a minor issue or omission in the algorithm design or implementation
      proficient: A reasonable algorithm is implemented to solve the problem which correctly solves the problem according to the given test inputs, and would be reasonably expected to solve the problem in the general case      
    - weight: 30
      description: Code Quality and Documentation
      preemerging: Code commenting and structure are absent, or code structure departs significantly from best practice, and/or the code departs significantly from the style guide
      beginning: Code commenting and structure is limited in ways that reduce the readability of the program, and/or there are minor departures from the style guide
      progressing: Thorough documentation is given on the file format chosen that is suitable for exchange with a partner for implementation
      proficient: Thorough documentation is given on the file format chosen that is suitable for exchange with a partner for implementation; additionally, a meaningful reflection is given about the experience writing a file reader that conforms to someone else's file specifications
    - weight: 10
      description: Writeup and Submission
      preemerging: An incomplete submission is provided
      beginning: The program is submitted, but not according to the directions in one or more ways (for example, because it is lacking a readme writeup or missing answers to written questions)
      progressing: The program is submitted according to the directions with a minor omission or correction needed, including a readme writeup describing the solution and answering nearly all questions posed in the instructions
      proficient: The program is submitted according to the directions, including a readme writeup describing the solution and answering all questions posed in the instructions
  readings:
    - rtitle: "Text and File Management Activity"
      rlink: "../Activities/TextAndFileManagement"    
      
tags:
  - introduction
  
---

In this lab, you will create and document your own file format for a family tree. You will also write a program to input information and output a family tree file in your format. You will then exchange file formats with a partner, who will write a program to read a file in your format and print the family tree to the screen and generate a dotty graph of the family tree.

## File Format Creation

Invent your own file format for a family tree. Be careful to avoid duplicating data within the file. Each person should have a unique identification record number that is referred to elsewhere in the file. The family tree file should include people (with their name, date of birth, and any other information you'd like to include), as well as relationships between family members (parent, child, sibling, *etc.*).

## File Format Documentation

Document your file format thoroughly. This should include a detailed explanation of how the file format works, what each part of the file represents, and how to read and write to the file.

## File Writer

Write a program that allows the user to enter information at the console and output a family tree file in your format. The program should be able to take input from the user and create a file in your format that represents a family tree.

## Exchanging File Formats and Creating a File Reader

Exchange your file format documentation (but not your code) with a partner. Your partner will write a program to read a file in your format.

Each partner will write a program that can read a file in the other partner's format, print the family tree to the screen, and generate a [dotty graph](https://graphviz.org/doc/info/lang.html) of the family tree.

### Dotty Graph Example

Here is an example of a directed graph in the DOT language.  The node names are given in quotes, with their label inside the properties brackets.  Then, the edges are defined by specifying two node names with a textual arrow `->` between them.  Edges can be labeled as well (for example, with the type of relationship between the two people).

```
digraph family_tree {
    // Define nodes
    "John" [label="John\n(1970- )"]
    "Jane" [label="Jane\n(1972- )"]
    "Alice" [label="Alice\n(1995- )"]
    "Bob" [label="Bob\n(1998- )"]

    // Define relationships
    "John" -> "Alice" [label="parent"]
    "John" -> "Bob" [label="parent"]
    "Jane" -> "Alice" [label="parent"]
    "Jane" -> "Bob" [label="parent"]
}
```

This graph can be converted to an image using the following command, assuming you have dotty/graphviz installed: `dot -Tpng filename.dot -o outfile.png`

## Reflection

Reflect in your README about how easy or difficult it was to follow the file format documentation, and why. Consider what made the documentation easy or difficult to understand, and how the documentation could be improved.  Specifically, answer the following questions:

1. Discuss with your partner ways that you could improve your own file format.  Document those suggestions here.
2. Why might it be difficult to encode relationships using a text-based format like CSV or json?  It's not impossible - you can do it, but what makes it difficult for you to do?
3. What are some ways you might use data structures to improve your program's performance to search and find relationships within your file format?  You don't have to make these changes, just discuss how you might use them, and how you might encode them into your file.

## Exporting your Project for Submission

When you're done, write a README for your project, and save all your files, before exporting your project to ZIP.  In your README, answer any bolded questions presented on this page.  