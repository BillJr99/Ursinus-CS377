---
layout: syllabus
permalink: /
title: "CS377: Databases"
excerpt: "CS377: Databases"
    
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
  course_prerequisites: "CS275"
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
      starttime: "1:00 AM"
      endtime: "1:50 AM"
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
    - fdate: "TBD"
      fstarttime: "TBD"
      fendtime: "TBD"
      froom: "TBD"    
  flexible_submission_policy: "In the absence of <a href=\"#accommodations\">accommodations</a> arranged in advance with the instructor or college, all assignments are due at 10:59PM Eastern Time on the date(s) stated on the schedule.  Assignments will be accepted without prior permission following this time with a points deduction of 5% per day if submitted before 10:59 PM Eastern Time on the day submitted.  This policy does not apply to extra credit opportunities: extra credit will not be awarded for assignments submitted under the flexible submission policy.  Late work cannot be accepted after the final class meeting, nor during final exams week, nor after the exam." 
  late_penalty_per_period: 5
  late_penalty_period: "day"
  banner: |
    <div style="width: 100%; display: table; border-collapse:separate; border-spacing:5px;">
    <div style="width: 100%; display: table-row;">
        <div style="display: table-cell; padding:5px; width:33%;">
            <a title="BernardoSulzbach, CC BY-SA 4.0 &lt;https://creativecommons.org/licenses/by-sa/4.0&gt;, via Wikimedia Commons" href="https://commons.wikimedia.org/wiki/File:DVD_Rental_Query.png"><img width="512" alt="DVD Rental Query" src="https://upload.wikimedia.org/wikipedia/commons/thumb/f/f2/DVD_Rental_Query.png/512px-DVD_Rental_Query.png"></a>
        </div>
        <div style="display: table-cell; padding:5px; width:33%;">
        <a title="Vitaly Zdanevich, CC0, via Wikimedia Commons" href="https://commons.wikimedia.org/wiki/File:Aws-dynamodb-webconsole-item_(cropped).png"><img width="256" alt="Aws-dynamodb-webconsole-item (cropped)" src="https://upload.wikimedia.org/wikipedia/commons/thumb/4/4d/Aws-dynamodb-webconsole-item_%28cropped%29.png/256px-Aws-dynamodb-webconsole-item_%28cropped%29.png"></a>    
        </div>
        <div style="display: table-cell; padding:5px; width:33%;">
        <img src="images/DatabaseSchema.png" alt="Example Record-Based Database Schema>
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
    endtime: "2:00 AM"
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
  image: https://opentextbc.ca/dbdesign01/wp-content/uploads/sites/11/2019/02/OTB008-Database-Design-2018-COVER-350x453.jpg
  isrequired: true 
  freelyavailable: true

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
  weight: "30%"
- category: "Quizzes"
  weight: "10%"  
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
    submission_types: "noupload"
          
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

Welcome to CS377!