
https://www.markdownguide.org/cheat-sheet/
## Introduction



## Lecture 1

### Data Base Management Systems (DBMS)

Databases are managed in a three-layer architecture meaning that there exists a Data Tier, a Logic Tier and a presentation tier. In the data tier the data itself is stored, in the logic tier the applications and processes are coordinated and in the presentation tier the formatted data is presented to the users. 

Databases help increase data consistency. They are collections of related data items. The way you manage and organize the data is called the Database system. The database management system is thus a way to both store and organize data points in an efficient maintainable ad concurrent way. 

**Relational Databases** are databases based on the relational model. Their store a set of tables with rows and columns (relations) and uses the relations between these to manage the data. The implementation and management of the relational database is done through the Relational Database management system (RDBMS). 

### Relational Model

Relations are tables containing rows and columns. The columns are the attributes of the table and the rows or tuples are the records or values. The Schema of a relation contains the attributes and name of the relation. 
![[Pasted image 20240902125143.png]]

Instances of the Schema are records in the relation so the rows in the table like (Blue Mountain, Marley Coffee)

**A Database** is a collection of tables or relations. The Schema of a Database is the set of all relation names in the database. A database instance is the set of all relations instances in the database. 

Relations are good for organizing and managing structured data. It is also the model behind SQL which is the most used querying language used currently. They are however too simple for unstructured data which is a lot of the data being generated today, this would mean a complex implementation for representing these data formats. 

The relations need a identifying column or attribute such as an id or other markers.

**Keys**
Keys are groups of identifiers that allows to identify a single record or row in the relation. This could be the CPR number for identifying people in Denmark. 

**Superkeys** are a set of attributes that uniquely identifiers records. **Minimal Superkeys** are keys where no attribute can be removed without violating the uniqueness property of the Superkey.

**Candidate Keys** are keys that satisfy uniqueness and minimality property that key is a minimal superkey. Superkeys contains at least one candidate key. Relations can have many candidate keys.

**Primary keys** is a single of the candidate keys that is chosen from the set of possible candidate keys. They cannot be null and are used to establish relations to other relations in the database. The remaining keys in the set are know as the **Alternative keys** 

**Relationships** linking together tables using keys. The reduces redundancy in the database, because the instances of the unique datapoints can be stored in different tables thus decoupling the tables but have good relations between the tables. 

**Foreign key** a foreign key is a primary key of a another table. Foreign keys values exist in some other record, they can be null. A relation can have more than one foreign keys. 

![[Pasted image 20240902133514.png]]

![[Pasted image 20240902133533.png]]


**Integrity Constraints** are limitations of the allowed content in the tables. This ensures correctness and consistency in the database. 

### Structured Query Language - Sequel (SQL)
A querying language to retrieve data from databases. Contains ways to define data bases using data definition language (DDL) (CREATE TABLE; ALTER TABLE; DROP TABLE)

**Data Definition Language (DDL)** Follows first normal form (1NF) that each attribute in a relation is a primitive type and has a unique name. The goal of this is to reduce redundancy in the databases. 

A table can be created: 

CREATE TABLE students ( SID INT PRIMARY KEY, Name VARCHAR(255), Email Char(11), Semester INT); 

In the creating foreign keys and primary keys can be defined in the creation process. 

**Multiple-Attribute Primary Keys**
Students ( SID : INT, Name : STRING, Email : STRING, Semester : INT) 
Courses ( CID : STRING, Name : STRING, DID : INT) 
Transcripts ( CID : STRING, SID : INT, Grade : STRING, Comment : STRING) 

CREATE TABLE 
Transcripts ( 
CID VARCHAR(25), 
SID INT, Grade INT, 
Comment VARCHAR(255), 
PRIMARY KEY (CID, SID), 
FOREIGN KEY (CID) REFERENCES Courses (CID), 
FOREIGN KEY (SID) REFERENCES Students (SID) 
);

You are on allowed to drop tables that contains references to other tables while those reference tables still exist. 

**Data manipulation language (DML)** 


