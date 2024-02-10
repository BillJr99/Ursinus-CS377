---
layout: assignment
permalink: /Assignments/VectorDB
title: "CS377: Database Design - Vector Databases"


info:
  coursenum: CS377
  points: 100
  goals:
    - To implement a program to create and populate a vector database using fundamental programming constructs and a flat file data store
  rubric:
    - weight: 60
      description: Algorithm Implementation
      preemerging: The algorithm fails on the test inputs due to major issues, or the program fails to compile and/or run
      beginning: The algorithm fails on the test inputs due to one or more minor issues
      progressing: The algorithm is implemented to solve the problem correctly according to given test inputs, but would fail if executed in a general case due to a minor issue or omission in the algorithm design or implementation
      proficient: A reasonable algorithm is implemented to solve the problem which correctly solves the problem according to the given test inputs, and would be reasonably expected to solve the problem in the general case
    - weight: 30
      description: Code Quality and Documentation
      preemerging: Code commenting and structure are absent, or code structure departs significantly from best practice, and/or the code departs significantly from the style guide
      beginning: Code commenting and structure is limited in ways that reduce the readability of the program, and/or there are minor departures from the style guide
      progressing: Code documentation is present that re-states the explicit code definitions, and/or code is written that mostly adheres to the style guide
      proficient: Code is documented at non-trivial points in a manner that enhances the readability of the program, and code is written according to the style guide
    - weight: 10
      description: Writeup and Submission
      preemerging: An incomplete submission is provided
      beginning: The program is submitted, but not according to the directions in one or more ways (for example, because it is lacking a readme writeup or missing answers to written questions)
      progressing: The program is submitted according to the directions with a minor omission or correction needed, including a readme writeup describing the solution and answering nearly all questions posed in the instructions
      proficient: The program is submitted according to the directions, including a readme writeup describing the solution and answering all questions posed in the instructions
  readings:
    - rtitle: "Vector Databases"
      rlink: "../Activities/VectorDB"
      
tags:
  - vector
  - programming
  
---

In this assignment, you will create and use a vector database for an application domain of your choosing, and use it to make recommendations by finding nearest neighbors to your query vector of features.

## Using a Flat File to Store Vector Data

You can use a database, grid, or other structure to store vector data; however, for simplicity, we will use a flat file using the `json` library in Python.  Flat files are not efficient for storage or retrieval, but will simplify our programming.  We will discuss methods to more efficiently store and search data during the course.

The following `Collection` class will simulate a database of vector data by creating an array of dictionary objects; each dictionary will contain the vector of features.  The dimension of the collection is equal to the length of the features vector (in other words, if each item in the collection has 7 features, then the dimension of the collection is 7).

```python
import numpy as np
from sklearn.metrics.pairwise import cosine_similarity
import json

class Collection:     
    def __init__(self, name, dimension):
        self.name = name
        self.dimension = dimension
        self.data = []
        
    def upsert(self, vectors, ids, metadata):
        for vector, id_, meta in zip(vectors, ids, metadata):
            # find index if id already exists
            index = next((index for (index, d) in enumerate(self.data) if d['id'] == id_), None)
            if index is None:
                # insert new item
                self.data.append({'id': id_, 'vector': vector, 'metadata': meta})
            else:
                # update existing item
                self.data[index]['vector'] = vector
                self.data[index]['metadata'] = meta
 
    def search(self, query_vectors, top_k):
        query_vectors = np.array(query_vectors)
        db_vectors = np.array([d['vector'] for d in self.data])
        scores = cosine_similarity(query_vectors, db_vectors)
        top_indices = scores.argsort()[0][::-1][:top_k]

        # return a list of objects representing the ID and score of each item in the search result
        class DictObj(object):
          def __init__(self, _id, _score):
            self.id = _id
            self.score = _score
            
        return [DictObj(self.data[i]['id'], scores[0][i]) for i in top_indices]

    def save(self, filename):
        with open(f'{filename}.json', 'w') as f:
            json.dump(self.data, f)

    @classmethod
    def load(cls, filename, dimension):
        c = cls(filename, dimension)
        with open(f'{filename}.json', 'r') as f:
            c.data = json.load(f)
        return c
```

You can instantiate one of these collections as follows, and then you can call `upsert` and `search` as you normally would.

```python
restaurants = Collection(name="restaurants", dimension=7)
```

## Part 1: Porting the Restaurants Tutorial
Using the tutorial example from class, set up the restaurants example using a flat file store above, and verify that you are able to query for a given feature vector.

## Part 2: Implementing Your Own Vector Database and Making Recommendations with User Input
Be creative here!  Modify your program to use feature vectors of your choice.  You could search for videos, houses, books, or anything else that you can describe semantically using feature vectors.  Create an initial vector database of sample data by reading vector features from a CSV file with well-described headers (so that another person could create sample data for your program!).  Then, prompt the user within your program to enter their preferences, and search and return the top `k` nearest matches.

## Part 3: Improving Search Performance Using Approximate Nearest Neighbors (ANN)
Modify the `Collection` class to support ANN for increased search efficiency over using the cosine similarity metric.  Use the example from our class notes to get started with sample code demonstrating the usage of ANN via the `annoy` library in Python.

### Modifying the Flat File
To save and load this into your flat file, you can modify the `save` and `load` functions of the `Collection` class as follows:

```python
    def save(self, filename):
        self.annoy_index.save(f'{filename}.ann')
        with open(f'{filename}.json', 'w') as f:
            json.dump(self.data, f)

    @classmethod
    def load(cls, filename, dimension):
        c = cls(filename, dimension)
        c.annoy_index.load(f'{filename}.ann')
        with open(f'{filename}.json', 'r') as f:
            c.data = json.load(f)
        c.count = len(c.data)
        return c
```

### Passing the Right Input to `get_nns_by_vector`
When you call `annoy_index.get_nns_by_vector`, the `annoy` library assumes that you are passing a single vector of size `dimension`.  The `cosine_similarity` function takes a 2-dimensional array in which the first item is an array of size `dimension`.  You can simply pass `query_vectors[0]` to `annoy_index.get_nns_by_vector` instead of `query_vectors` to remedy this.

### Calculating a Score for each Nearest Neighbor
`get_nns_by_vector` does not return the scores, but you can obtain distances which you can insert into your result object for each score by calling `annoy_index.get_distance(i, j)` to get the distance between each item (`i`) in the return set of `get_nns_by_vector` and the `query_vectors[0]` input (`j`).  Since the score is inversely proportional to the distance (that is, higher distances imply a lower score), you can set the score to `1/distance` for each distance.