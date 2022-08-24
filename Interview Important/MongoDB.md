# MongoDB Interview Questions

### 1. What are some of the advantages of MongoDB?

Some advantages of MongoDB are as follows:

-   MongoDB supports field, range-based, string pattern matching type queries. for searching the data in the database 
-   MongoDB support primary and secondary index on any fields
-   MongoDB basically uses JavaScript objects in place of procedures
-   MongoDB uses a dynamic database schema

### 2. What is a Document in MongoDB?

A Document in MongoDB is an ordered set of keys with associated values. It is represented by a map, hash, or dictionary. In JavaScript, documents are represented as objects:  
`{"greeting" : "Hello world!"}`


### 3. What is a Collection in MongoDB?

A collection in MongoDB is a group of documents. If a document is the MongoDB analog of a row in a relational database, then a collection can be thought of as the analog to a table.  
Documents within a single collection can have any number of different “shapes.”, i.e. collections have dynamic schemas.   
For example, both of the following documents could be stored in a single collection:

```plaintext
{"greeting" : "Hello world!", "views": 3}
{"signoff": "Good bye"}
```


### 4. How does Scale-Out occur in MongoDB?
The document-oriented data model of MongoDB makes it easier to split data across multiple servers. Balancing and loading data across a cluster is done by MongoDB. It then redistributes documents automatically.  
  
The mongos acts as a query router, providing an interface between client applications and the sharded cluster.

### 5. What are some features of MongoDB?
-   **Indexing:** It supports generic secondary indexes and provides unique, compound, geospatial, and full-text indexing capabilities as well.
-   **Aggregation:** It provides an aggregation framework based on the concept of data processing pipelines.
-   **Special collection and index types:** It supports time-to-live (TTL) collections for data that should expire at a certain time
-   **File storage:** It supports an easy-to-use protocol for storing large files and file metadata.
-   **Sharding:** Sharding is the process of splitting data up across machines.

### 6. How do you Delete a Document?
`> db.books.deleteOne({"_id" : 3})`

### 7. How to perform queries in MongoDB?
`> db.users.find({"age" : 24})`


###  8. Explain the term “Indexing” in MongoDB.
MongoDB uses indexing in order to make the query processing more efficient. If there is no indexing, then the MongoDB must scan every document in the collection and retrieve only those documents that match the query. Indexes are special data structures that stores some information related to the documents such that it becomes easy for MongoDB to find the right data file. The indexes are order by the value of the field specified in the index.

**Syntax –**   
`db.COLLECTION_NAME.createIndex({KEY:1})`

The key determines the field on the basis of which you want to create an index and 1 (or -1) determines the order in which these indexes will be arranged(ascending or descending).

### 9. Explain the process of Sharding.
Sharding is the process of splitting data up across machines. We also use the term “partitioning” sometimes to describe this concept. We can store more data and handle more load without requiring larger or more powerful machines, by putting a subset of data on each machine.  
In the figure below, RS0 and RS1 are shards. MongoDB’s sharding allows you to create a cluster of many machines (shards) and break up a collection across them, putting a subset of data on each shard. This allows your application to grow beyond the resource limits of a standalone server or replica set.

![[sharding_mongoDB.png]]



### 10. Why you used MongoDB instead of MYSQL ?
https://medium.com/@rsk.saikrishna/when-to-use-mongodb-rather-than-mysql-d03ceff2e922

To answer the main question: “when to use MongoDB instead of MySQL?” you need to take into account your project requirements and further goals. MySQL is well-recognized for its high performance, flexibility, reliable data protection, high availability, and management ease. Proper data indexing can solve the issue with performance, facilitate interaction and ensure robustness. But if your “data is unstructured and complex, or if you can’t pre-define your schema, you’d better opt for MongoDB.” And what is more, if you need to handle a large volume of data and store it as documents — MongoDB will help you to meet the challenges.

![[mongodbVSmysql.png]]


