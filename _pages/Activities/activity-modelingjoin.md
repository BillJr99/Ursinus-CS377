---
layout: activity
permalink: /Activities/Modeling/Join
title: "CS377: Database Design - Data Modeling and the Join"


info:
  goals: 
    - To model table joins
    - To differentiate between the different type of joins
    - To identify potential anomalies in data schemas
    - To take steps to normalize data schemas to avoid anomalies
  additional_reading:
    - title: "SQL Joins"
      link: "https://en.wikipedia.org/wiki/Join_(SQL)"
  
  models:
    - model: |
        <img src="https://opentextbc.ca/wp-content/uploads/sites/11/2013/12/Bank-Accounts-1-300x197.jpg" alt="Bank Accounts Table from Database Design 2nd Ed by Watt and Eng">
      title: Relational Design
      questions:
        - "What data redundancies do you see in this table, and how can you fix each?"
        - "How would you change the address of a bank?  Remove a bank?  Insert a new account an an existing back, but with an updated address?  These are <strong>update anomalies</strong>, <strong>deletion anomalies</strong>, and <strong>insertion anomalies</strong>."
        - "Design a schema that eliminates data redundancy in this table."
    - model: |
        <img src="https://opentextbc.ca/wp-content/uploads/sites/11/2013/12/Ch-10-ProjectEmp-table.jpg" alt="Flawed Projects Table from Database Design 2nd Ed by Watt and Eng">
        <br>
        <img src="https://opentextbc.ca/wp-content/uploads/sites/11/2013/12/Ch-10-Project-to-Emp-ERD-300x114.jpg" alt="An Improved Projects Schema from Database Design 2nd Ed by Watt and Eng">
        <br>
        <img src="https://opentextbc.ca/wp-content/uploads/sites/11/2013/12/Ch-10-Project-and-Emp-tables-300x89.jpg" alt="The Improved Projects Table from Database Design 2nd Ed by Watt and Eng">
      title: Case Study
      questions:
        - "Induce as many anomalies as you can in the flawed table above!"
        - "How does the improved (<strong>normalized</strong>) schema help prevent the anomalies you were able to identify?"
    - model: |
        <h3>Inner Join</h3>
        <a title="GermanX, CC BY-SA 4.0 &lt;https://creativecommons.org/licenses/by-sa/4.0&gt;, via Wikimedia Commons" href="https://commons.wikimedia.org/wiki/File:SQL_Join_-_07_A_Inner_Join_B.svg"><img width="128" alt="SQL Join - 07 A Inner Join B" src="https://upload.wikimedia.org/wikipedia/commons/thumb/1/18/SQL_Join_-_07_A_Inner_Join_B.svg/128px-SQL_Join_-_07_A_Inner_Join_B.svg.png"></a>
        <br>
        <h3>Left Outer Join</h3>
        <a title="GermanX, CC BY-SA 4.0 &lt;https://creativecommons.org/licenses/by-sa/4.0&gt;, via Wikimedia Commons" href="https://commons.wikimedia.org/wiki/File:SQL_Join_-_01_A_Left_Join_B.svg"><img width="128" alt="SQL Join - 01 A Left Join B" src="https://upload.wikimedia.org/wikipedia/commons/thumb/f/f6/SQL_Join_-_01_A_Left_Join_B.svg/128px-SQL_Join_-_01_A_Left_Join_B.svg.png"></a>
      title: The SQL Join
      questions:
        - "Joins are classified by which records are included if a corresponding match is not found in one table.  An <strong>inner join</strong> includes only records that match across both tables.  A <strong>left outer</strong> join includes all rows from the first table and their corresponding match from the second table (or <code>NULL</code> if no match exists from the second table.  What do you think a <strong>right outer join is</strong>, and a <strong>full outer join</strong>?"
        - "What records are included in an inner join, a left outer join, a right outer join, and a full outer join, for <a href=\"https://en.wikipedia.org/wiki/Join_(SQL)\">this data table</a>?  Write the SQL <code>JOIN</code> statements required to implement each join by linking the <code>DepartmentID</code> column."
        
tags:
  - join
  - sql
  
---

## Facilitating Integrity with Modeling and the SQL Join

In the field of database management, ensuring data integrity is of utmost importance. Data integrity refers to the accuracy, consistency, and reliability of data stored in a database. One of the ways to facilitate data integrity is through the use of modeling and the SQL Join operation.

### SQL Joins

A SQL Join is a powerful operation that combines rows from two or more tables based on a related column between them. It allows data from multiple tables to be retrieved and combined in a meaningful way. The result of a join is a new table, also known as a result set, that combines rows from the joined tables based on a specified condition. The condition is typically the equality between the values in the related columns.

The Wikipedia article on [SQL Joins](https://en.wikipedia.org/wiki/Join_(SQL)) provides a comprehensive introduction to the topic. It explains various types of joins, including inner join, left join, right join, and outer join, along with their semantics and practical examples. This article serves as an excellent starting point for understanding SQL joins and their applications.
