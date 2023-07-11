---
layout: syllabus
permalink: /
title: "CS377: Database Design"
excerpt: "CS377: Database Design"
    
info:
  course_number: CS377
  course_sections: 
  - section: "A"
  course_title: "Database Design"
  credit_hours: "4 Semester Hours"
  course_homepage: "https://www.billmongan.com/Ursinus-CS377-Fall2021/"
  teamshelproom: https://teams.microsoft.com/l/channel/19%3a6ddddb88493946fa956387e9543a3b06%40thread.tacv2/Mongan%2520Drop-In%2520Office%2520Hours?groupId=b16dcd6b-3522-4564-8306-9051a92c68ba&tenantId=921f1c03-8689-4e60-a722-f5ea581e00fe
  class_notebook: https://ursinuscollege365-my.sharepoint.com/personal/wmongan_ursinus_edu/Documents/Class%20Notebooks/CS377%20Fall%202021
  ical: files/CS377.ics
  course_prerequisites: "CS274"
  course_start_date: "2021/08/30"
  course_end_date: "2021/12/10"
  course_description: "The concepts involved in designing and using a database management system. Logical and physical database design.  Entity-Relational Modeling. Various types of database structures, manipulations of a database structure through applications, query techniques, and programming in a database language. Prerequisite: CS-275. Offered in the fall of  odd years. Three hours per week."
  welcome_message: "Welcome to CS377!"
  class_meets_days:
    isM: true
    isT: false
    isW: true
    isR: false
    isF: true 
    isS: false
    isU: false
  class_meets_locations:
  - section:
    - day: "M"
      starttime: "11:00 AM"
      endtime: "11:50 AM"
      place: "IDC 116"
    - day: "W"
      starttime: "11:00 AM"
      endtime: "11:50 AM"
      place: "IDC 116"
    - day: "F"
      starttime: "11:00 AM"
      endtime: "11:50 AM"
      place: "IDC 116"    
  midtermexam: 
    - mdate: "TBD"
      mstarttime: "TBD"
      mendtime: "TBD"
      mroom: "TBD"       
  finalexam: 
    - fdate: "2021/12/13"
      fstarttime: "10:00 AM"
      fendtime: "12:00 PM"
      froom: "IDC 116"    
  flexible_submission_policy: "In the absence of <a href=\"#accommodations\">accommodations</a> arranged in advance with the instructor or college, all assignments are due at 10:59PM Eastern Time on the date(s) stated on the schedule.  Assignments will be accepted without prior permission following this time with a points deduction of 4% per day if submitted before 10:59 PM Eastern Time on the day submitted.  Each student will receive a total of 10 &quot;slack days&quot; for the semester with which to waive these grade reductions; for example, one assignment may be submitted 10 days late, or two assignments may be submitted 5 days late, with no grade reduction.  Should an exemption to this policy be requested and granted, a 5% per day reduction will be applied.  Extra credit will not be awarded for assignments submitted under the flexible submission policy.  Students with accommodations will receive additional &quot;slack days&quot; as specified within the accommodations letter; however, some deliverables cannot be subject to accommodations due to the time-sensitive nature of the assignment (for example, group assignments, presentations, and course surveys).  Students who add the class late shall receive additional slack days equal to the number of days between the start of classes and the first date that approval is given or that class is attended (whichever occurs first).  Under no circumstances (including accommodations) can late work be accepted after the final class meeting, nor during final exams week, nor after the exam." 
  late_penalty_per_period: 4
  late_penalty_period: "day"
  banner: |
    <div style="width: 100%; display: table; border-collapse:separate; border-spacing:5px;">
    <div style="width: 100%; display: table-row;">
        <div style="display: table-cell; padding:5px; width:33%;">
            <a title="BernardoSulzbach, CC BY-SA 4.0 &lt;https://creativecommons.org/licenses/by-sa/4.0&gt;, via Wikimedia Commons" href="https://commons.wikimedia.org/wiki/File:DVD_Rental_Query.png"><img width="256" alt="DVD Rental Query" src="https://upload.wikimedia.org/wikipedia/commons/thumb/f/f2/DVD_Rental_Query.png/512px-DVD_Rental_Query.png"></a>
        </div>
        <div style="display: table-cell; padding:5px; width:33%;">
        <a title="Timo Tijhof, CC BY 4.0 &lt;https://creativecommons.org/licenses/by/4.0&gt;, via Wikimedia Commons" href="https://commons.wikimedia.org/wiki/File:MediaWiki_1.28.0_database_schema.svg"><img width="288" alt="MediaWiki 1.28.0 database schema" src="https://upload.wikimedia.org/wikipedia/commons/thumb/9/94/MediaWiki_1.28.0_database_schema.svg/512px-MediaWiki_1.28.0_database_schema.svg.png"></a>  
        </div>
        <div style="display: table-cell; padding:5px; width:33%;">
        <img src="images/DatabaseSchema.png" alt="Example Record-Based Database Schema" width="192">
        </div>
    </div>
    </div>
    
instructors:
- name: William Mongan
  title: Professor
  email: wmongan@ursinus.edu
  phone: "610-409-3410"
  office: "Pfahler Hall 101L"
  webpage_url: "http://www.billmongan.com"
  picture: /images/profile.png
  officehours:
  - day: "M"
    starttime: "12:00 PM"
    endtime: "2:00 PM"
    location: "Pfahler Hall 101L"  
  - day: "T"
    starttime: "11:00 AM"
    endtime: "2:00 PM"
    location: "Pfahler Hall 101L"        
  - day: "W"
    starttime: "12:00 PM"
    endtime: "2:00 PM"
    location: "Pfahler Hall 101L"        
  - day: "F"
    starttime: "12:00 PM"
    endtime: "2:00 PM"
    location: "Pfahler Hall 101L"    
    
textbooks:
- title: "Database Design"
  authors: "Adrienne Watt and Nelson Eng"
  edition: "2nd Edition"
  link: https://opentextbc.ca/dbdesign01/open/download?type=pdf
  isrequired: true 
  freelyavailable: https://opentextbc.ca/dbdesign01/open/download?type=pdf
- title: "The Little MongoDB Book"
  authors: "Karl Seguin"
  edition: "Version 2.6 Edition"
  link: https://www.openmymind.net/mongodb.pdf
  isrequired: true
  freelyavailable: https://www.openmymind.net/mongodb.pdf

objectives:
- objective: "To select appropriately between data models including relational and non-relational databases"
- objective: "To scale databases to high-performance data models for real-time cloud deployments"
- objective: "To define and apply the tradeoffs between consistency, scale, and performance"
- objective: "To implement database solutions that are robust and secure"
- objective: "To implement front-end interfaces to explore backend databases"

goals:
- goal: "To harnass the informative potential of data through organization and scale"

grade_breakdown:
- category: "Programming Assignments"
  weight: "40%"
- category: "Labs"
  weight: "25%"
- category: "Exercises"
  weight: "15%"
- category: "Final Project"
  weight: "20%"  

letter_grades:
- letter: "A+"
  range: "96.9-100"
- letter: "A"
  range: "93-96.89"
- letter: "A-"
  range: "89.5-92.99"
- letter: "B+"
  range: "87-89.49"
- letter: "B"
  range: "83-86.99"
- letter: "B-"
  range: "79.5-82.99"
- letter: "C+"
  range: "77-79.49"
- letter: "C"
  range: "73-76.99"
- letter: "C-"
  range: "69.5-72.99"
- letter: "D+"
  range: "67-69.49"
- letter: "D"
  range: "63-66.99"
- letter: "D-"
  range: "59.5-62.99"
- letter: "F"
  range: "0-59.49" 

schedule:
- week: "0"
  date: "0"
  title: "Course Overview: What is a Database, and Why Use Them?"
  link: "../Ursinus-CS377-Overview"   
  deliverables:
  - dtitle: "Programming Assignment: Warmup Handed Out"    
    dlink: "Assignments/Warmup"
    points: 15
    submission_types: "onpaper"
- week: "0"
  date: "1"
  title: "Course Overview: What is a Database, and Why Use Them?"
  readings:
  - rtitle: "Introduction to Databases"
    rlink: "https://www.techopedia.com/6/28832/enterprise/databases/introduction-to-databases"
- week: "0"
  date: "2"
  title: "Managing Data: Text and Files" 
  link: "Activities/TextAndFileManagement"
  readings:
  - rtitle: "DD Ch. 1"
    rlink: false  
- week: "1"
  date: "0"
  title: "File I/O Primer"
  link: "Activities/FileIO"
  deliverables:
  - dtitle: "Programming Assignment: Warmup Due"    
    dlink: "Assignments/Warmup"
    points: 15
    submission_types: "onpaper"
  - dtitle: "Lab: File I/O Handed Out"
    dlink: "Labs/FileIO"
    points: 100    
    rubricpath: "_pages/Labs/lab-fileio.md"    
- week: "1"
  date: "1"
  title: "Organizing Data: Fields, Records, and Keys"
  link: "Activities/OrganizingData"
  deliverables:
  - dtitle: "Exercise: Quadratic Formula in Python"
    dlink: "Modules/Python/Warmup/Exercise"
    points: 3
    submission_types: "onpaper"
  readings:
  - rtitle: "DD Ch. 2"
    rlink: false  
- week: "1"
  date: "2"
  title: "Relational Database Systems (RDS)"
  link: "Activities/RDS"
  deliverables:
  - dtitle: "Programming Assignment: GEDCOM File Format Handed Out"
    dlink: "Assignments/GEDCOM/FileIO"
    points: 100    
    rubricpath: "_pages/Assignments/asmt-gedcomfile.md"  
- week: "2"
  date: "0"
  title: "Relational Database Systems (RDS)"
  deliverables:
  - dtitle: "Lab: File I/O Due"
    dlink: "Labs/FileIO"
    points: 100    
    rubricpath: "_pages/Labs/lab-fileio.md"     
- week: "2"
  date: "1"
  title: "Processing and Aggregating Data Records"
  link: "Activities/RDS/Aggregating"
  deliverables:
  - dtitle: "Exercise: Iteration in Python"
    dlink: "Modules/Python/Iteration/Exercise"
    points: 3
    submission_types: "onpaper"  
  readings:
  - rtitle: "DD Ch. 3"
    rlink: false 
  - rtitle: "Database Introduction"
    rlink: "https://comptoolsres.github.io/Database_Introduction.html"
  - rlink: https://www.sqlite.org/lang_aggfunc.html
    rtitle: Sqlite Aggregating Functions    
- week: "2"
  date: "2"
  title: "Processing and Aggregating Data Records"    
- week: "3"
  date: "0"
  title: "Processing and Aggregating Data Records"
- week: "3"
  date: "1"
  title: "Data Modeling and Schemas"
  link: "Activities/Modeling/Schemas"
  deliverables:
  - dtitle: "Programming Assignment: GEDCOM File Format Due"
    dlink: "Assignments/GEDCOM/FileIO"
    points: 100  
    rubricpath: "_pages/Assignments/asmt-gedcomfile.md"   
  readings:
  - rtitle: "DD Ch. 4-5"
    rlink: false 
- week: "3"
  date: "2"
  title: "Data Modeling and Schemas"
  deliverables:
  - dtitle: "Lab: Database Tables Lab Handed Out"
    dlink: "Labs/DatabaseTables"
    points: 100    
    rubricpath: "_pages/Labs/lab-dbtables.md"   
- week: "4"
  date: "0"
  title: "Data Modeling and Schemas" 
- week: "4"
  date: "1"
  title: "" 
  title: "The Relational Database Model and Database Programming Primer"
  link: "Activities/RelationalModel"
  readings:
  - rtitle: "DD Ch. 6-7"
    rlink: false
  - rlink: https://pypi.org/project/PyMySQL/
    rtitle: PyMySQL Python Library
  - rlink: https://docs.python.org/3/library/sqlite3.html
    rtitle: Sqlite3 Python Library    
  - rlink: https://www.tutorialspoint.com/postgresql/postgresql_python.htm
    rtitle: PostgreSQL Python Library
  - rlink: https://github.com/comptoolsres/Jupyter_content/blob/main/py4e_ch15_databases.ipynb
    rtitle: Databases and SQL    
- week: "4"
  date: "2"
  title: "The Relational Database Model and Database Programming Primer"
  deliverables: 
  - dtitle: "Lab: Schemas Handed Out"
    dlink: "Labs/Schemas"
    points: 100    
    rubricpath: "_pages/Labs/lab-schemas.md"        
- week: "5"
  date: "0"
  title: "The Relational Database Model and Database Programming Primer"
  deliverables:
  - dtitle: "Lab: Database Tables Lab Due"
    dlink: "Labs/DatabaseTables"
    points: 100    
    rubricpath: "_pages/Labs/lab-dbtables.md"    
- week: "5"
  date: "1"
  title: "The Entity-Relational (ER) Model" 
  link: "Activities/ERModel"
  readings:
  - rtitle: "DD Ch. 8"
    rlink: false     
  deliverables: 
  - dtitle: "Programming Assignment: ER Modeling Handed Out"
    dlink: "Assignments/ERModeling"
    points: 100    
    submission_types: "written"      
- week: "5"
  date: "2"
  title: "The Structured Query Language (SQL)" 
  link: "Activities/SQL"
  readings:
  - rtitle: "DD Ch. 15-16"
    rlink: false
  - rtitle: "A Gentle Introduction to SQL"
    rlink: "https://a-gentle-introduction-to-sql.readthedocs.io/en/latest/"    
- week: "6"
  date: "0"
  title: "The Structured Query Language (SQL)"
  deliverables:
  - dtitle: "Lab: Schemas Due"
    dlink: "Labs/Schemas"
    points: 100    
    rubricpath: "_pages/Labs/lab-schemas.md"   
  - dtitle: "Lab: Database Design Lab Handed Out"
    dlink: "Labs/DatabaseDesign"
    points: 100    
    rubricpath: "_pages/Labs/lab-dbdesign.md"   
- week: "6"
  date: "1"
  title: "The Structured Query Language (SQL)"
  deliverables:
  - dtitle: "Exercise: SQL Warmup"
    dlink: "Modules/SQL/Warmup/Exercise"
    points: 3
    submission_types: "onpaper"   
  readings:
  - rtitle: "SQL Injections from Computerphile"
    rlink: "https://www.youtube.com/watch?v=_jKylhJtPmI"
  - rtitle: "Avoiding SQL Injection Attacks by Learning to Execute One"
    rlink: "https://www.youtube.com/watch?v=ciNHn38EyRc"      
- week: "6"
  date: "2"
  title: "Data Integrity"
  link: "Activities/DataIntegrity"  
  readings:
  - rtitle: "DD Ch. 9"
    rlink: false 
- week: "7"
  date: "1"
  title: "Facilitating Integrity with Modeling and the SQL Join"
  link: "Activities/Modeling/Join"
  deliverables:
  - dtitle: "Programming Assignment: ER Modeling Due"
    dlink: "Assignments/ERModeling"
    points: 100    
    submission_types: "written"    
  - dtitle: "Programming Assignment: Database Programming Handed Out"
    dlink: "Assignments/DatabaseProgramming"
    points: 100    
    rubricpath: "_pages/Assignments/asmt-dbprogramming.md"      
  readings:
  - rtitle: "DD Ch. 10"
    rlink: false    
  - rtitle: "SQL Joins"
    rlink: "https://en.wikipedia.org/wiki/Join_(SQL)"    
- week: "7"
  date: "2"
  title: "Facilitating Integrity with Modeling and the SQL Join"
  deliverables:
  - dtitle: "Exercise: SQL Aggregation"
    dlink: "Modules/SQL/Aggregation/Exercise"
    points: 3
    submission_types: "onpaper"    
- week: "8"
  date: "0"
  title: "Facilitating Integrity with Modeling and the SQL Join"
  deliverables:
  - dtitle: "Lab: Database Design Lab Due"
    dlink: "Labs/DatabaseDesign"
    points: 100    
    rubricpath: "_pages/Labs/lab-dbdesign.md"     
- week: "8"
  date: "1"
  title: "Facilitating Integrity with Modeling and the SQL Join"
  deliverables:
  - dtitle: "Exercise: SQL Joins"
    dlink: "Modules/SQL/Join/Exercise"
    points: 3
    submission_types: "onpaper"     
- week: "8"
  date: "2"
  title: "ER Modeling and Normalization"
  link: "Activities/Modeling/Normalization"
  readings:
  - rtitle: "DD Ch. 11-12"
    rlink: false 
  deliverables:
  - dtitle: "Programming Assignment: Database Programming Due"
    dlink: "Assignments/DatabaseProgramming"
    points: 100    
    rubricpath: "_pages/Assignments/asmt-dbprogramming.md"   
  - dtitle: "Programming Assignment: SQL Programming Handed Out"
    dlink: "Assignments/SQLProgramming"
    points: 100    
    rubricpath: "_pages/Assignments/asmt-sqlprogramming.md"  
- week: "9"
  date: "0"
  title: "ER Modeling and Normalization"
- week: "9"
  date: "1"
  title: "ER Modeling and Normalization"
- week: "9"
  date: "2"
  title: "A Non-Relational Database Model: NoSQL"
  link: "Activities/NoSQL"
  readings:
  - rtitle: "M Ch. 4, 8 (1, 5)"
    rlink: false
- week: "10"
  date: "0"
  title: "A Non-Relational Database Model: NoSQL"
  deliverables:
  - dtitle: "Programming Assignment: SQL Programming Due"
    dlink: "Assignments/SQLProgramming"
    points: 100    
    rubricpath: "_pages/Assignments/asmt-sqlprogramming.md"   
  - dtitle: "Programming Assignment: SQL Joins Handed Out"
    dlink: "Assignments/Join"
    points: 100    
    submission_types: "written" 
- week: "10"
  date: "1"
  title: "CRUD with NoSQL" 
  link: "Activities/NoSQL/CRUD"
  readings:
  - rtitle: "M Ch. 5 (2)"
    rlink: false    
  - rtitle: "PyMongo Tutorial"
    rlink: "https://pymongo.readthedocs.io/en/stable/tutorial.html"    
- week: "10"
  date: "2"
  title: "CRUD with NoSQL"
- week: "11"
  date: "0"
  title: "RESTful Web Services with Databases"
  link: "Activities/WebServices"  
  readings:
  - rtitle: "Flask RESTful Web Services"
    rlink: "https://blog.miguelgrinberg.com/post/designing-a-restful-api-with-python-and-flask"  
  - rtitle: "Python Requests Library"
    rlink: "https://realpython.com/python-requests/"
  - rtitle: "How to use curl"
    rlink: "https://flaviocopes.com/http-curl/"
  deliverables:
  - dtitle: "Programming Assignment: SQL Joins Due"
    dlink: "Assignments/Join"
    points: 100    
    submission_types: "written"   
  - dtitle: "Programming Assignment: Join Programming Handed Out"
    dlink: "Assignments/JoinProgramming"
    points: 100
    rubricpath: "_pages/Assignments/asmt-joinprogramming.md"     
- week: "11"
  date: "1"
  title: "RESTful Web Services with Databases"      
- week: "11"
  date: "2"
  title: "NoSQL Data Processing and Aggregation" 
  link: "Activities/NoSQL/Aggregating"    
  readings:
  - rtitle: "M Ch. 6, 9 (3, 6)"
    rlink: false 
  deliverables:
  - dtitle: "Project: Final Project Handed Out"
    dlink: "Projects/Final"
    points: 100    
    rubricpath: "_pages/Projects/proj-final.md"     
- week: "12"
  date: "0"
  title: "NoSQL Data Models: Key-Value, Document, Columnar, and Graph"
  link: "Activities/NoSQL/DataModels"
  deliverables:
  - dtitle: "Programming Assignment: Join Programming Due"
    dlink: "Assignments/JoinProgramming"
    points: 100
    rubricpath: "_pages/Assignments/asmt-joinprogramming.md"    
  - dtitle: "Lab: Graph Databases with Redis Handed Out"
    dlink: "Labs/Redis"
    points: 100    
    rubricpath: "_pages/Labs/lab-redis.md"      
  readings:
  - rtitle: "Types of NoSQL Databases"
    rlink: "https://www.mongodb.com/scale/types-of-nosql-databases"  
  - rtitle: "Setting up Redis"
    rlink: "https://dev.to/ramko9999/host-and-use-redis-for-free-51if"    
- week: "13"
  date: "0"
  title: "Indexing a Denormalized NoSQL Datastore"
  link: "Activities/NoSQL/Indexing"
  readings:
  - rtitle: "M Ch. 7 (4)"
    rlink: false   
  deliverables:
  - dtitle: "Programming Assignment: Normalization Handed Out"
    dlink: "Assignments/Normalization"
    points: 100    
    submission_types: "written"       
- week: "13"
  date: "1"
  title: "Workshop: Toward Scaled Managed Cloud Databases"
  readings:
  - rtitle: "M Ch. 10 (7)"
    rlink: false   
- week: "13"
  date: "2"
  title: "Workshop: Toward Scaled Managed Cloud Databases"    
- week: "14"
  date: "0"
  title: "Workshop: Toward Scaled Managed Cloud Databases"     
  deliverables:
  - dtitle: "Project: Final Project Due"
    dlink: "Projects/Final"
    points: 100    
    rubricpath: "_pages/Projects/proj-final.md"   
- week: "14"
  date: "1"
  title: "Review"   
  deliverables:
  - dtitle: "Lab: Graph Databases with Redis Due"
    dlink: "Labs/Redis"
    points: 100    
    rubricpath: "_pages/Labs/lab-redis.md"     
- week: "14"
  date: "2"
  title: "Review"
  deliverables:   
  - dtitle: "Programming Assignment: Normalization Due"
    dlink: "Assignments/Normalization"
    points: 100    
    submission_types: "written"    
  
university:
  semester: "Fall"
  academicyear: "2021-22"
  fall:
  - kname: "Add Deadline"
    kdate: "2021/09/10"
    kdisplay: true
  - kname: "Mid Semester Grades Posted"
    kdate: "2021/10/15"
    kdisplay: false    
  - kname: "Drop with a W Deadline"
    kdate: "2021/10/27"
    kdisplay: true  
  - kname: "Reading Day"
    kdate: "2021/12/11"
    kdisplay: true     
  - kname: "Finals Week Begins"
    kdate: "2021/12/13"
    kdisplay: false
  - kname: "Finals Week Ends"
    kdate: "2021/12/18"
    kdisplay: false
  spring:
  - kname: "Add Deadline"
    kdate: "2022/02/1"
    kdisplay: true
  - kname: "Mid Semester Grades Posted"
    kdate: "2021/03/4"
    kdisplay: false    
  - kname: "Drop with a W Deadline"
    kdate: "2022/03/23"
    kdisplay: true
  - kname: "Designated Thursday Schedule"
    kdate: "2022/05/4"
    kdisplay: false     
  - kname: "Reading Day"
    kdate: "2022/05/5"
    kdisplay: false    
  - kname: "Finals Week Begins"
    kdate: "2022/05/06"
    kdisplay: false
  - kname: "Finals Week Ends"
    kdate: "2022/05/12"
    kdisplay: false       
  - kname: "Baccalaureate"
    kdate: "2022/05/13"
    kdisplay: false
  - kname: "Commencement"
    kdate: "2022/05/14"
    kdisplay: false 
  fallholidays:
  - date: "2021/10/16"
  - date: "2021/10/17"
  - date: "2021/10/18"
  - date: "2021/10/19"
  - date: "2021/11/24"
  - date: "2021/11/25"
  - date: "2021/11/26"
  - date: "2021/11/27"
  - date: "2021/11/28"
  springholidays:
  - date: "2022/01/17"  
  - date: "2022/03/5"  
  - date: "2022/03/6"  
  - date: "2022/03/7"  
  - date: "2022/03/8"  
  - date: "2022/03/9"  
  - date: "2022/03/10"  
  - date: "2022/03/11"  
  - date: "2022/03/12"  
  - date: "2022/03/13"  
  
---

## Overview
Welcome to CS377: Database Design!  In this course, we will explore models for storing, organizing, indexing, searching, transmitting, and scaling data to make it useful for humans and computers to extract efficiently and effectively. 

## Homework

### Labs
Approximately every week, we will have a lab session where students get a chance to practice concepts we just learned in a safe and [collaborative](#collaboration) environment. Tasks will be given that serve as warm-ups for the larger assignments, and you will have a chance to refine your submissions as you practice.

### Assignments
The bulk of the grade in the course will be earned by completing individual programming assignments. Be sure to start them early! Note that [collaboration and sharing rules](#collaboration) differ slightly for labs and assignments.

## Classroom Participation

### Group Work \[[^1]\]
In addition to ordinary participation that follows the natural rhythm of a lecture, most days there will be at least one followup problem, which is a question that follows on the heels of newly presented material. Students will split into groups of 2 and try to write some code to address a particular problem. When a group of students believe they have figured out the answer, they raise their hand. The other students can continue to work while I verify that the answer is correct. If the answer is correct, the students present the answer to the class. If the group is not correct upon my checking, then the groups continue this process until one gets it correct.

Other ways to help your fellow classmates in class are as follows:

* Helping to teach a student a topic during office hours.
* Certain calls for participation in class
* Particularly helpful or insightful messages on Microsoft Teams
* Finding mistakes in the book or on the assigned homework and labs

### Class Participation and Classroom Etiquette \[[^1]\]
For classroom attendance, the following rules apply:

* Please be attentive during class. There will be class exercises that involve coding, but class time should be used for learning computer science. It is imperative that technology be used for this purpose during our class time together. **Alternatively, please try to think of this as a safe space away from social media.** We could all use a break, and we are fortunate to have a good excuse to make that space.
* Please follow common courtesy. For instance, you can bring food and drink as long as it's not distracting, but please clean up after yourself if you do. Our janitorial staff deserves the utmost respect and help with their job.
* In-class exercises and "low stakes" activities will take place individually and in groups to assess our progress together.  These exercises will be given both synchronously (for example, in-class activities, pair programming exercises) and asynchronously (for example, pre-lab exercises, peer code reviews, book surveys) and will be graded on a participation basis.  These are given equal weight and form the basis of the class participation score.
* If a class session is remote, please feel free to make choices that make you most comfortable.  For example, I will record these sessions for students who cannot make the session or for those who would benefit from a review of the material.  I'd encourage you to enable your video feed if it is available, but if you need leave your video off, you feel free to do so; however, if you find that this becomes necessary on a prolonged basis, please see me to discuss.  Please keep your microphone on mute to avoid background noises while others are speaking; however, please do not feel "mic fright" about unmuting to speak up and participate anytime.  If, however, you would prefer to communicate via the chat interface (either exclusively or in combination with your audio/video), you should feel free to do that.  Whether in-person or remote, all I ask is that you engage as best you can; the material is challenging but fun, and we're all here to learn new things together.

[^1]: This introduction is adapted from Dr. Tralie's CS173 [Course Syllabus](http://www.ctralie.com/Teaching/CS173_S2020/index.html).
