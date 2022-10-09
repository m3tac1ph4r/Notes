# Indexing :



1. Indexing is used to **optimise the performance** of a database by minimising the number of disk accesses required when a query is processed.
2. The index is a type of **data structure**. It is used to locate and access the data in a database table quickly.
3. **Speed up operations** with read operations like *SELECT* queries, *WHERE* clause etc.
4. **Search Key :** Contains copy of primary key or candidate key of the table or something else.
5. **Data Reference :** Pointer holding the address of disk block where the value of the corresponding key is stored.
6. Indexing is *optional*, but increases access speed. It is not the primary mean to access the tuple, it is secondary mean.
7. **Index file is always sorted.**


### Indexing Methods :

##### 1. Primary Indexing (Clustering Indexing) :
1. A file may have several indices, on different search keys. If the data file containing the records is sequentially ordered, a Primary index is an index whose search key also defines the sequential order of the file.
2. All files are ordered sequentially on some search keys. It could be Primary key or non primary key.

###### Types of Primary Indexing :

**1. Dense Index :** 
1. The dense index contains an index record for every search key value in the data file.
2. The index record contains the search-key value would be stored sequentially after the first record.
3. It needs more space to store index record itself. The index records have the search key and a pointer to the actual record on the disk.

![[dense_indexing.png]]


**2. Sparse Index :**
1. It is an index record that appears for only some of the values in the file. Sparse Index helps you to resolve the issues of dense Indexing in DBMS. In this method of indexing technique, a range of index columns stores the same data block address, and when data needs to be retrieved, the block address will be fetched.
2. However, sparse Index stores index records for only some search-key values. It needs less space, less maintenance overhead for insertion, and deletions but It is slower compared to the dense Index for locating records.
![[sparse_indexing.png]]

**3. Based on Key attribute :**
1. Data file is stored w.r.t primary key attribute.
2. PK will be used as search-key in index.
3. Sparse index will be formed i.e, number of entries in the index file= number of blocks in datafile.

**3. Based on Non-Key attribute :**
1. Data file is sorted w.r.t non-key atttribute.
2. Number of enteries= unique non-key attributes value in the data file.
3. This is dense index, as all the unique value will have an entry in the index file.
4. E.g., Let's assume that a company recruited many employees in various departments. In this case, clustering indexing in DBMS should be created for all employees who belong to the same dept.

![[non_key_indexing.png]]

##### 2. Multi-level Indexing  :
1. Index with two or more levels.
2. Multilevel Indexing in Database is created when a primary index does not fit in memory. In this type of indexing method, you can reduce the number of disk accesses to short any record and kept on a disk as a sequential file and create a sparse base on that file. 

![[multiLevel_Indexing.png]]

##### 3. Secondary Indexing :
1. Datafile is unsorted. Hence, Primary Indexing is not possible.
2. Can be done on key, non-key attribute.
3. Called secondary indexing because normally one indexing is already applied
4. No. of entries in the index file= number of records in the data file.
5. It's an example of Dense Index.
6. In secondary Indexing the data will be unsorted but the data which we will be using for Indexing will be sorted in indexing table. 
    Ex: In main file the search_key is unsorted and in indexing it is sorted. So we can apply binary search in indexing and it will get the result faster.

![[secondary_Indexing_Ex1.png]]

![[secondary_Indexing_1.png]]


We can also store the difference occurence of key using linkedlist in indexing table if data is unsorted.

![[secondary_Indexing_2.png]]


### Advantages of Indexing :

1. It helps to reduce the total number of I/O operations needed to retrieve that data.
2. Offers faster search and retreival of data to users.
3. Indexing also helps you to reduce

### Disadvantages of Indexing :
1. To perform the indexing database management system, you need a primary key on the table with a unique value.
2. SQL Indexing Decrease performance in INSERT, DELETE, and UPDATE query.


