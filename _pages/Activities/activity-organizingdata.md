---
layout: activity
permalink: /Activities/OrganizingData
title: "CS377: Database Design - Data Organization: Fields, Records, and Keys"


info:
  goals: 
    - To define a record, field, and key in a database system
    - To explain the importance and challenges of internal consistency
    - To represent sparse data compactly with Compressed Sparse Row (CSR) storage and decode it back to its original form
    
  models:
    - model: |
        <img alt="Ham Radio Logbook Showing Two Records with Slightly Different Field Values" src="../images/logbook.png">
      title: "Records, Fields, and Keys"
      questions:
        - "What records do you see in the data?  What fields?"
        - "What should happen if a particular field does not have a value?"
        - "Two records are sometimes linked together; what do you think this means in this application?"
        - "The two records are somewhat different; how, and what should be done about this?"
        - "What field(s) are most likely to be unique throughout the table?  These are referred to as a <strong>key</strong>, but a single serial number is often used instead to guarantee uniqueness."
    - model: |
        <img alt="An Example Gradebook" src="https://s3.amazonaws.com/kb-media.populi.co/course_gradebook_editing_grades.png">
      title: "Internal Consistency"
      questions:
        - "Which fields should a user be able to update?  Which ones should a user not update directly, and why?"
    - model: |
        <table border="1" cellpadding="4">
          <caption>A mostly-empty matrix, and the three arrays that store only its nonzero values in Compressed Sparse Row (CSR) form</caption>
          <tr><th></th><th>col 0</th><th>col 1</th><th>col 2</th></tr>
          <tr><th>row 0</th><td>1</td><td>0</td><td>2</td></tr>
          <tr><th>row 1</th><td>0</td><td>3</td><td>4</td></tr>
          <tr><th>row 2</th><td>5</td><td>6</td><td>7</td></tr>
        </table>
        <pre>
        data    = [1, 2, 3, 4, 5, 6, 7]   # the nonzero values, row by row
        indices = [0, 2, 1, 2, 0, 1, 2]   # the column of each value
        indptr  = [0, 2, 4, 7]            # where each row starts in data
        </pre>
      title: "Compressed Sparse Row (CSR) Storage"
      embed: |
        <iframe
          height="600px"
          width="100%"
          src="https://www.billmongan.com/Ursinus-CS377/assets/code-viewer.html?zip=https%3A%2F%2Fraw.githubusercontent.com%2FBillJr99%2FUrsinus-CS377%2Fgh-pages%2Ffiles%2Freplit%2FCompressedSparseRowGraphDFSExamplePython.zip&title=Compressed%20Sparse%20Row%20Graph%20DFS%20Example"
          scrolling="yes"
          frameborder="no"
          allowfullscreen="true"
          sandbox="allow-scripts allow-same-origin">
        </iframe>
      questions:
        - "Using only the three arrays, reconstruct row 1 of the matrix: <code>indptr[1] = 2</code> and <code>indptr[2] = 4</code>, so row 1's values are <code>data[2:4]</code> in columns <code>indices[2:4]</code>.  What are they, and does your answer match the table?"
        - "How many values does row <code>i</code> contain, in terms of <code>indptr</code>?  What does it mean when <code>indptr[i] == indptr[i+1]</code>?"
        - "The dense 3&times;3 matrix stores 9 numbers; CSR stores 7 + 7 + 4 = 18.  For this small, mostly-full matrix, CSR is <em>bigger</em>!  For what kinds of data does CSR win, and by how much would it win for a 1,000,000 &times; 1,000,000 matrix with 10 nonzeros per row?"
        - "Run the embedded example, which stores a graph's edges as a CSR adjacency matrix and traverses it with depth-first search.  Where in the code are <code>indptr</code> and <code>indices</code> used to find a node's neighbors?"
        
tags:
  - records
  - fields
  - keys  
---

In the field of databases and data management, it is essential to understand how data is organized to effectively store, retrieve, and manipulate information. One fundamental concept is the organization of data into fields, records, and keys, which forms the foundation of many database systems.  In this context, a field represents an individual data item, a record represents a set of related fields, and a key serves as a unique identifier for each record.

## Fields

A field is a single piece of information stored in a database. It represents an attribute of an entity or an object. For instance, in a database of employees, fields could include the employee's name, age, and job title. Each field contains a specific type of data, such as text, number, date, or Boolean.

A field, also known as an attribute, is the smallest unit of data in a database system. It can hold various types of data, such as numbers, text, dates, or even binary values. Fields should be carefully defined to ensure consistency and accuracy in data representation. For instance, when designing a database for a library, fields like book title, author, publication year, and ISBN number can be defined to store relevant information.

In Python, fields can be represented using variables of appropriate data types. For example, consider a field called `age` to store the age of individuals. We can define and assign a value to this field as follows:

```python
age = 25
```

## Records

Records are collections of related fields that represent a complete unit of information. In the context of a database, a record typically refers to a row in a table. For example, an employee record may include fields such as name, age, job title, department, and salary.

A record is a collection of related fields that together represent a complete set of information. Records allow us to organize data efficiently and facilitate data retrieval and manipulation operations. In the library database example, each book can be represented as a record, consisting of fields such as title, author, publication year, and ISBN number.

In Python, records can be represented using various data structures such as lists, tuples, or dictionaries. For instance, suppose we define a record representing a person's information as a dictionary:

```python
person = {
    "name": "John",
    "age": 25,
    "gender": "Male"
}
```

Here, the keys `"name"`, `"age"`, and `"gender"` represent the fields, and their corresponding values represent the data associated with each field.

## Keys

A key is a field or combination of fields used to uniquely identify each record within a database table. Keys are crucial for efficient querying and indexing operations. A primary key is a unique identifier for a record and is often used as a reference for other tables. Alternatively, a composite key is a combination of two or more fields that, when combined, uniquely identify a record.  There are various types of keys, such as primary keys, candidate keys, and foreign keys.

In Python, keys can be implemented using a combination of fields that form a tuple or a dictionary. For instance, let's consider a record representing a book in a library database, where the ISBN number can serve as the key:

```python
book = {
    "title": "Introduction to Database Systems",
    "author": "C. J. Date",
    "publication_year": 2004,
    "isbn": "978-0321197849"
}
```

Here, the `"isbn"` field serves as the key, which uniquely identifies this particular book record.

## Python Examples

In Python, data can be organized using data structures such as dictionaries, lists, and classes. Here are some examples of organizing data using Python:

1. Dictionary example:
   ```python
   employee = {
       'name': 'John Doe',
       'age': 30,
       'job_title': 'Software Engineer',
       'department': 'IT',
       'salary': 50000
   }
   ```

2. List of dictionaries example:
   ```python
   employees = [
       {'name': 'John Doe', 'age': 30, 'job_title': 'Software Engineer', 'salary': 50000},
       {'name': 'Jane Smith', 'age': 25, 'job_title': 'Data Analyst', 'salary': 45000},
       {'name': 'Mike Johnson', 'age': 35, 'job_title': 'Project Manager', 'salary': 60000}
   ]
   ```
   
3. Class example:
   ```python
   class Employee:
       def __init__(self, name, age, job_title, salary):
           self.name = name
           self.age = age
           self.job_title = job_title
           self.salary = salary
   
   employee = Employee('John Doe', 30, 'Software Engineer', 50000)
   ```

## Storing Sparse Data: Compressed Sparse Row (CSR)

So far our records have been *dense*: every field of every record holds a value.  But much real data is **sparse** — almost entirely empty.  Think of a table of *which customers bought which products* (most customers buy almost none of the products), a word-document frequency matrix in a search engine, or the friendship graph of a social network (most pairs of people are not friends).  Storing every empty cell explicitly wastes almost all of the space.

**Compressed Sparse Row (CSR)** storage solves this by keeping only the nonzero values, together with just enough bookkeeping to know where each one belongs.  It is how scientific libraries (like `scipy.sparse`), search engines, and graph databases physically lay out sparse tables and adjacency matrices.

### The Three Arrays

CSR replaces a matrix with three flat arrays:

| Array | One entry per... | Meaning |
|-------|------------------|---------|
| `data` | nonzero value | the values themselves, read left-to-right, top row first |
| `indices` | nonzero value | the **column** where the matching `data` entry lives |
| `indptr` | row, plus one extra | `indptr[i]` says where row `i` **starts** inside `data`/`indices` |

The name says it all: the rows are *compressed* — instead of storing each row's empty cells, we store one pointer per row into the packed value list.

### Encoding, Step by Step

Take this 3×3 matrix (the same one as in the model above and in the embedded example):

|       | col 0 | col 1 | col 2 |
|-------|-------|-------|-------|
| row 0 | 1     | 0     | 2     |
| row 1 | 0     | 3     | 4     |
| row 2 | 5     | 6     | 7     |

1. **Walk the matrix row by row, skipping zeros**, appending each nonzero value to `data` and its column to `indices`:
   - Row 0 contributes value `1` (column 0) and value `2` (column 2).
   - Row 1 contributes `3` (column 1) and `4` (column 2).
   - Row 2 contributes `5` (column 0), `6` (column 1), and `7` (column 2).
   - Result: `data = [1, 2, 3, 4, 5, 6, 7]`, `indices = [0, 2, 1, 2, 0, 1, 2]`.
2. **Record where each row began.**  Row 0 started at position 0; row 1 started at position 2 (row 0 used two slots); row 2 started at position 4; and everything ends at position 7.  So `indptr = [0, 2, 4, 7]` — always one entry longer than the number of rows, so every row has both a start and an end.

### Decoding, Step by Step

To read **row `i`**, slice between consecutive row pointers — this is the entire trick:

1. `start = indptr[i]` and `end = indptr[i+1]`.
2. Row `i`'s values are `data[start:end]`.
3. Their columns are `indices[start:end]`.
4. Every other column in row `i` is zero.

Worked for row 1: `start = indptr[1] = 2`, `end = indptr[2] = 4`; the values `data[2:4] = [3, 4]` belong in columns `indices[2:4] = [1, 2]`.  Filling the remaining column (0) with zero reconstructs row 1 exactly: `[0, 3, 4]`.  As a bonus, `end - start` (here `4 - 2 = 2`) is the number of nonzeros in the row — no scanning required.

A single element lookup, say cell `(1, 2)`, is the same slice plus a search: among `indices[2:4] = [1, 2]`, column 2 appears at offset 1 of the slice, so the value is `data[2 + 1] = 4`.

```python
import numpy as np
from scipy.sparse import csr_matrix

m = csr_matrix((np.array([1, 2, 3, 4, 5, 6, 7]),      # data
                np.array([0, 2, 1, 2, 0, 1, 2]),      # indices
                np.array([0, 2, 4, 7])),              # indptr
               shape=(3, 3))
print(m.toarray())
```

Expected output:

```
[[1 0 2]
 [0 3 4]
 [5 6 7]]
```

### Why Databases Care

- **Space:** a matrix with a million rows and columns but ~10 nonzeros per row needs about 10<sup>7</sup> stored numbers in CSR instead of 10<sup>12</sup> cells dense — a 100,000× saving.  (Our tiny 3×3 example is *worse* in CSR — compression only pays when most cells are empty.)
- **Row access is fast:** fetching a row is one slice — exactly the access pattern of "give me this customer's purchases" or "give me this node's neighbors."  The embedded example above exploits this to run depth-first search over a graph stored in CSR form.
- **Trade-off:** *column* access and single-cell updates are awkward (inserting a nonzero shifts everything after it, like inserting into the middle of an array).  A sibling format, CSC (Compressed Sparse **Column**), makes the opposite trade — another instance of the recurring database theme that the right physical organization depends on your query pattern.
