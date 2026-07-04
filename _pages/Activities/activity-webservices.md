---
layout: activity
permalink: /Activities/WebServices
title: "CS377: Database Design - RESTful Web Services to Map to CRUD Functionality"


info:
  goals: 
    - To integrate a Flask web service with a NoSQL database
    - To differentiate the layers of database interfaces (driver/DB-API, ORM, and REST) and choose an appropriate one for an application
  additional_reading:
    - title: "Flask RESTful Web Services"
      link: "https://blog.miguelgrinberg.com/post/designing-a-restful-api-with-python-and-flask"
    - title: "Authentication with Flask"
      link: "https://blog.miguelgrinberg.com/post/restful-authentication-with-flask"
    - title: "Python Requests Library"
      link: "https://realpython.com/python-requests/"
    - title: "How to use curl"
      link: "https://flaviocopes.com/http-curl/"      
    
  models:
    - model: |
        <a title="Santiago Paredes, CC BY 3.0 &lt;https://creativecommons.org/licenses/by/3.0&gt;, via Wikimedia Commons" href="https://commons.wikimedia.org/wiki/File:SQLyHTTP.JPG"><img width="512" alt="SQLyHTTP" src="https://commons.wikimedia.org/w/index.php?title=Special:Redirect/file/SQLyHTTP.JPG"></a>
      title: Creating a RESTful Web Service in Python with Flask
      embed: |
        <iframe
          height="600px"
          width="100%"
          src="https://www.billmongan.com/Ursinus-CS377/assets/code-viewer.html?zip=https%3A%2F%2Fraw.githubusercontent.com%2FBillJr99%2FUrsinus-CS377%2Fgh-pages%2Ffiles%2Freplit%2FPythonFlaskDBExample.zip&title=Python%20Flask%20DB%20Example"
          scrolling="yes"
          frameborder="no"
          allowfullscreen="true"
          sandbox="allow-scripts allow-same-origin">
        </iframe>      
      questions:
        - "The URL bindings to each function look similar from function to function; what differentiates them and what actions each function takes?"
        - "What HTTP <strong>methods</strong> (or verbs) do you see in this program?  To what part of the CRUD model does each correspond?"
        - "What happens if you request a person ID that doesn't exist?"
        - "Investigate what it means to be a <strong>RESTful</strong> web service?"
        - "Investigate how to use <a href=\"https://curl.se/docs/manpage.html\">curl</a> to invoke these web services."
        - "How would you modify this example to incorporate a NoSQL database backend?  How about a relational database backend?"
    - model: |
        <script type="syntaxhighlighter" class="brush: python"><![CDATA[        
        import requests
        
        resp = requests.post("http://127.0.0.1/api/v1/person", json={"age": 38, "name": "Alex"}, headers={'Accept': 'application/json'})
        ]]></script>
      title: Making a Web Service Client Request
      questions:
        - "How might you make an HTTP get request to retrieve the set of people from your example web service?"
        - "Investigate how to add authentication to an HTTP request."
        - "How would you make these requests using curl?"
    - model: |
        <table border="1" cellpadding="4">
          <caption>Three layers at which a program can talk to a database</caption>
          <tr><th>Layer</th><th>You write</th><th>Example</th><th>Who typically uses it</th></tr>
          <tr><td>Driver / DB-API</td><td>SQL strings</td><td><code>cursor.execute("SELECT * FROM person WHERE id = ?", (pid,))</code></td><td>Code running next to the database</td></tr>
          <tr><td>ORM</td><td>Classes and objects</td><td><code>session.get(Person, pid)</code></td><td>Application developers on the same team</td></tr>
          <tr><td>REST web service</td><td>HTTP requests</td><td><code>GET /api/v1/person/1</code></td><td>Any client, anywhere, in any language</td></tr>
        </table>
      title: "Layers of Database Interfaces"
      embed: |
        <iframe
          height="600px"
          width="100%"
          src="https://www.billmongan.com/Ursinus-CS377/assets/code-viewer.html?zip=https%3A%2F%2Fraw.githubusercontent.com%2FBillJr99%2FUrsinus-CS377%2Fgh-pages%2Ffiles%2Freplit%2FFlaskExample.zip&title=Flask%20REST%20Example"
          scrolling="yes"
          frameborder="no"
          allowfullscreen="true"
          sandbox="allow-scripts allow-same-origin">
        </iframe>
      questions:
        - "The embedded Flask example stores its <code>people</code> list in memory rather than a database.  Which layer(s) from the table would you add to persist the data, and where in the code would each go?"
        - "Each layer trades control for convenience.  What does the REST layer give you that the DB-API layer cannot?  What does the DB-API layer let you do that would be awkward through REST?"
        - "Why do we not simply expose the database's own network port (for example, MySQL's port 3306) to the Internet and let clients run SQL directly?  List at least two reasons."
        
tags:
  - nosql
  - restful
  - programming
  
---

## Layers of Database Interfaces

Before diving into REST specifically, it helps to see where a web service sits among the ways a program can talk to a database.  There are three common "altitudes," and real systems usually stack them:

```
+---------------------------------------------------------------+
|  Any client: browser, curl, mobile app, another service        |
|      |  HTTP + JSON ("GET /api/v1/person/1")                   |
|      v                                                         |
|  REST web service (Flask)          <- interface 3: the network |
|      |  Python objects (Person)                                |
|      v                                                         |
|  ORM layer (e.g., SQLAlchemy)      <- interface 2: objects     |
|      |  SQL ("SELECT ... WHERE id = ?")                        |
|      v                                                         |
|  Driver / DB-API (sqlite3, PyMySQL) <- interface 1: SQL        |
|      |  the database's wire protocol                           |
|      v                                                         |
|  Database engine                                               |
+---------------------------------------------------------------+
```

### Interface 1: The Python DB-API (drivers)

Python database drivers — `sqlite3`, `PyMySQL`, `psycopg2` — all follow the same standard, [PEP 249, the Python Database API](https://peps.python.org/pep-0249/).  That is why the code looks so similar no matter which engine you use: `connect()` gives you a connection, `cursor()` gives you a cursor, `execute()` runs SQL (with `?` or `%s` placeholders for parameters), and `fetchall()`/`fetchone()` retrieve results.

```python
import sqlite3

conn = sqlite3.connect("people.db")
cur = conn.cursor()
cur.execute("SELECT name, age FROM person WHERE id = ?", (1,))
row = cur.fetchone()   # e.g., ("Alex", 38)
conn.close()
```

You write raw SQL, so you have full control — and full responsibility for parameterizing inputs (never concatenate!), managing transactions, and translating rows (plain tuples) into whatever objects your program needs.

### Interface 2: The ORM Layer

An **Object-Relational Mapper (ORM)** such as [SQLAlchemy](https://www.sqlalchemy.org/) sits on top of a DB-API driver and maps tables to classes and rows to objects, generating the SQL for you:

```python
person = session.get(Person, 1)   # ORM issues the SELECT for us
print(person.name, person.age)    # a real Python object, not a tuple
```

The ORM handles parameterization, type conversion, and relationships between tables (a `person.emails` attribute instead of a manual join).  The trade-off is a layer of machinery between you and the SQL — for unusual or performance-critical queries, developers often drop back down to interface 1.  We explore this layer in depth in the [SQLAlchemy activity](./SQLAlchemy).

### Interface 3: REST over the Database

The first two interfaces require the client to be *your own program*, running with database credentials and a network route to the database.  A **RESTful web service** wraps the database behind HTTP so that *any* client — a browser, a phone app, `curl`, a program in another language — can use it without credentials to the database itself:

| CRUD operation | SQL (interface 1) | HTTP (interface 3) |
|----------------|-------------------|---------------------|
| Create | `INSERT INTO person ...` | `POST /api/v1/person` |
| Read   | `SELECT ... WHERE id = 1` | `GET /api/v1/person/1` |
| Update | `UPDATE person SET ... WHERE id = 1` | `PUT /api/v1/person/1` |
| Delete | `DELETE FROM person WHERE id = 1` | `DELETE /api/v1/person/1` |

This is why we never expose the database port directly to the Internet: the web service layer enforces *authentication* (who are you?), *authorization* (which rows may you touch?), *validation* (is this input sane?), and *shape* (clients see friendly JSON, not your schema), while the database credentials stay safely on the server — ideally in a `.env` configuration file rather than in the code, as discussed in the [SQL activity](./SQL#keeping-credentials-out-of-your-code-with-dotenv).

**Choosing a layer:** inside one program, use the DB-API or an ORM; between programs, machines, or organizations, put a REST interface in front.  Most production systems use all three at once — exactly the stack you will build in the [RESTful Web Services assignment](../Assignments/RESTful).

## RESTful Web Services
Representational State Transfer (REST)ful Web Services are a popular architecture for building scalable and interoperable distributed systems. They provide an efficient way to expose data and functionality through HTTP endpoints. 

### Flask RESTful Web Services
[Flask RESTful Web Services](https://blog.miguelgrinberg.com/post/designing-a-restful-api-with-python-and-flask) is a blog post by Miguel Grinberg that provides an in-depth tutorial on designing RESTful APIs with Python and Flask. The tutorial covers various aspects of building web services, including resource modeling, routing, request handling, and response formatting. The post emphasizes the use of Flask-RESTful, an extension that simplifies the development of RESTful APIs with Flask.

According to Grinberg, Flask-RESTful offers powerful abstractions to define resources as classes and map them to URLs using routing decorators. It also provides request parsing, input validation, and output serialization capabilities out of the box. Grinberg gives detailed examples and code snippets to showcase these features. The tutorial also highlights the importance of using HTTP status codes appropriately to communicate the outcome of requests.

### How to use curl
[curl](https://flaviocopes.com/http-curl/) is a popular command-line tool for making HTTP requests. Flavio Copes's blog post provides a comprehensive guide on how to use `curl` effectively.

The guide starts with the basics of making GET and POST requests using `curl` and covers various features and options available. It describes how to pass headers, cookies, HTTP authentication, and handle redirects. Additionally, it demonstrates how to make requests with a specific HTTP method, set request body data, and handle response headers and status codes.

An example of making a GET request using `curl`:

```bash
curl -X GET https://api.example.com/users
```

### Python Requests Library
The [Python Requests Library](https://realpython.com/python-requests/) is a comprehensive guide by Real Python on using the `requests` library to interact with RESTful APIs. The `requests` library is an elegant and simple HTTP library for Python, widely used for making HTTP requests.

The guide demonstrates the various HTTP methods supported by `requests`, including GET, POST, PUT, and DELETE. It also covers authentication, headers, query parameters, and handling responses in both JSON and XML formats. Real Python emphasizes best practices, such as using session objects for handling persistent connections and working with asynchronous requests using `requests-futures`.

An example of performing a GET request using the `requests` library:

```python
import requests

response = requests.get('https://api.example.com/users')
if response.status_code == 200:
    users = response.json()
    print(users)
```

#### Example

Here's an example of a POST request:

```python
import requests
import json

url = 'https://jsonplaceholder.typicode.com/posts'
data = {'title': 'foo', 'body': 'bar', 'userId': 1}

response = requests.post(url, data=json.dumps(data))

print(response.status_code)
print(response.json())
```

And here's an example of a PUT request:

```python
import requests
import json

url = 'https://jsonplaceholder.typicode.com/posts/1'
data = {'id': 1, 'title': 'foo', 'body': 'bar', 'userId': 1}

response = requests.put(url, data=json.dumps(data))

print(response.status_code)
print(response.json())
```

In these examples, we're using the JSONPlaceholder API, which is a simple fake REST API for testing and prototyping.

The equivalent CURL commands would be:

POST:

```bash
curl -X POST -H "Content-Type: application/json" -d '{"title":"foo", "body":"bar", "userId":1}' https://jsonplaceholder.typicode.com/posts
```

PUT:

```bash
curl -X PUT -H "Content-Type: application/json" -d '{"id":1, "title":"foo", "body":"bar", "userId":1}' https://jsonplaceholder.typicode.com/posts/1
```

- POST is used to submit data to be processed to a specified resource. It's often used when you want to upload a file or submit a completed web form.
- PUT is used to update a current resource with new data. It's often used when you're updating existing records.

### Authentication
There are several RESTful authentication methods, including Basic Auth, OAuth, JWT (JSON Web Tokens), and API Keys. 

For Basic Auth, here's an example in Python:

```python
import requests
from requests.auth import HTTPBasicAuth

response = requests.get('https://api.github.com/user', auth=HTTPBasicAuth('user', 'pass'))

print(response.status_code)
```

And the equivalent CURL command:

```bash
curl -u user:pass https://api.github.com/user
```

In this example, we're accessing the GitHub API, which supports Basic Auth for some operations. You would replace 'user' and 'pass' with your actual GitHub username and password (which should be stored outside of your code, perhaps in an encrypted file that only your user has read access to).

## Accessing RESTful Data through a Web Page

```
<!DOCTYPE html>
<html>
<head>
    <title>Weather App</title>
    <style>
        #weather {
            font-size: 2em;
            margin-top: 20px;
        }
    </style>
</head>
<body>
    <h1>Current Weather</h1>
    <div id="weather">Loading...</div>

    <script>
        // Initial API endpoint
        const initialApiUrl = 'https://api.weather.gov/points/40.194,-75.4563';

        // Fetch initial data from API
        fetch(initialApiUrl)
            .then(response => response.json())
            .then(data => {
                // Get forecast URL from initial data
                const forecastApiUrl = data.properties.forecast;

                // Fetch forecast data from API
                return fetch(forecastApiUrl);
            })
            .then(response => response.json())
            .then(data => {
                // Update div with forecast data
                const weatherDiv = document.getElementById('weather');
                const forecast = data.properties.periods[0];
                weatherDiv.innerHTML = `
                    <h2>${forecast.name}</h2>
                    <p>${forecast.detailedForecast}</p>
                `;
            })
            .catch(error => {
                console.error('Error:', error);
            });
    </script>
</body>
</html>
```
