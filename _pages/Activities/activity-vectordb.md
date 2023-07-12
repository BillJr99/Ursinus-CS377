---
layout: activity
permalink: /Activities/VectorDB
title: "CS377: Database Design - Vector Databases"
excerpt: "CS377: Database Design - Vector Databases"

info:
  goals: 
    - To explain the benefits of a Vector Database approach
    - To explore applications of Vector Databases including Large Language Models
    
  models:
    - model: |
        <p>consider a scenario where we have a database of restaurants, and each restaurant is represented by a vector that encodes various features such as cuisine type, price range, location, etc. We can use a vector database to perform efficient similarity searches, such as finding restaurants that are similar to a given restaurant.</p>
        <script type="syntaxhighlighter" class="brush: python"><![CDATA[    
        import vecs

        DB_CONNECTION = "postgresql://<user>:<password>@<host>:<port>/<db_name>"

        # create vector store client
        vx = vecs.create_client(DB_CONNECTION)

        # Create a collection to store vectors specifying the collections name and the number of dimensions in the vectors you intend to store.
        restaurants = vx.create_collection(name="restaurants", dimension=7)  # assuming we have 7 features

        # To access a previously created collection, use `get_collection` to retrieve it by name
        restaurants = vx.get_collection(name="restaurants")

        # `vecs` combines the concepts of "insert" and "update" into "upsert". Upserting records adds them to the collection if the `id` is not present, or updates the existing record if the `id` does exist.
        # add records to the collection
        restaurants.upsert(
            vectors=[
                # your vectors here, each vector is a list of 7 numbers representing the features of a restaurant
                # The first number is the price range, the next three numbers represent the cuisine type, the fifth number is the rating, the sixth number indicates whether the restaurant is vegetarian-friendly, and the seventh number indicates whether the restaurant has outdoor seating.
                [0.5, 1, 0, 0, 0.8, 1, 0],  # a mid-priced Italian restaurant with good ratings, vegetarian-friendly, with outdoor seating
                [0.2, 0, 1, 0, 0.6, 0, 1],  # an inexpensive Chinese restaurant with medium ratings, not vegetarian-friendly, with outdoor seating
                [0.7, 0, 0, 1, 0.9, 1, 1],  # an expensive Mexican restaurant with excellent ratings, vegetarian-friendly, with no outdoor seating
            ],
            ids=[
                # your ids here, each id is a unique identifier for a restaurant
                "restaurant_1",
                "restaurant_2",
                "restaurant_3",                
            ],
            metadata=[
                # your metadata here, each metadata is a dictionary containing additional information about a restaurant
                {"name": "Italian Restaurant", "location": "123 Main St"},
                {"name": "Chinese Restaurant", "location": "456 Oak St"},
                {"name": "Mexican Restaurant", "location": "789 Pine St"},                
            ]
        )

        # Now, let's say we have a user's cuisine preference represented as a vector
        user_pref_vector = [0.3, 1, 1, 1, 0.9, 0, 1]  # this should be generated based on the user's preferences

        # We can find the top 5 restaurants that are most similar to the user's preference
        results = restaurants.search(query_vectors=[user_pref_vector], top_k=5)

        for result in results:
            print(f"Restaurant ID: {result.id}, Score: {result.score}")
        
        ]]></script>
      title: Vector Database Design
      questions:
        - "What do you think the values within the <code>user_pref_vector</code> represent?"
        - "Given a set of similar vectors in the <code>restaurants</code> collection, what kind of math might you perform to find restaurants most similar to the user's preferences given the <code>user_pref_vector</code>?"
        - "Given the user preference vector, what restaurant would you recommend?"
        - "Why might this data storage and query technique be advantageous over traditional text-based search methods?"
        - "What are the operational tradeoffs to this approach?  In other words, what are the challenges we must manage?"
        
tags:
  - vector
  
---

## Vector Databases
A vector database is a type of database that is designed to store, manage, and query vector data. Vector data is a representation of points, lines, and polygons on a two-dimensional plane, commonly used in geographic information systems (GIS) and computer graphics.

In this course, we will explore the fundamentals of vector databases, including the data model, storage mechanisms, indexing techniques, and query optimization strategies.

### Data Model
The data model used in vector databases is based on the concept of vector geometry. It represents spatial objects as points, lines, and polygons. Points are defined by their x and y coordinates, lines by a series of connected points, and polygons by a closed loop of line segments.

One popular data model for vector databases is the Simple Feature Model, which is a standard defined by the Open Geospatial Consortium (OGC). It defines a set of geometry types (e.g., point, line string, polygon) and provides a standard way to represent and query spatial data.

### Storage Mechanisms
Vector databases employ various storage mechanisms to efficiently store and retrieve spatial data. Some of the commonly used storage mechanisms are:

1. **Flat Files**: Simplest form of storage where data is stored as a text file, with each line representing a spatial object. This approach is limited in terms of efficient querying and data management.

2. **RDBMS**: Relational Database Management Systems (RDBMS) such as PostgreSQL with PostGIS extension provide enhanced support for spatial data types, indexing, and querying. It allows for the integration of spatial data with non-spatial data.

3. **Spatial Indexes**: To optimize spatial queries, vector databases employ spatial indexing techniques such as R-trees, Quad-trees, and Grids. These indexes partition the spatial data into a hierarchical structure, enabling efficient querying based on spatial relationships.

#### Underlying Storage

In a PostgreSQL database, vector data can be stored in several ways depending on the specific use case and the extensions used. Here are a few common methods:

- ***Array Data Type***: PostgreSQL has built-in support for arrays. A vector can be stored as an array of numbers. This is a simple and straightforward method, but it does not support advanced vector operations.

- ***PostGIS Extension***: For geographical vector data, the PostGIS extension provides a set of types and functions that can be used to store and query geographical vectors.

- ***Cube Extension***: The cube data type can be used to represent multidimensional cubes or, in other words, vectors. The cube extension provides a number of functions and operators for working with cubes.

- ***Custom Extensions***: There are also custom PostgreSQL extensions designed specifically for working with vectors. For example, the FAISS extension for PostgreSQL allows you to perform efficient similarity search on vectors.

In the case of the vecs library mentioned in the previous examples, it uses the cube extension for storing vectors and the `pg_trgm` extension for text search. The vectors are stored as cube type in a column, and each vector can be associated with an ID and metadata.

Please note that while PostgreSQL and its extensions provide the capability to store and perform operations on vectors, they do not provide the same level of functionality as a dedicated vector database or a vector search library like FAISS. For advanced vector operations, you would typically use a specialized tool or library.  We are using an RDBMS example here to show how this approach can be used with database engines that you are already familiar with.

### Querying a Vector Database
A vector database stores data in a high-dimensional space, where each data point is represented as a vector. When you perform a query on a vector database, you're essentially asking the database to find the vectors that are most similar to your query vector. This is typically done using a measure of vector similarity, such as cosine similarity or Euclidean distance.

The process usually involves the following steps:

1. ***Vectorization***: The query is converted into a vector using the same process that was used to convert the original data into vectors. This could involve a variety of techniques, such as one-hot encoding, word embeddings, or more complex machine learning models.

2. ***Similarity Search***: The vectorized query is compared to all vectors in the database to calculate a similarity score. This score represents how similar the query vector is to each database vector.

Here is an example of how these similarity scores might be calculated (using cosine similarity):

```python
import numpy as np
from sklearn.metrics.pairwise import cosine_similarity

def find_nearest_vector(vectors, target_vector):
    cosine_similarities = cosine_similarity(vectors, target_vector.reshape(1, -1))
    nearest_index = np.argmax(cosine_similarities)
    nearest_vector = vectors[nearest_index]
    return nearest_vector

# Example usage
vectors = np.array([[1, 2, 3], [4, 5, 6], [7, 8, 9]]) # the collection of vectors
target_vector = np.array([2, 4, 6]) # the user preference vector for which we are seeking a nearest match in the collection

nearest_vector = find_nearest_vector(vectors, target_vector)
print("Nearest vector:", nearest_vector)
```

In this program, we use the `cosine_similarity` function from the `sklearn.metrics.pairwise` module to calculate the cosine similarity between each vector in the `vectors` array and the `target_vector`. The `cosine_similarity` function expects the input to be in the shape `(n_samples, n_features)`, so we reshape the `target_vector` using `reshape(1, -1)`.

The `cosine_similarity` function returns a similarity matrix with shape `(n_samples, 1)`, where each element represents the cosine similarity between the corresponding vector and the target vector. We then find the index of the vector with the highest cosine similarity using `np.argmax`.

Finally, we retrieve the nearest vector using the index found and return it as the result.

3. ***Ranking***: The vectors in the database are ranked based on their similarity scores, and the top K vectors are selected. These are the vectors that are most similar to the query vector.

4. ***Retrieval***: The data associated with the top K vectors is retrieved and returned as the result of the query.

### Vector Databases and Large Language Models (LLM)
Large language models like GPT-3 or BERT can be thought of as a kind of vector database. When the model is trained, it learns to represent words, phrases, or entire sentences as high-dimensional vectors. These vectors capture the semantic meaning of the text.

When you ask a large language model a question, it vectorizes your question and compares it to the vectors it has learned during training. It then generates a response based on the vectors that are most similar to your query vector.

However, it's important to note that large language models don't explicitly store all the vectors they generate during training. Instead, they learn a function that can generate a vector for any given input. This allows them to work with a virtually unlimited amount of data, as they don't need to store a vector for every possible input.

In some cases, large language models can be combined with vector databases to create more powerful systems. For example, a language model could be used to vectorize text data, which is then stored in a vector database. This allows for efficient similarity search on large text datasets, which can be useful for applications like information retrieval, recommendation systems, or question answering.

### Challenges in Vector Databases
Vector databases come with several challenges when dealing with large-scale spatial data:

1. **Data Volume**: Spatial data can be massive, especially when dealing with high-resolution datasets. Ensuring efficient storage and query performance becomes critical.

2. **Indexing**: Choosing the appropriate index structure and optimizing index performance is important for efficient spatial querying.

3. **Query Optimization**: Optimizing query planning and execution is crucial to handle complex spatial queries involving multiple spatial conditions.

### Scaling for Efficiency
When searching a large vector database, calculating the similarity vectors for all vectors in the database can be computationally expensive and time-consuming. To scale the calculation, you can use approximate nearest neighbor (ANN) algorithms or dimensionality reduction techniques. Here are two common approaches:

1. **Approximate Nearest Neighbor (ANN) Search:** ANN algorithms provide an efficient way to find approximate nearest neighbors, sacrificing some accuracy for faster retrieval. These algorithms, such as Locality-Sensitive Hashing (LSH) and k-d trees, can significantly speed up the search process for large vector databases. They work by partitioning the vector space into smaller regions, allowing for quick elimination of large portions of the database without calculating the exact similarity for every vector.

Here is an example of ANN Search using the annoy library:

```python
from annoy import AnnoyIndex

# Example data
vectors = [[1, 2, 3], [4, 5, 6], [7, 8, 9], [10, 11, 12]]

# Build the Annoy index
annoy_index = AnnoyIndex(len(vectors[0]), 'euclidean')
for i, vec in enumerate(vectors):
    annoy_index.add_item(i, vec)
annoy_index.build(10)  # Number of trees in the index

# Query for the nearest neighbors
query_vector = [3, 4, 5]
nearest_indexes = annoy_index.get_nns_by_vector(query_vector, n=2)

# Retrieve the nearest vectors
nearest_vectors = [vectors[i] for i in nearest_indexes]

print("Nearest vectors:", nearest_vectors)
```

2. **Dimensionality Reduction:** Another approach is to reduce the dimensionality of the vectors before calculating the similarity. Dimensionality reduction techniques, like Principal Component Analysis (PCA) or t-distributed Stochastic Neighbor Embedding (t-SNE), can transform high-dimensional vectors into lower-dimensional representations while preserving their structure and similarity relationships. By operating on the reduced-dimensional space, the similarity calculations become more efficient.

These approaches can be combined to further improve the efficiency. For example, you can first apply dimensionality reduction to reduce the vector space's dimensionality and then use an ANN algorithm to perform fast approximate nearest neighbor search.  By utilizing ANN algorithms or dimensionality reduction techniques, you can scale the calculation of similarity vectors and perform efficient searches on large vector databases.

Here is an example of Dimensionality Reduction using PCA:

For Dimensionality Reduction using PCA:

```python
import numpy as np
from sklearn.decomposition import PCA

# Example data
vectors = np.array([[1, 2, 3], [4, 5, 6], [7, 8, 9], [10, 11, 12]])

# Dimensionality reduction using PCA
pca = PCA(n_components=2)
reduced_vectors = pca.fit_transform(vectors)

print("Original vectors:")
print(vectors)
print("Reduced vectors:")
print(reduced_vectors)
```

## References

1. Worboys, Michael F., and Matt Duckham. "GIS: a computing perspective." CRC Press, 2015. [Link](https://www.crcpress.com/GIS-A-Computing-Perspective/Worboys-Duckham/p/book/9781482215891)

2. OGC Simple Feature Specification. [Link](https://www.opengeospatial.org/standards/sfa)

3. PostGIS Documentation. [Link](https://postgis.net/documentation/)

4. Abdo, Wajahat et al. "A Comparative Study of Spatial Indexing Techniques in Vector Data". International Journal of Computer Applications, 2019. [PDF](https://www.ijcaonline.org/archives/volume181/number35/abdo-2019-ijca-920724.pdf)