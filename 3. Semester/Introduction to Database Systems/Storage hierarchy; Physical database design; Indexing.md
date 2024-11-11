
## Storage Hierarchy 

Different types of storage have different access times and expenses 
![[Pasted image 20241021121710.png]]

Volatile storage looses data when disconnected and is addresses byte-wise, while Non-Volatile storage remains stable even when turned off, it is also addressed in blocks which are made up of multiple bytes.

Non Volatile storage is referred to as Disk-Storage in this course. 

It is almost always better to access data sequentially since it provides security in ensuring that the correct data is accessed with the highest probability. 

The design goals are to 
allow the databases to manage more data that is available on the main memory 
the database should behave like the data is available in main memory
the database should maximize sequential access to the database 

On the PC the databases are stored as one or more files on the disk and proprietary software is responsible for maintaining the files within the database. The **Storage Manger** tracks read/write operations aswell as the available space. 
The database files may be broken down into smaller **Pages** which are then stored on disk. 

A page is a fixed size of data, which can contain meta-data, indexes, log records and more. Typically multiple tables are not stored on a single page. So each page contains only one type of data. Some systems require pages to be self, contained. Pages have unique identifiers such that the DBMS can map page ID's to the physical position in storage. 



## Indexing

**Full Table Scans**
Are queries where all the tuples of the relation are scanned 

**Selective Queries**
Are queries which do not read every tuple in the relation. This can be effective if only a small percentage of the tuples within the relation are needed in order to answer the query. 

**Point Queries**
Are Queries that are looking for exactly one value. These can of course return more than one tuple. 
They are faster to do if the data is sorted by the attribute used then binary search can be used to speed up the lookup time. 

**Range Queries**
Are queries that look for tuples which are between two values. These are also easy on sorted data sets. 

Database indexes are pointers to specific parts of the database which help speed up lookup time into the database. Some index references some set of the database records. 
![[Pasted image 20241021125631.png]]

### Techniques for Indexing 
Indexes are an implementation of the symbol table data structure. 

**Tree Based Indexing**
Tree based indexing works around a dynamic search structure which is updated upon insertion in to the database. The Tree is used to navigate the database. This is often preferred since it allows for easy implementation of range **and** point queries. 

**Hashing Based Indexing**
Converts the attribute value into some database address with a hash function. Can be good for large scale **join** operation.

### Index Storing ![[Pasted image 20241021131847.png]]
- Clusted indexing makes  point and range queries efficient since reads are sequential and minimal 
- Many DBMSs automatically build a clustered index on the primary key of each relation.
- A clustered index is sometimes referred to as a primary or sparse index.
There can only be one clustered index, because we only store one order of each relation such that the same data is not sorted according to multiple values. 


![[Pasted image 20241021132415.png]]

### Index Scan vs Full Table Scan
* Point and range queries on the attribute(s) of the clustered index are almost always best performed using an index scan. 
*  Non-clustered indexes should only be used with high selectivity queries.
![[Pasted image 20241021133145.png]]

### Covering Index

An index setup where data entries contain all queried attributes. So only by looking at the index you can answer the query. 

So if you index is mapped using all the parameters used in you queried you index is covered for that specific query. Meaning that for covered index queries it is not necessary to read from the disk directly. 

For example if you have and index of movie years and you are only looking for entries where some year is equal to some value, then it is not needed to look at anything other than the index itself. 

It doesn't matter if the index is clustered or unclustered since you are never accessing the files themselves. And thus you will never have any disk-reads with queries on covered indexes. You will still need to read the index itself, but this is also true for the other indexes. 

