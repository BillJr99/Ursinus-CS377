---
layout: exercise_sql
permalink: /Modules/Warmup/Exercise
title: "CS377: Database Design - Introduction to Databases"
excerpt: "CS377: Database Design - Introduction to Databases"

info:
  points: 3
  instructions: "Modify the MyFirstStatement.sql file to insert the number 42 into the table, and then to retrieve it."
  goals:
    - To become familiar with the basic structure of a database
    - To write a SQL statement
    
canvasasmtid: "107081"   
canvaspoints: 3
  
processor:  
  correctfeedback: "Correct!!" 
  incorrectfeedback: "Try again"
  submitformlink: false
  feedbackprocess: | 
    var pos = feedbackString;
  correctcheck: |
    pos.toLowerCase().includes("42")
 
files:
  - filename: "MyFirstStatement.sql"
    name: myfirststatement
    ismain: false
    isreadonly: false
    isvisible: true
    code: | 
        -- TODO: insert a value into the mytable database table
        -- TODO: retrive the value from the table

  - filename: "Setup.sql"
    ismain: true
    name: main
    isreadonly: true
    isvisible: true
    code: |
        CREATE TABLE mytable (a int);
        
---
