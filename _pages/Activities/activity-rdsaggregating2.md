---
layout: activity
permalink: /Activities/RDS/Aggregating2
title: "CS377: Database Design - Aggregation in Relational Databases"
excerpt: "CS377: Database Design - Aggregation in Relational Databases"

info:
  prev: ./Aggregating
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
        <script type="syntaxhighlighter" class="brush: sql"><![CDATA[   
        PRAGMA foreign_keys = ON; -- Enforce foreign key constraints
        
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
        - "Try selecting all data from the <code>sqlite_master</code> table, and the <code>sqlite_sequence</code> table.  What do you think these contain?"
        - "How might you update or delete records in these tables?"
        - "What should you be careful of when deleting records?"
    - model: |
        <script type="syntaxhighlighter" class="brush: sql"><![CDATA[        
        INSERT INTO ENROLLMENTS(StudentID, CourseID) VALUES (
          (SELECT ID FROM STUDENTS WHERE FirstName="Alex" AND LastName="Smith"), 
          (SELECT ID FROM COURSES WHERE CourseNum="CS377")
        );
        INSERT INTO ENROLLMENTS(StudentID, CourseID) VALUES (
          (SELECT ID FROM STUDENTS WHERE FirstName="Lee" AND LastName="Jones"), 
          (SELECT ID FROM COURSES WHERE CourseNum="CS377")
        );
        INSERT INTO ENROLLMENTS(StudentID, CourseID) VALUES (
          (SELECT ID FROM STUDENTS WHERE FirstName="Brian" AND LastName="McMullen"), 
          (SELECT ID FROM COURSES WHERE CourseNum="CS173")
        );       
        ]]></script>
      title: "Inserting with SQL Subqueries"
      embed: |
        <iframe height="400px" width="100%" src="https://repl.it/@BillJr99/Sql-AggregationSubqueryExample?lite=true" scrolling="no" frameborder="no" allowtransparency="true" allowfullscreen="true" sandbox="allow-forms allow-pointer-lock allow-popups allow-same-origin allow-scripts allow-modals"></iframe>       
      questions:
        - "What values are being inserted into the <code>ENROLLMENTS</code> table, and how?"        
        
tags:
  - tables
  - aggregation
  - keys
  - rds
  - sql
  
---

## SQL Aggregation Functions

SQL aggregation functions are used to perform calculations on multiple rows of a single column of a table. They return a single value. Here are some examples:

1. **COUNT()**: This function returns the number of rows that matches a specified criterion.

    ```sql
    SELECT COUNT(column_name)
    FROM table_name
    WHERE condition;
    ```

2. **SUM()**: This function returns the total sum of a numeric column.

    ```sql
    SELECT SUM(column_name)
    FROM table_name
    WHERE condition;
    ```

3. **AVG()**: This function returns the average value of a numeric column.

    ```sql
    SELECT AVG(column_name)
    FROM table_name
    WHERE condition;
    ```

4. **MIN() and MAX()**: These functions return the smallest and largest value of the selected column respectively.

    ```sql
    SELECT MIN(column_name)
    FROM table_name
    WHERE condition;

    SELECT MAX(column_name)
    FROM table_name
    WHERE condition;
    ```

5. **GROUP BY**: This statement is often used with aggregate functions (COUNT, MAX, MIN, SUM, AVG) to group the result-set by one or more columns.

    ```sql
    SELECT column_name, aggregate_function(column_name)
    FROM table_name
    WHERE condition
    GROUP BY column_name;
    ```

6. **HAVING**: This clause was added to SQL because the WHERE keyword could not be used with aggregate functions. It is often used with the GROUP BY clause.

    ```sql
    SELECT column_name, aggregate_function(column_name)
    FROM table_name
    WHERE condition
    GROUP BY column_name
    HAVING aggregate_function(column_name) condition;
    ```

## SQL Subqueries

A subquery is a SQL query nested inside a larger query. A subquery may occur in:

- A SELECT clause
- A FROM clause
- A WHERE clause

The subquery can be nested inside a SELECT, INSERT, UPDATE, or DELETE statement or inside another subquery. Here is an example:

```sql
SELECT column_name
FROM table_name
WHERE column_name = (SELECT column_name FROM table_name WHERE condition);
```

You can find more examples of subqueries in these repositories:

- [CSE 344: Introduction to Data Management](https://github.com/ldfaiztt/CSE344/blob/c765a2b62d1688c423c3acd8064c46e54f8b6460/lecture07-sql-subqueries-additional-examples.sql)
- [SQL_use_case_chinook_db](https://github.com/alzaia/SQL_use_case_chinook_db/blob/f753bf346378baaf133a47c217d04b535bfccd16/SQLite_Chinook_code/03_sql_subqueries_and_joins.sql)
- [data_management_group5](https://github.com/Gaoyuan66/data_management_group5/blob/549d706f726a870f0276988fe46c74fd2ce45b70/Session3/2021/SQL.Subqueries.and.Views.sql)

## SQL Joins
A JOIN clause is used to combine rows from two or more tables, based on a related column between them. Here are the different types of SQL JOINs:

1. ***INNER JOIN***: The INNER JOIN keyword selects records that have matching values in both tables.

```sql
SELECT column_name(s)
FROM table1
INNER JOIN table2
ON table1.column_name = table2.column_name;
```

2. ***LEFT (OUTER) JOIN***: The LEFT JOIN keyword returns all records from the left table (`table1`), and the matched records from the right table (`table2`). The result is NULL from the right side, if there is no match.

```sql
SELECT column_name(s)
FROM table1
LEFT JOIN table2
ON table1.column_name = table2.column_name;
```

3. ***RIGHT (OUTER) JOIN***: The RIGHT JOIN keyword returns all records from the right table (`table2`), and the matched records from the left table (`table1`). The result is NULL from the left side, when there is no match.

```sql
SELECT column_name(s)
FROM table1
RIGHT JOIN table2
ON table1.column_name = table2.column_name;
```

4. ***FULL (OUTER) JOIN***: The FULL OUTER JOIN keyword return all records when there is a match in either left (`table1`) or right (`table2`) table records.

```sql
SELECT column_name(s)
FROM table1
FULL OUTER JOIN table2
ON table1.column_name = table2.column_name;
```

You can find more examples of joins in this repository:

- [SQL_use_case_chinook_db](https://github.com/alzaia/SQL_use_case_chinook_db/blob/f753bf346378baaf133a47c217d04b535bfccd16/SQLite_Chinook_code/03_sql_subqueries_and_joins.sql)

## Data Cleansing

**Data cleansing**, also known as data cleaning or data scrubbing, is the process of identifying and correcting or removing corrupt, inaccurate, incomplete, or irrelevant parts of data in a dataset. It's a crucial step in the data preparation process because the quality of data directly impacts the quality of insights and decisions made from that data.

### Common Data Cleansing Techniques

Here are some common data cleansing techniques:

1. **Removing Duplicates**: Duplicate data can occur for many reasons and can skew analysis results.

2. **Handling Missing Values**: Missing data can be handled in several ways, such as ignoring the record, filling the missing value with a specific value or an average, or using a prediction model to estimate the missing value.

3. **Data Type Correction**: Sometimes, data can be recorded in the wrong format. For example, a numerical value could be recorded as a string. Correcting the data type ensures that the data can be used correctly in calculations and comparisons.

4. **Syntax or Spelling Corrections**: This includes correcting typos, capitalization errors, and inconsistent spellings.

### SQL Examples for Data Cleansing

Now, let's look at some SQL examples for these data cleansing techniques. Note that these examples are generic and may need to be adjusted based on your specific RDS database and tables.

**1. Removing Duplicates**

```sql
DELETE FROM table_name
WHERE row_id NOT IN (
    SELECT MIN(row_id)
    FROM table_name
    GROUP BY column1, column2, ..., columnN
);
```

**2. Handling Missing Values**

```sql
-- Filling missing values with a specific value
UPDATE table_name
SET column_name = 'value'
WHERE column_name IS NULL;

-- Filling missing values with an average
UPDATE table_name
SET column_name = (
    SELECT AVG(column_name) 
    FROM table_name
)
WHERE column_name IS NULL;
```

**3. Data Type Correction**

```sql
-- Changing data type from string to integer
ALTER TABLE table_name
ALTER COLUMN column_name TYPE INT USING column_name::integer;
```

**4. Syntax or Spelling Corrections**

```sql
-- Correcting a typo
UPDATE table_name
SET column_name = REPLACE(column_name, 'incorrect', 'correct')
WHERE column_name LIKE '%incorrect%';
```

Remember, data cleansing is an iterative process and often requires a deep understanding of the data you're working with. Always backup your data before performing any data cleansing operations.
