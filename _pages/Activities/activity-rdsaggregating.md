---
layout: activity
permalink: /Activities/RDS/Aggregating
title: "CS377: Database Design - Aggregation in Relational Databases"
excerpt: "CS377: Database Design - Aggregation in Relational Databases"

info:
  goals: 
    - To explain the use of primary and foreign keys in database systems
    - To aggregate records across multiple tables with referential keys
    - To express basic queries in the programmatic language SQL (Structured Query Language)
  additional_reading:
    - link: https://comptoolsres.github.io/Database_Introduction.html
      title: Database Introduction
    - link: https://www.sqlite.org/lang_aggfunc.html
      title: Sqlite Aggregating Functions
      
  models:
    - model: |
        <table style="border-collapse:collapse;border-spacing:0" class="tg"><thead><tr><th style="background-color:#000000;border-color:inherit;border-style:solid;border-width:1px;color:#ffffff;font-family:Arial, sans-serif;font-size:14px;font-weight:normal;overflow:hidden;padding:10px 5px;text-align:center;vertical-align:top;word-break:normal">FirstName</th><th style="background-color:#000000;border-color:inherit;border-style:solid;border-width:1px;color:#ffffff;font-family:Arial, sans-serif;font-size:14px;font-weight:normal;overflow:hidden;padding:10px 5px;text-align:center;vertical-align:top;word-break:normal">LastName</th><th style="background-color:#000000;border-color:inherit;border-style:solid;border-width:1px;color:#ffffff;font-family:Arial, sans-serif;font-size:14px;font-weight:normal;overflow:hidden;padding:10px 5px;text-align:center;vertical-align:top;word-break:normal">Age</th></tr></thead><tbody><tr><td style="border-color:inherit;border-style:solid;border-width:1px;font-family:Arial, sans-serif;font-size:14px;overflow:hidden;padding:10px 5px;text-align:left;vertical-align:top;word-break:normal">Alex</td><td style="border-color:inherit;border-style:solid;border-width:1px;font-family:Arial, sans-serif;font-size:14px;overflow:hidden;padding:10px 5px;text-align:left;vertical-align:top;word-break:normal">Smith</td><td style="border-color:inherit;border-style:solid;border-width:1px;font-family:Arial, sans-serif;font-size:14px;overflow:hidden;padding:10px 5px;text-align:left;vertical-align:top;word-break:normal">20</td></tr><tr><td style="border-color:inherit;border-style:solid;border-width:1px;font-family:Arial, sans-serif;font-size:14px;overflow:hidden;padding:10px 5px;text-align:left;vertical-align:top;word-break:normal">Lee</td><td style="border-color:inherit;border-style:solid;border-width:1px;font-family:Arial, sans-serif;font-size:14px;overflow:hidden;padding:10px 5px;text-align:left;vertical-align:top;word-break:normal">Jones</td><td style="border-color:inherit;border-style:solid;border-width:1px;font-family:Arial, sans-serif;font-size:14px;overflow:hidden;padding:10px 5px;text-align:left;vertical-align:top;word-break:normal">21</td></tr><tr><td style="border-color:inherit;border-style:solid;border-width:1px;font-family:Arial, sans-serif;font-size:14px;overflow:hidden;padding:10px 5px;text-align:left;vertical-align:top;word-break:normal">Brian</td><td style="border-color:inherit;border-style:solid;border-width:1px;font-family:Arial, sans-serif;font-size:14px;overflow:hidden;padding:10px 5px;text-align:left;vertical-align:top;word-break:normal">McMullen</td><td style="border-color:inherit;border-style:solid;border-width:1px;font-family:Arial, sans-serif;font-size:14px;overflow:hidden;padding:10px 5px;text-align:left;vertical-align:top;word-break:normal">18</td></tr><tr><td style="border-color:inherit;border-style:solid;border-width:1px;font-family:Arial, sans-serif;font-size:14px;overflow:hidden;padding:10px 5px;text-align:left;vertical-align:top;word-break:normal">Samantha</td><td style="border-color:inherit;border-style:solid;border-width:1px;font-family:Arial, sans-serif;font-size:14px;overflow:hidden;padding:10px 5px;text-align:left;vertical-align:top;word-break:normal">Johnson</td><td style="border-color:inherit;border-style:solid;border-width:1px;font-family:Arial, sans-serif;font-size:14px;overflow:hidden;padding:10px 5px;text-align:left;vertical-align:top;word-break:normal">22</td></tr><tr><td style="border-color:black;border-style:solid;border-width:1px;font-family:Arial, sans-serif;font-size:14px;overflow:hidden;padding:10px 5px;text-align:left;vertical-align:top;word-break:normal">Lee</td><td style="border-color:black;border-style:solid;border-width:1px;font-family:Arial, sans-serif;font-size:14px;overflow:hidden;padding:10px 5px;text-align:left;vertical-align:top;word-break:normal">Jones</td><td style="border-color:black;border-style:solid;border-width:1px;font-family:Arial, sans-serif;font-size:14px;overflow:hidden;padding:10px 5px;text-align:left;vertical-align:top;word-break:normal">24</td></tr></tbody></table>
        <br>
        <table style="border-collapse:collapse;border-spacing:0" class="tg"><thead><tr><th style="background-color:#000000;border-color:inherit;border-style:solid;border-width:1px;color:#ffffff;font-family:Arial, sans-serif;font-size:14px;font-weight:normal;overflow:hidden;padding:10px 5px;text-align:center;vertical-align:top;word-break:normal">CourseNum</th><th style="background-color:#000000;border-color:inherit;border-style:solid;border-width:1px;color:#ffffff;font-family:Arial, sans-serif;font-size:14px;font-weight:normal;overflow:hidden;padding:10px 5px;text-align:center;vertical-align:top;word-break:normal">CourseName</th></tr></thead><tbody><tr><td style="border-color:inherit;border-style:solid;border-width:1px;font-family:Arial, sans-serif;font-size:14px;overflow:hidden;padding:10px 5px;text-align:left;vertical-align:top;word-break:normal">CS377</td><td style="border-color:inherit;border-style:solid;border-width:1px;font-family:Arial, sans-serif;font-size:14px;overflow:hidden;padding:10px 5px;text-align:left;vertical-align:top;word-break:normal">Database Design</td></tr><tr><td style="border-color:inherit;border-style:solid;border-width:1px;font-family:Arial, sans-serif;font-size:14px;overflow:hidden;padding:10px 5px;text-align:left;vertical-align:top;word-break:normal">CS173</td><td style="border-color:inherit;border-style:solid;border-width:1px;font-family:Arial, sans-serif;font-size:14px;overflow:hidden;padding:10px 5px;text-align:left;vertical-align:top;word-break:normal">Intro to Computer Science</td></tr><tr><td style="border-color:inherit;border-style:solid;border-width:1px;font-family:Arial, sans-serif;font-size:14px;overflow:hidden;padding:10px 5px;text-align:left;vertical-align:top;word-break:normal">CS174</td><td style="border-color:inherit;border-style:solid;border-width:1px;font-family:Arial, sans-serif;font-size:14px;overflow:hidden;padding:10px 5px;text-align:left;vertical-align:top;word-break:normal">Object Oriented Programming</td></tr><tr><td style="border-color:inherit;border-style:solid;border-width:1px;font-family:Arial, sans-serif;font-size:14px;overflow:hidden;padding:10px 5px;text-align:left;vertical-align:top;word-break:normal">CS275</td><td style="border-color:inherit;border-style:solid;border-width:1px;font-family:Arial, sans-serif;font-size:14px;overflow:hidden;padding:10px 5px;text-align:left;vertical-align:top;word-break:normal">Software Engineering</td></tr></tbody></table>
      title: Tables
      questions:
        - "How might you compare database tables and records, with software classes and objects?"
        - "How can you differentiate between the two students named Lee?"
        - "Not all cultures use &quot;first&quot; and &quot;last&quot; names; what might be a better choice for these column names?"
    - model: |
        <table style="border-collapse:collapse;border-spacing:0" class="tg"><thead><tr><th style="background-color:#000000;border-color:inherit;border-style:solid;border-width:1px;color:#ffffff;font-family:Arial, sans-serif;font-size:14px;font-weight:normal;overflow:hidden;padding:10px 5px;text-align:center;vertical-align:top;word-break:normal">FirstName</th><th style="background-color:#000000;border-color:inherit;border-style:solid;border-width:1px;color:#ffffff;font-family:Arial, sans-serif;font-size:14px;font-weight:normal;overflow:hidden;padding:10px 5px;text-align:center;vertical-align:top;word-break:normal">LastName</th><th style="background-color:#000000;border-color:inherit;border-style:solid;border-width:1px;color:#ffffff;font-family:Arial, sans-serif;font-size:14px;font-weight:normal;overflow:hidden;padding:10px 5px;text-align:center;vertical-align:top;word-break:normal">Age</th><th style="background-color:#000000;border-color:black;border-style:solid;border-width:1px;color:#ffffff;font-family:Arial, sans-serif;font-size:14px;font-weight:normal;overflow:hidden;padding:10px 5px;text-align:left;vertical-align:top;word-break:normal">Course</th></tr></thead><tbody><tr><td style="border-color:inherit;border-style:solid;border-width:1px;font-family:Arial, sans-serif;font-size:14px;overflow:hidden;padding:10px 5px;text-align:left;vertical-align:top;word-break:normal">Alex</td><td style="border-color:inherit;border-style:solid;border-width:1px;font-family:Arial, sans-serif;font-size:14px;overflow:hidden;padding:10px 5px;text-align:left;vertical-align:top;word-break:normal">Smith</td><td style="border-color:inherit;border-style:solid;border-width:1px;font-family:Arial, sans-serif;font-size:14px;overflow:hidden;padding:10px 5px;text-align:left;vertical-align:top;word-break:normal">20</td><td style="border-color:black;border-style:solid;border-width:1px;font-family:Arial, sans-serif;font-size:14px;overflow:hidden;padding:10px 5px;text-align:left;vertical-align:top;word-break:normal">CS377 Database Design</td></tr><tr><td style="border-color:inherit;border-style:solid;border-width:1px;font-family:Arial, sans-serif;font-size:14px;overflow:hidden;padding:10px 5px;text-align:left;vertical-align:top;word-break:normal">Lee</td><td style="border-color:inherit;border-style:solid;border-width:1px;font-family:Arial, sans-serif;font-size:14px;overflow:hidden;padding:10px 5px;text-align:left;vertical-align:top;word-break:normal">Jones</td><td style="border-color:inherit;border-style:solid;border-width:1px;font-family:Arial, sans-serif;font-size:14px;overflow:hidden;padding:10px 5px;text-align:left;vertical-align:top;word-break:normal">21</td><td style="border-color:black;border-style:solid;border-width:1px;font-family:Arial, sans-serif;font-size:14px;overflow:hidden;padding:10px 5px;text-align:left;vertical-align:top;word-break:normal">CS377 Database Design</td></tr><tr><td style="border-color:inherit;border-style:solid;border-width:1px;font-family:Arial, sans-serif;font-size:14px;overflow:hidden;padding:10px 5px;text-align:left;vertical-align:top;word-break:normal">Brian</td><td style="border-color:inherit;border-style:solid;border-width:1px;font-family:Arial, sans-serif;font-size:14px;overflow:hidden;padding:10px 5px;text-align:left;vertical-align:top;word-break:normal">McMullen</td><td style="border-color:inherit;border-style:solid;border-width:1px;font-family:Arial, sans-serif;font-size:14px;overflow:hidden;padding:10px 5px;text-align:left;vertical-align:top;word-break:normal">18</td><td style="border-color:black;border-style:solid;border-width:1px;font-family:Arial, sans-serif;font-size:14px;overflow:hidden;padding:10px 5px;text-align:left;vertical-align:top;word-break:normal">CS173 Intro to Computer Science</td></tr><tr><td style="border-color:inherit;border-style:solid;border-width:1px;font-family:Arial, sans-serif;font-size:14px;overflow:hidden;padding:10px 5px;text-align:left;vertical-align:top;word-break:normal">Samantha</td><td style="border-color:inherit;border-style:solid;border-width:1px;font-family:Arial, sans-serif;font-size:14px;overflow:hidden;padding:10px 5px;text-align:left;vertical-align:top;word-break:normal">Johnson</td><td style="border-color:inherit;border-style:solid;border-width:1px;font-family:Arial, sans-serif;font-size:14px;overflow:hidden;padding:10px 5px;text-align:left;vertical-align:top;word-break:normal">22</td><td style="border-color:black;border-style:solid;border-width:1px;font-family:Arial, sans-serif;font-size:14px;overflow:hidden;padding:10px 5px;text-align:left;vertical-align:top;word-break:normal">CS174 Object Oriented Programming</td></tr><tr><td style="border-color:black;border-style:solid;border-width:1px;font-family:Arial, sans-serif;font-size:14px;overflow:hidden;padding:10px 5px;text-align:left;vertical-align:top;word-break:normal">Lee</td><td style="border-color:black;border-style:solid;border-width:1px;font-family:Arial, sans-serif;font-size:14px;overflow:hidden;padding:10px 5px;text-align:left;vertical-align:top;word-break:normal">Jones</td><td style="border-color:black;border-style:solid;border-width:1px;font-family:Arial, sans-serif;font-size:14px;overflow:hidden;padding:10px 5px;text-align:left;vertical-align:top;word-break:normal">24</td><td style="border-color:black;border-style:solid;border-width:1px;font-family:Arial, sans-serif;font-size:14px;overflow:hidden;padding:10px 5px;text-align:left;vertical-align:top;word-break:normal">CS174 Object Oriented Programming</td></tr><tr><td style="border-color:black;border-style:solid;border-width:1px;font-family:Arial, sans-serif;font-size:14px;overflow:hidden;padding:10px 5px;text-align:left;vertical-align:top;word-break:normal">Lee</td><td style="border-color:black;border-style:solid;border-width:1px;font-family:Arial, sans-serif;font-size:14px;overflow:hidden;padding:10px 5px;text-align:left;vertical-align:top;word-break:normal">Jones</td><td style="border-color:black;border-style:solid;border-width:1px;font-family:Arial, sans-serif;font-size:14px;overflow:hidden;padding:10px 5px;text-align:left;vertical-align:top;word-break:normal">21</td><td style="border-color:black;border-style:solid;border-width:1px;font-family:Arial, sans-serif;font-size:14px;overflow:hidden;padding:10px 5px;text-align:left;vertical-align:top;word-break:normal">CS275 Software Engineering</td></tr></tbody></table>
      title: Primary and Foreign Keys
      questions:
        - "What is unfortunate about the structure of these tables?  What could we do to improve upon it?"
        - "Modify the tables above to add a &quot;serial number&quot; or a <strong>primary key</strong> to each of the tables."
        - "Can you think of a way to identify courses without having to number them?  What might a more &quot;natural key&quot; be?"
        - "What disadvantage could arise from using the data itself (like &quot;CS377&quot;) as a key, particularly if that data changes over time?"
        - "Eliminate the redundant data in these tables by replacing any redundancies with a new column and row specifying the appropriate key value that can be looked up in the corresponding table.  This is called a <strong>foreign key</strong>."
    - model: |
        <table style="border-collapse:collapse;border-spacing:0" class="tg"><thead><tr><th style="background-color:#000000;border-color:inherit;border-style:solid;border-width:1px;color:#ffffff;font-family:Arial, sans-serif;font-size:14px;font-weight:normal;overflow:hidden;padding:10px 5px;text-align:center;vertical-align:top;word-break:normal">FirstName</th><th style="background-color:#000000;border-color:inherit;border-style:solid;border-width:1px;color:#ffffff;font-family:Arial, sans-serif;font-size:14px;font-weight:normal;overflow:hidden;padding:10px 5px;text-align:center;vertical-align:top;word-break:normal">LastName</th><th style="background-color:#000000;border-color:inherit;border-style:solid;border-width:1px;color:#ffffff;font-family:Arial, sans-serif;font-size:14px;font-weight:normal;overflow:hidden;padding:10px 5px;text-align:center;vertical-align:top;word-break:normal">Age</th><th style="background-color:#000000;border-color:black;border-style:solid;border-width:1px;color:#ffffff;font-family:Arial, sans-serif;font-size:14px;font-weight:normal;overflow:hidden;padding:10px 5px;text-align:left;vertical-align:top;word-break:normal">Course</th></tr></thead><tbody><tr><td style="border-color:inherit;border-style:solid;border-width:1px;font-family:Arial, sans-serif;font-size:14px;overflow:hidden;padding:10px 5px;text-align:left;vertical-align:top;word-break:normal">Alex</td><td style="border-color:inherit;border-style:solid;border-width:1px;font-family:Arial, sans-serif;font-size:14px;overflow:hidden;padding:10px 5px;text-align:left;vertical-align:top;word-break:normal">Smith</td><td style="border-color:inherit;border-style:solid;border-width:1px;font-family:Arial, sans-serif;font-size:14px;overflow:hidden;padding:10px 5px;text-align:left;vertical-align:top;word-break:normal">20</td><td style="border-color:black;border-style:solid;border-width:1px;font-family:Arial, sans-serif;font-size:14px;overflow:hidden;padding:10px 5px;text-align:left;vertical-align:top;word-break:normal">CS377 Database Design</td></tr><tr><td style="border-color:inherit;border-style:solid;border-width:1px;font-family:Arial, sans-serif;font-size:14px;overflow:hidden;padding:10px 5px;text-align:left;vertical-align:top;word-break:normal">Lee</td><td style="border-color:inherit;border-style:solid;border-width:1px;font-family:Arial, sans-serif;font-size:14px;overflow:hidden;padding:10px 5px;text-align:left;vertical-align:top;word-break:normal">Jones</td><td style="border-color:inherit;border-style:solid;border-width:1px;font-family:Arial, sans-serif;font-size:14px;overflow:hidden;padding:10px 5px;text-align:left;vertical-align:top;word-break:normal">21</td><td style="border-color:black;border-style:solid;border-width:1px;font-family:Arial, sans-serif;font-size:14px;overflow:hidden;padding:10px 5px;text-align:left;vertical-align:top;word-break:normal">CS377 Database Design</td></tr><tr><td style="border-color:inherit;border-style:solid;border-width:1px;font-family:Arial, sans-serif;font-size:14px;overflow:hidden;padding:10px 5px;text-align:left;vertical-align:top;word-break:normal">Brian</td><td style="border-color:inherit;border-style:solid;border-width:1px;font-family:Arial, sans-serif;font-size:14px;overflow:hidden;padding:10px 5px;text-align:left;vertical-align:top;word-break:normal">McMullen</td><td style="border-color:inherit;border-style:solid;border-width:1px;font-family:Arial, sans-serif;font-size:14px;overflow:hidden;padding:10px 5px;text-align:left;vertical-align:top;word-break:normal">18</td><td style="border-color:black;border-style:solid;border-width:1px;font-family:Arial, sans-serif;font-size:14px;overflow:hidden;padding:10px 5px;text-align:left;vertical-align:top;word-break:normal">CS173 Intro to Computer Science</td></tr><tr><td style="border-color:inherit;border-style:solid;border-width:1px;font-family:Arial, sans-serif;font-size:14px;overflow:hidden;padding:10px 5px;text-align:left;vertical-align:top;word-break:normal">Samantha</td><td style="border-color:inherit;border-style:solid;border-width:1px;font-family:Arial, sans-serif;font-size:14px;overflow:hidden;padding:10px 5px;text-align:left;vertical-align:top;word-break:normal">Johnson</td><td style="border-color:inherit;border-style:solid;border-width:1px;font-family:Arial, sans-serif;font-size:14px;overflow:hidden;padding:10px 5px;text-align:left;vertical-align:top;word-break:normal">22</td><td style="border-color:black;border-style:solid;border-width:1px;font-family:Arial, sans-serif;font-size:14px;overflow:hidden;padding:10px 5px;text-align:left;vertical-align:top;word-break:normal">CS174 Object Oriented Programming</td></tr><tr><td style="border-color:black;border-style:solid;border-width:1px;font-family:Arial, sans-serif;font-size:14px;overflow:hidden;padding:10px 5px;text-align:left;vertical-align:top;word-break:normal">Lee</td><td style="border-color:black;border-style:solid;border-width:1px;font-family:Arial, sans-serif;font-size:14px;overflow:hidden;padding:10px 5px;text-align:left;vertical-align:top;word-break:normal">Jones</td><td style="border-color:black;border-style:solid;border-width:1px;font-family:Arial, sans-serif;font-size:14px;overflow:hidden;padding:10px 5px;text-align:left;vertical-align:top;word-break:normal">24</td><td style="border-color:black;border-style:solid;border-width:1px;font-family:Arial, sans-serif;font-size:14px;overflow:hidden;padding:10px 5px;text-align:left;vertical-align:top;word-break:normal">CS174 Object Oriented Programming</td></tr><tr><td style="border-color:black;border-style:solid;border-width:1px;font-family:Arial, sans-serif;font-size:14px;overflow:hidden;padding:10px 5px;text-align:left;vertical-align:top;word-break:normal">Lee</td><td style="border-color:black;border-style:solid;border-width:1px;font-family:Arial, sans-serif;font-size:14px;overflow:hidden;padding:10px 5px;text-align:left;vertical-align:top;word-break:normal">Jones</td><td style="border-color:black;border-style:solid;border-width:1px;font-family:Arial, sans-serif;font-size:14px;overflow:hidden;padding:10px 5px;text-align:left;vertical-align:top;word-break:normal">21</td><td style="border-color:black;border-style:solid;border-width:1px;font-family:Arial, sans-serif;font-size:14px;overflow:hidden;padding:10px 5px;text-align:left;vertical-align:top;word-break:normal">CS275 Software Engineering</td></tr></tbody></table>
      title: Aggregation
      questions:
        - "Using your new table structure, describe an algorithm to determine the average age of students enrolled in CS377."
        - "What other types of aggregation functions might be useful across these tables?"
        - "Extend the course database to show enrollments in a particular semester; once the class agrees on a design, draw out the tables and data including the key values."
    - model: |
        <script type="syntaxhighlighter" class="brush: sql"><![CDATA[        
        -- Students Table
        CREATE TABLE STUDENTS (
            ID INTEGER NOT NULL PRIMARY KEY AUTOINCREMENT, 
            FirstName TEXT NOT NULL, 
            LastName TEXT NOT NULL, 
            Age INTEGER
        );

        INSERT INTO STUDENTS (FirstName, LastName, Age) VALUES ("Alex", "Smith", 20);
        INSERT INTO STUDENTS (FirstName, LastName, Age) VALUES ("Lee", "Jones", 21);
        INSERT INTO STUDENTS (FirstName, LastName, Age) VALUES ("Brian", "McMullen", 18);
        INSERT INTO STUDENTS (FirstName, LastName, Age) VALUES ("Samantha", "Johnson", 22);
        INSERT INTO STUDENTS (FirstName, LastName, Age) VALUES ("Lee", "Jones", 24);

        -- Courses Table
        CREATE TABLE COURSES (
          ID INTEGER NOT NULL PRIMARY KEY AUTOINCREMENT, 
          CourseNum TEXT NOT NULL, 
          CourseName TEXT NOT NULL
        );

        INSERT INTO COURSES (CourseNum, CourseName) VALUES ("CS377", "Database Design");
        INSERT INTO COURSES (CourseNum, CourseName) VALUES ("CS173", "Intro to Computer Science");
        INSERT INTO COURSES (CourseNum, CourseName) VALUES ("CS174", "Object Oriented Programming");
        INSERT INTO COURSES (CourseNum, CourseName) VALUES ("CS275", "Software Engineering");

        -- Try it out
        SELECT * FROM STUDENTS;
        SELECT * FROM COURSES;

        -- Link the Tables Together with Primary and Foreign Keys
        CREATE TABLE ENROLLMENTS (
          ID INTEGER NOT NULL PRIMARY KEY AUTOINCREMENT, 
          StudentID INTEGER NOT NULL, 
          CourseID INTEGER NOT NULL, 
          FOREIGN KEY(StudentID) REFERENCES STUDENTS(ID), 
          FOREIGN KEY(CourseID) REFERENCES COURSES(ID)
        );

        INSERT INTO ENROLLMENTS(StudentID, CourseID) VALUES (1, 1);
        INSERT INTO ENROLLMENTS(StudentID, CourseID) VALUES (2, 1);
        INSERT INTO ENROLLMENTS(StudentID, CourseID) VALUES (3, 2);

        SELECT * FROM ENROLLMENTS;

        -- Join
        SELECT * FROM ENROLLMENTS 
          INNER JOIN STUDENTS
            ON STUDENTS.ID = ENROLLMENTS.StudentID
          INNER JOIN COURSES
            ON COURSES.ID = ENROLLMENTS.CourseID;

        -- Aggregation
        SELECT 
          COUNT(ENROLLMENTS.ID) AS NumStudents, 
          AVG(STUDENTS.Age) AS AvgAge 
        FROM ENROLLMENTS
          INNER JOIN STUDENTS
            ON STUDENTS.ID = ENROLLMENTS.StudentID
          INNER JOIN COURSES
            ON COURSES.ID = ENROLLMENTS.CourseID
        WHERE COURSES.CourseNum = "CS377";
        
        -- Group and Sort
        SELECT 
          COUNT(ENROLLMENTS.ID) AS NumStudents, 
          AVG(STUDENTS.Age) AS AvgAge,
          CourseNum
        FROM ENROLLMENTS
          INNER JOIN STUDENTS
            ON STUDENTS.ID = ENROLLMENTS.StudentID
          INNER JOIN COURSES
            ON COURSES.ID = ENROLLMENTS.CourseID
        GROUP BY CourseNum
        ORDER BY NumStudents DESC;        
        ]]></script>
      title: The Structured Query Language (SQL)
      questions:
        - "Which statements create tables, and which statements insert records into tables?"
        - "What is unique about the ID columns?  What does <code>AUTOINCREMENT</code> mean?"
        - "What are the values of the <code>STUDENTS</code> and <code>COURSES</code> tables?"
    - model: |
        <script type="syntaxhighlighter" class="brush: sql"><![CDATA[        
        -- These use the table created by the statements above...
        -- You can paste that code together to run everything at once
        -- Join
        SELECT * FROM ENROLLMENTS 
          INNER JOIN STUDENTS
            ON STUDENTS.ID = ENROLLMENTS.StudentID
          INNER JOIN COURSES
            ON COURSES.ID = ENROLLMENTS.CourseID;

        -- Aggregation
        SELECT 
          COUNT(ENROLLMENTS.ID) AS NumStudents, 
          AVG(STUDENTS.Age) AS AvgAge 
        FROM ENROLLMENTS
          INNER JOIN STUDENTS
            ON STUDENTS.ID = ENROLLMENTS.StudentID
          INNER JOIN COURSES
            ON COURSES.ID = ENROLLMENTS.CourseID
        WHERE COURSES.CourseNum = "CS377";
        
        -- Group and Sort
        SELECT 
          COUNT(ENROLLMENTS.ID) AS NumStudents, 
          AVG(STUDENTS.Age) AS AvgAge,
          CourseNum
        FROM ENROLLMENTS
          INNER JOIN STUDENTS
            ON STUDENTS.ID = ENROLLMENTS.StudentID
          INNER JOIN COURSES
            ON COURSES.ID = ENROLLMENTS.CourseID
        GROUP BY CourseNum
        ORDER BY NumStudents DESC;        
        ]]></script>
      title: "Aggregating, Joining, Grouping, and Sorting with SQL"
      embed: |
        <iframe height="400px" width="100%" src="https://repl.it/@BillJr99/Sql-AggregationExample?lite=true" scrolling="no" frameborder="no" allowtransparency="true" allowfullscreen="true" sandbox="allow-forms allow-pointer-lock allow-popups allow-same-origin allow-scripts allow-modals"></iframe>       
      questions:
        - "What is being used to create <strong>aggregated</strong> calculated columns, like the average of a column?"
        - "What clause is used to give a column a custom name?"
        - "How do you think you sort by the average age of the students in each class in ascending order?"
        - "What do you think the <code>INNER JOIN</code> keyword does, and what do you think the resulting table looks like?"
        - "Modify the SQL code example below to incorporate the revisions that the class has recommended."
        
tags:
  - tables
  - aggregation
  - keys
  - rds
  - sql
  
---

