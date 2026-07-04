---
layout: assignment
permalink: /Assignments/Join
title: "CS377: Database Design - The SQL Join"


info:
  coursenum: CS377
  points: 100
  goals:
    - To read and interpret relational models for database systems according to specifications
  readings:
    - rtitle: "SQL Join Activity"
      rlink: "../Activities/Modeling/Join" 
      
tags:
  - joins
  - modeling
  
---

## Purpose

Joins are the mechanism that makes a *normalized* database usable: once we split data into multiple tables to eliminate redundancy and anomalies, joins are how we reassemble it to answer questions.  Practicing joins on paper — predicting exactly which rows appear in the result before running anything — is how database professionals debug queries that return too many rows, too few rows, or unexpected `NULL`s.  This assignment builds that prediction skill.

## Task

Complete Exercises 1 and 2 in Chapter 10 of the Database Design textbook.

For each exercise:

1. **Read the tables first.**  Identify the join column(s) shared between the tables, and note any rows that will *not* find a match on the other side — these unmatched rows are what distinguish the join types.
2. **Write the SQL statement** for the requested join, using explicit `INNER JOIN` / `LEFT JOIN` / `RIGHT JOIN` / `FULL OUTER JOIN ... ON ...` syntax rather than comma-separated tables.
3. **Show the result table** row by row, including `NULL` values in unmatched columns where an outer join preserves a row.
4. **Explain in one or two sentences** why each unmatched row was kept or dropped for that join type.

If you are unsure how to trace a join by hand, work through the step-by-step walkthrough in the [SQL Join Activity](../Activities/Modeling/Join) first — it traces an inner, left, right, and full outer join on the same pair of small tables.

**A common pitfall:** rows with `NULL` in the join column match *nothing* — not even other `NULL`s.  Watch for these when deciding which rows pair up.

## Criteria

Your submission is complete when you can check off each of the following:

- [ ] Each join is written in explicit `JOIN ... ON ...` syntax and names the correct join type for the question asked.
- [ ] Each result table contains exactly the rows the join produces — no missing matches, no invented rows.
- [ ] Unmatched rows preserved by outer joins show `NULL` in the columns from the other table.
- [ ] For every row that appears in one join type's result but not another's, your explanation identifies which side of the join it came from and why it was kept or dropped.
- [ ] Your README answers all bolded questions on this page.

## Exporting your Project for Submission

When you're done, write a README for your project, and save all your files, before exporting your project to ZIP.  In your README, answer any bolded questions presented on this page.  