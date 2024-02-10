---
layout: activity
permalink: /Activities/TextAndFileManagement
title: "CS377: Database Design - Text and File Management"


info:
  goals: 
    - To read files for processing
    - To represent models in text file format
    
  models:
    - model: |
        <a title="Gringer, Public domain, via Wikimedia Commons" href="https://commons.wikimedia.org/wiki/File:CousinTree_kinship.svg"><img width="512" alt="CousinTree kinship" src="https://upload.wikimedia.org/wikipedia/commons/thumb/d/d7/CousinTree_kinship.svg/512px-CousinTree_kinship.svg.png"></a>
        <br>
        <iframe src="https://en.wikipedia.org/wiki/GEDCOM#Example" width="100%"></iframe>
      title: "A Flat File Structure: GEDCOM"
      questions:
        - "The GEDCOM file format defines ancestral history.  What do you think each of the line headings mean?  If you aren't sure, write one down and skip it for now; we'll check the <a href=\"https://gedcom.io/specifications/FamilySearchGEDCOMv7.html\">specifications</a> later!"
        - "What do you think the numbers mean at the beginning of each line?"
        - "What is a &quot;record&quot; in this format?  How many different types of records can you find, and how many records of each type are there?"
        - "Draw a diagram representing the family depicted by this example."
        - "Could you represent this data in a more friendly way by making &quot;tables&quot; or spreadsheets?  Try representing the basic information in Microsoft Excel, using the <a href=\"https://support.microsoft.com/en-us/office/vlookup-function-0bbc8083-26fe-4963-8ab8-93a18ad188a1\"><code>VLOOKUP</code> function</a> to refer to data across tables."
    - model: |
        <iframe src="https://api.weatherusa.net/v1/forecast?q=40.1915,-75.4559&daily=0&units=e&maxtime=7d" width="100%"></iframe>
      title: Javascript Object Notation (JSON)
      questions:
        - "This JSON result was returned from a web request to <a href=\"https://api.weatherusa.net/v1/forecast?q=40.1915,-75.4559&daily=0&units=e&maxtime=7d\">https://api.weatherusa.net/v1/forecast?q=40.1915,-75.4559&daily=0&units=e&maxtime=7d</a>, which obtains the 7-day forecast at Ursinus College given the College's latitude and longitude GPS coordinates.  Use a <a href=\"https://jsonformatter.org/json-pretty-print\">JSON Pretty Printer</a> to better format the JSON for reading."
        - What do the curly braces represent?
        - What does the square bracket represent?
      embed: |
        <iframe height="400px" width="100%" src="https://repl.it/@BillJr99/PythonWeatherClient?lite=true" scrolling="no" frameborder="no" allowtransparency="true" allowfullscreen="true" sandbox="allow-forms allow-pointer-lock allow-popups allow-same-origin allow-scripts allow-modals"></iframe>  
    - model: |
        <div align="left">
        <pre>
        <code>
        {
            "response": {
                "version": "0.1",
                "termsofService": "http://www.wunderground.com/weather/api/d/terms.html",
                "features": {
                    "conditions": 1
                }
            },
            "current_observation": {
                "image": {
                    "url": "http://icons-ak.wxug.com/graphics/wu2/logo_130x80.png",
                    "title": "Weather Underground",
                    "link": "http://www.wunderground.com"
                },
                "display_location": {
                    "city": "Philadelphia",
                    "state": "PA",
                    "zip": "19104",
                    "latitude": "39.96150970",
                    "longitude": "-75.19716644",
                    "elevation": "41.00000000"
                },
                "observation_location": {
                    "full": "University City - West Philadelphia, Philadelphia, Pennsylvania",
                    "city": "University City - West Philadelphia, Philadelphia",
                    "state": "Pennsylvania",
                    "latitude": "39.950554",
                    "longitude": "-75.211868",
                    "elevation": "70 ft"
                },
              "temp_f": 76.5,      
            }
        }
        </code>
        <pre>
        </div>
      title: A Sample JSON Response
      questions:
        - "What is the path to <code>longitude</code>?"
        - "What is the path to <code>temp_f</code>?"
    - model: |
        <script type="syntaxhighlighter" class="brush: python"><![CDATA[        
        f = open("somepath.txt", "a+") # a+ for append to the end, w for overwrite
        
        f.write("This is a test")
        
        data = f.read() # can provide the number of bytes
        
        lines = data.split("\n")
        words = data.split()
        
        f.close()
        ]]></script> 
      title: Basic File Reading
      questions:
        - "Modify this program to read a comma separated value, and for each row, print every column individually via a loop (so that they print without the commas!)."
      embed: |
        <iframe height="400px" width="100%" src="https://repl.it/@BillJr99/PythonFileIO?lite=true" scrolling="no" frameborder="no" allowtransparency="true" allowfullscreen="true" sandbox="allow-forms allow-pointer-lock allow-popups allow-same-origin allow-scripts allow-modals"></iframe>         
        
tags:
  - files 
  
---

## Data Representation

Before delving into managing data, it is essential to understand how data is represented. In computers, data is typically represented using binary digits (bits), which are either 0s or 1s. Binary representation allows computers to store and process data efficiently. However, for humans to work with data, we often use higher-level abstractions such as characters, numbers, and text.

To represent characters and text within computers, several encoding schemes have been developed. The most widely used encoding scheme is ASCII (American Standard Code for Information Interchange), which assigns a unique numerical value to each character. For example, the character 'A' is represented by the ASCII value 65.

Modern encoding schemes, such as Unicode, have expanded on ASCII and provide a comprehensive set of characters covering various writing systems and languages. Unicode allows the representation of characters from different scripts, including Latin, Cyrillic, Chinese, and others.

Python provides built-in support for working with different encodings and manipulating text data. The `ord()` function can be used to obtain the Unicode code point of a character, while the `chr()` function converts a Unicode code point to its corresponding character. Here is an example:

```python
# ASCII value of 'A'
ascii_value = ord('A')
print(ascii_value)  # Output: 65

# Character corresponding to Unicode code point 65
character = chr(65)
print(character)  # Output: A
```

Further reading: 
- [ASCII - Wikipedia](https://en.wikipedia.org/wiki/ASCII)
- [Unicode - Wikipedia](https://en.wikipedia.org/wiki/Unicode)

---

## Text Encoding and Decoding

When working with text data, it is crucial to be aware of the encoding used to represent the text. Different encoding schemes can lead to incorrect interpretation or loss of information if not handled correctly. Therefore, the ability to encode and decode text is essential.

In Python, the `encode()` and `decode()` methods can be used to convert text between different encodings. The encoding argument specifies the desired encoding while decoding or encoding the text. Here is an example that demonstrates encoding and decoding using the UTF-8 encoding:

```python
text = 'Hello, World!'

# Encoding text to UTF-8
encoded_text = text.encode('utf-8')
print(encoded_text)  # Output: b'Hello, World!'

# Decoding UTF-8 text
decoded_text = encoded_text.decode('utf-8')
print(decoded_text)  # Output: Hello, World!
```

It is important to note that when reading or writing text files in Python, it is necessary to specify the appropriate encoding explicitly. Failure to do so may result in text corruption or misinterpretation. The `open()` function in Python provides an `encoding` parameter that can be used to specify the desired encoding for file operations.

Further reading:
- [Unicode Transformation Formats - Python documentation](https://docs.python.org/3/library/codecs.html#standard-encodings)

---

## File I/O Primer

### Introduction

File I/O, or Input/Output, is an essential concept in programming that allows us to read data from and write data to files. Being able to work with files is crucial for many tasks, such as loading external data, managing configurations, logging information, and storing results.

In this primer, we will discuss the basic operations involved in file I/O, as well as provide examples in Python to illustrate the concepts.

### File Modes

When opening a file, we need to specify the mode for opening it, which determines whether we want to read, write, or append to the file. The following are the most common file modes:

- **"r"**: Read mode. Opens the file for reading (default).
- **"w"**: Write mode. Opens the file for writing. Creates a new file if it doesn't exist or truncates the file if it exists.
- **"a"**: Append mode. Opens the file for appending. Creates a new file if it doesn't exist.
- **"x"**: Exclusive creation mode. Opens the file for writing, but only if it doesn't exist already.
- **"b"**: Binary mode. Opens the file in binary mode, which is used for non-text files.
- **"t"**: Text mode. Opens the file in text mode (default).

It's important to note that when opening a file, we should always close it when we are done to release the resources associated with it. This can be done using the `close()` method on the file object.

### Reading from a File

To read data from a file, we first need to open it in read mode using the `open()` function. Once the file is opened, we can use various methods to read its contents. Some common methods include:

- **`read()`**: Reads the entire content of the file as a single string.
- **`readline()`**: Reads a single line from the file and returns it as a string.
- **`readlines()`**: Reads all lines from the file and returns them as a list of strings.

Here's an example that demonstrates reading from a file in Python:

```python
# Open the file in read mode
file = open("data.txt", "r")

# Read the entire content of the file
content = file.read()
print(content)

# Close the file
file.close()
```

Python also provides a convenient way to work with files using the 'with' statement. The 'with' statement automatically takes care of closing the file object, even in case of exceptions or errors. The following example demonstrates how to read a file using the 'with' statement:

```python
# Read a file using 'with' statement
with open('example.txt', 'r') as file:
    contents = file.read()
    print(contents)
```

### Writing to a File

To write data to a file, we need to open it in write mode using the `open()` function. Once the file is opened, we can use the `write()` method to write data to it. It's important to note that the `write()` method overwrites the existing content of the file. If we want to append to the file instead, we should open it in append mode.

Here's an example that demonstrates writing to a file in Python:

```python
# Open the file in write mode
file = open("output.txt", "w")

# Write data to the file
file.write("Hello, World!")

# Close the file
file.close()
```

### File Seeking: Navigating Large Files Efficiently

When working with large files in Python, it is often inefficient to read the entire file at once, especially if you only need to access specific sections of the file. File seeking allows you to navigate through a file and read or write data at specific positions, making it a valuable technique for handling large datasets or known file formats. 

#### The `seek()` Method

Python provides the `seek()` method for file objects, which allows you to move the file's current position to a specified offset. The general syntax for `seek()` is as follows:

```python
file_object.seek(offset, whence)
```

- `offset`: It represents the number of bytes to move, relative to the `whence` parameter.
- `whence`: It specifies the reference point from where the offset is applied. It can take one of the following values:
  - `0` (default): The offset is relative to the beginning of the file.
  - `1`: The offset is relative to the current position.
  - `2`: The offset is relative to the end of the file.

#### Example: Parsing a Large CSV File

Suppose you have a large CSV file containing millions of records, and you only need to extract data from a specific section of the file. Instead of loading the entire file into memory, you can leverage file seeking to read the desired portion efficiently.

Let's say the CSV file has the following structure:

```
Name,Age,Location
John Doe,25,New York
Jane Smith,30,San Francisco
Alice Johnson,27,Chicago
... (millions of other records)
```

To extract data from the file, you can use the following steps:

1. Open the file using the `open()` function and obtain a file object.
2. Determine the start and end positions of the section you want to read, either by known offsets or specific markers within the file.
3. Use the `seek()` method to move the file's current position to the desired starting position.
4. Read the required number of bytes using the `read()` method.
5. Close the file once you have finished processing.

Here's an example implementation that demonstrates reading a specific section of a large CSV file:

```python
with open('large_file.csv', 'r') as file:
    # Seek to the desired starting position (e.g., 100 bytes into the file)
    file.seek(100)

    # Read the next 200 bytes (assuming the desired section ends there)
    data = file.read(200)

    # Process the extracted data
    # (e.g., parse the CSV data and perform relevant operations)

    print(data)  # Output or further processing
```

By utilizing file seeking, you can efficiently read and process large files without the need to load the entire file into memory, thus saving resources and improving performance.

### Additional Resources

For more in-depth information on file I/O in Python, you may find the following resources helpful:

1. Van Rossum, G., & Drake, F. L. (1995). Python tutorial. Centrum voor Wiskunde en Informatica Amsterdam, The Netherlands, Tech. Rep, 9509.

2. Beazley, D. M. (2009). Python Essential Reference. Addison-Wesley.

3. Lundh, F. (2021). Python Standard Library. File I/O. Retrieved from [File Objects - Python documentation](https://docs.python.org/3/tutorial/inputoutput.html#reading-and-writing-files)

These references provide more detailed explanations and cover advanced topics such as file handling techniques, error handling, and working with large files.

In conclusion, understanding file I/O is crucial for any programmer as it allows us to interact with external files and perform various data processing tasks. By familiarizing ourselves with the basic operations involved in file I/O, we can leverage its capabilities in our projects effectively.

---

## File Processing Techniques

Processing files efficiently often involves working with their contents line by line or in chunks rather than loading the entire file into memory. This approach is particularly useful when working with large files.

In Python, the `readline()` method can be used to read one line at a time from a file. The example below demonstrates how to read a file line by line and process the lines individually:

```python
# Read a file line by line
with open('example.txt', 'r') as file:
    for line in file:
        # Process each line
        print(line)
```

Another technique for processing files is reading or writing in chunks. Instead of reading or writing the entire file at once, data is processed in smaller chunks, which can be more memory-efficient. The following example demonstrates reading a file in chunks of 1 kilobyte:

```python
# Read a file in chunks
with open('example.txt', 'r') as file:
    while True:
        chunk = file.read(1024)  # Read 1 kilobyte at a time
        if not chunk:
            break
        # Process the chunk
        print(chunk)
```

These file processing techniques can significantly improve performance and memory usage when working with large datasets or files.

Further reading:
- [The I/O module - Python documentation](https://docs.python.org/3/tutorial/inputoutput.html#methods-of-file-objects)

### Error Handling in File I/O Operations

- Reference: Flanagan, D., & Flanagan, Y. A. (2021). Python Cookbook: Modern Recipes for Busy Developers. O'Reilly Media.

- Python Example:
```python
try:
    file = open("file.txt", "r")
    # Perform file I/O operations
    file.close()
except FileNotFoundError:
    print("File not found.")
except IOError:
    print("An I/O error occurred.")
```

### File Permissions and Access Control

- Reference: Lutz, M. (2013). Learning Python. O'Reilly Media.

- Python Example:
```python
import os

# Get current file permissions
permissions = os.stat("file.txt").st_mode
print(f"Current permissions: {permissions:o}")

# Change file permissions
os.chmod("file.txt", 0o755)
```

### Streamed File Processing

- Reference: Beazley, D. M. (2009). Python Essential Reference. Addison-Wesley Professional.

- Python Example:
```python
def process_large_file(file_path):
    with open(file_path, 'r') as large_file:
        for line in large_file:
            # Process each line
            print(line)

process_large_file("large_file.txt")
```
        
## Working with JSON in Python

JSON (JavaScript Object Notation) is a popular data format with diverse uses in data interchange, including that of web applications with servers. Python has a built-in package called `json` for encoding and decoding JSON data.

### Importing the JSON module

To work with JSON data in Python, we need to import the `json` module. This is done with the `import` statement in Python.

```python
import json
```

### Reading JSON data
To read JSON data, we use the `json.load()` or `json.loads()` methods.

#### `json.load()`
The `json.load()` method is used to read a file containing JSON object.

```python
import json

with open('data.json') as f:
    data = json.load(f)

print(data)
```

#### `json.loads()`
The `json.loads()` method is used if you have a JSON formatted string that you want to convert into a Python object.

```python
import json

json_string = '{"name": "John", "age": 30, "city": "New York"}'
data = json.loads(json_string)

print(data)
```

### Writing JSON data
To write JSON data, we use the json.dump() or json.dumps() methods.

#### `json.dump()`
The `json.dump()` method is used to write a Python object into a JSON file.

```python
import json

data = {
    "name": "John",
    "age": 30,
    "city": "New York"
}

with open('data.json', 'w') as f:
    json.dump(data, f)
```

#### `json.dumps()`
The `json.dumps()` method converts a Python object into a JSON string.

```python
import json

data = {
    "name": "John",
    "age": 30,
    "city": "New York"
}

json_string = json.dumps(data)

print(json_string)
```

### Reading JSON data into a Python dictionary
JSON data naturally translates into a Python dictionary. This is because JSON format is essentially a structured form of data that aligns well with the structure of a dictionary. When we load JSON data using the json module, it is converted into a Python dictionary.

Here's an example:

```python
import json

# JSON string
json_string = '{"name": "John", "age": 30, "city": "New York"}'

# Use json.loads() to convert JSON string to a Python dictionary
data = json.loads(json_string)

# Now data is a Python dictionary
print(type(data))  # <class 'dict'>
print(data)  # {'name': 'John', 'age': 30, 'city': 'New York'}
```

In this example, `json.loads()` is used to convert a JSON string into a Python dictionary. The resulting dictionary, data, can be used just like any other dictionary in Python. For instance, you can access the value of "name" in the JSON data with data`['name']`.

Similarly, when reading from a JSON file, the data is loaded as a dictionary:

```python
import json

# Open the JSON file
with open('data.json') as f:
    data = json.load(f)

# Now data is a Python dictionary
print(type(data))  # <class 'dict'>
```

In this case, `json.load()` is used to read the JSON file and convert it into a Python dictionary.

## Reading and Writing CSV Files

CSV (Comma-Separated Values) files are a common format for storing tabular data. While Python provides a built-in `csv` library to handle CSV files conveniently, it's essential to understand the underlying operations. In this article, we will explore how to read and write CSV files using only raw file read and write operations in Python, without relying on the `csv` library.

### Reading CSV File
To read a CSV file without using the `csv` library, we can open the file, read its contents, and process the data manually. Here's an example:

```python
filename = "data.csv"

# Open the CSV file in read mode
with open(filename, 'r') as file:
    # Read all lines from the file
    lines = file.readlines()

    # Process each line
    for line in lines:
        # Split the line into values
        values = line.strip().split(',')

        # Process the values
        for value in values:
            # Do something with the value
            print(value)
```

In the above example, we open the CSV file using the `open()` function in read mode (`'r'`). We read all lines from the file using `readlines()`. Each line is then split using the `split()` method with a comma as the delimiter. We can now process each value as desired.

### Writing to CSV File
Similarly, we can write data to a CSV file without using the `csv` library. Here's an example:

```python
filename = "output.csv"

# Sample data
data = [
    ['Name', 'Age', 'Country'],
    ['John', '25', 'USA'],
    ['Alice', '30', 'Canada'],
    ['Bob', '20', 'UK']
]

# Open the CSV file in write mode
with open(filename, 'w') as file:
    # Write data to the file
    for row in data:
        line = ','.join(row)
        file.write(line + '\n')
```

In the above example, we have a nested list `data`, representing the rows of the CSV file. We open the file in write mode (`'w'`) using `open()`. We iterate over each row and join the values with a comma using `join()`. We write each line to the file using `write()`, adding a newline character (`\n`) after each line.

### Using the `csv` Library
While reading and writing CSV files manually can be useful in some cases, Python provides a dedicated `csv` library that simplifies CSV file handling. Let's explore how to use the `csv` library with examples.

#### Reading CSV File with `csv` Library
To read a CSV file using the `csv` library, we can use the `csv.reader` class. Here's an example:

```python
import csv

filename = "data.csv"

# Open the CSV file using csv.reader
with open(filename, 'r') as file:
    # Create a csv.reader object
    reader = csv.reader(file)

    # Process each row
    for row in reader:
        # Process the values
        for value in row:
            # Do something with the value
            print(value)
```

In the above example, we import the `csv` module and open the CSV file. We create a `csv.reader` object by passing the file object to it. We can now iterate over the rows using the reader object and process the values as required.

#### Writing to CSV File with `csv` Library
To write data to a CSV file using the `csv` library, we can use the `csv.writer` class. Here's an example:

```python
import csv

filename = "output.csv"

# Sample data
data = [
    ['Name', 'Age', 'Country'],
    ['John', '25', 'USA'],
    ['Alice', '30', 'Canada'],
    ['Bob', '20', 'UK']
]

# Open the CSV file using csv.writer
with open(filename, 'w', newline='') as file:
    # Create a csv.writer object
    writer = csv.writer(file)

    # Write data to the file
    writer.writerows(data)
```

In the above example, we import the `csv` module and open the CSV file. We create a `csv.writer` object by passing the file object to it. We can now write the entire list of rows to the file using the `writerows()` method of the writer object.

## File Encoding and Character Sets

When working with text data, it's important to understand file encoding and character sets. File encoding determines how the binary data in a file is interpreted and converted into characters. Character sets, on the other hand, define the specific set of characters that can be represented.

### ASCII (American Standard Code for Information Interchange)

ASCII is one of the earliest character encoding standards and is widely used in computer systems. It represents characters using 7 bits, allowing for a total of 128 different characters. This encoding includes basic Latin letters, digits, punctuation marks, and control characters.

Advantages of ASCII:
- ASCII encoding is simple and straightforward.
- It requires less storage space compared to other encodings.
- It is compatible with most computer systems.

Python Example for Reading ASCII-encoded Data:
```python
with open('file.txt', 'r', encoding='ascii') as file:
    data = file.read()
    print(data)
```

Python Example for Writing ASCII-encoded Data:
```python
data = "Hello, ASCII!"
with open('file.txt', 'w', encoding='ascii') as file:
    file.write(data)
```

### UTF-8 (Unicode Transformation Format - 8-bit)

UTF-8 is a widely used character encoding that supports almost all characters from all scripts and languages. It can represent any character in the Unicode standard using variable-length encoding, with each character represented by 1 to 4 bytes.

Advantages of UTF-8:
- UTF-8 is backward-compatible with ASCII. ASCII characters are encoded using a single byte, making it compatible with existing ASCII-based systems.
- It can represent a vast range of characters, including characters from different languages, mathematical symbols, emojis, etc.
- It provides efficient storage as it uses variable-length encoding.

Python Example for Reading UTF-8-encoded Data:
```python
with open('file.txt', 'r', encoding='utf-8') as file:
    data = file.read()
    print(data)
```

Python Example for Writing UTF-8-encoded Data:
```python
data = "Hello, UTF-8!"
with open('file.txt', 'w', encoding='utf-8') as file:
    file.write(data)
```

### UTF-16 (Unicode Transformation Format - 16-bit)

UTF-16 is another character encoding that represents characters using either 2 or 4 bytes. It can represent all Unicode characters, including characters outside the Basic Multilingual Plane (BMP), which are represented using surrogate pairs.

Advantages of UTF-16:
- It provides a fixed-length encoding, which can simplify some text processing operations.
- It can represent characters from various scripts, including less common or historic scripts.

Python Example for Reading UTF-16-encoded Data:
```python
with open('file.txt', 'r', encoding='utf-16') as file:
    data = file.read()
    print(data)
```

Python Example for Writing UTF-16-encoded Data:
```python
data = "Hello, UTF-16!"
with open('file.txt', 'w', encoding='utf-16') as file:
    file.write(data)
```

Understanding file encoding and character sets is crucial for proper handling of text data. By selecting the appropriate encoding, you can ensure the accurate representation and compatibility of characters in your files.

## Binary File I/O

- Reference: VanderPlas, J. (2016). Python Data Science Handbook: Essential Tools for Working with Data. O'Reilly Media.

- Python Example:
```python
# Write binary data
with open("file.bin", "wb") as binary_file:
    binary_file.write(b'\x00\x01\x02\x03')

# Read binary data
with open("file.bin", "rb") as binary_file:
    data = binary_file.read()
    print(data)
```
    
### Example: File Compression and Archiving with the ZIP file format

- Reference: Ramalho, L. (2020). Fluent Python. O'Reilly Media.

- Python Example (Using `zipfile` module):
```python
import zipfile

# Compress files
with zipfile.ZipFile("archive.zip", "w") as zip_file:
    zip_file.write("file1.txt")
    zip_file.write("file2.txt")

# Extract files from archive
with zipfile.ZipFile("archive.zip", "r") as zip_file:
    zip_file.extractall("extracted_files")
```    

Using the `zipfile` library, we can read and write zip files using its binary format.  But let's explore how to read binary data from a zip file using Python's raw file read/write operations. We will focus on extracting the header information and the list of files contained within the zip file.

We can learn about the binary format of a zip file by reviewing the [ZIP file format specification](https://pkware.cachefly.net/webdocs/casestudies/APPNOTE.TXT) provided by PKWARE. It contains detailed information about the structure and components of ZIP files, which we will use below.

#### Reading the Zip File Header
The header of a zip file contains metadata about the file, such as the version, compression method, and file entry information. Let's see how we can read this information using Python:

```python
# Open the zip file in binary mode
with open('example.zip', 'rb') as file:
    # Read the first 30 bytes of the file
    header_data = file.read(30)

# Extract the relevant information from the header data
version = header_data[4:6]
compression_method = header_data[6:8]
# ... (Extract other relevant information)

# Print the extracted information
print(f"Version: {version}")
print(f"Compression Method: {compression_method}")
# ... (Print other extracted information)
```

In the above code, we open the zip file in binary mode using the `open()` function and read the first 30 bytes of the file. We then extract the relevant information from the header data using slicing operations. Finally, we print the extracted information.

#### Reading the List of Files in a Zip File
After reading the header, we can move on to extracting the list of files present in the zip file. Each file entry in a zip file has its own header, which contains information about the file name, file size, and other attributes. Here's how we can read the list of files:

```python
# Open the zip file in binary mode
with open('example.zip', 'rb') as file:
    # Read the header to determine the start of the file entries
    header_data = file.read(30)
    central_directory_offset = int.from_bytes(header_data[16:20], byteorder='little')

    # Seek to the start of the central directory
    file.seek(central_directory_offset)

    # Read the central directory and extract file entries
    while file.read(4) == b'PK\x01\x02':
        # Read the file entry data
        file_entry_data = file.read(46)

        # Extract relevant information from the file entry data
        file_name = file_entry_data[28:30]
        file_size = int.from_bytes(file_entry_data[18:22], byteorder='little')
        # ... (Extract other relevant information)

        # Print the extracted information
        print(f"File Name: {file_name}")
        print(f"File Size: {file_size}")
        # ... (Print other extracted information)
```

In the above code, we first read the header to determine the start offset of the central directory. We then seek to that offset using the `seek()` method. After that, we iterate through the central directory entries by checking for the signature bytes 'PK\x01\x02'. For each file entry, we read the relevant data and extract the required information.

By using Python's raw file read/write operations, we can read binary data from popular file formats like zip files. In this article, we explored how to read the header information and extract the list of files from a zip file. Remember to handle errors and edge cases appropriately when working with binary data.