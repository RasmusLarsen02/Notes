
How do we define the quality of some database? 

How do we ensure integrity of the data 

How do we ensure good performance?


## Bad database design

![[Pasted image 20241007121917.png]]

Tables that contain redundant and non entity specific data can create problems on insertions, deletions and updates 
Say if we wanted to create a student that isn't related to a course then those values would be null. 
Or if we wanted to delete a student we are also deleting the course information 
Or if we wanted to update the room than we risk corrupting the data if not careful. 

**Decomposition** can fix many of these issues by separating repeated data into their own tables 
![[Pasted image 20241007122826.png]]


## functional dependencies

if attributes define some other attributes.  They are defined from the database schema not the values of individual entries in the tables. FDs allows us to quantify the quality of the database and evaluate the design of the relationship. You can use them with the **Normal Forms**, which are defined from the functional dependencies. 


## Normal Forms 

Ensures that the database doesn't contain certain well known issues they are segregated into different title that get progressively more restrictive 


* First Normal Form (1NF)
"All attributes are of atomic forms" meaning that no attributes should be lists or sets, such as first & last name being under "name" or a attribute containing some list of emails for the user. This can be fixed by decomposing the table by keeping track of the emails in a separate table. 

* Second Normal Form (2NF)
Values should follow 1NF **AND** attributes should **fully** depend on the whole candidate key or keys

![[Pasted image 20241007125010.png]]

* Third Normal Form (3NF)
All functional dependencies for some relation.  If A is a subset of X meaning it is a trivial functional dependency or X contains some key for the Relation R or A is part of some key. 

![[Pasted image 20241007125346.png]]

* Boyce-Codd Normal From (BCNF)
IF looking at all functional dependencies. They should either be trivial or the X should contain the key for R 


## Algorithm for Decomposition 

1. Find all FDS
2. While FD < 3NF : Decompose 

Will result in either 3NF or BCNF 


**Example 1**
**AB**CD 

AB -> C
C -> D

This is in 2NF  because of transitivity 

can be decomposed to 
**AB**C
**C**D

Now it is in BCNF because all attributes are only dependent on primary keys. 