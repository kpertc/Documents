#data #programming-language 

SQL, Structured Query Language

Brew install SQL
```shell
brew install mysql
```

### Tutorial:

<iframe width="560" height="315" src="https://www.youtube.com/embed/HXV3zeQKqGY" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

### What is a database?

Relational database management systems -> This course -> MySQL

##### 

**Database -> Any collection of related information**

**Any collection of related information**
-   Phone Book
-   Shopping list
-   Todo list
-   Your 5 best friends
-   Facebook's User base

**Databases can be stored in different ways**
-   On Paper
-   In your mind
-   On a computer
-   This powerpoint
-   Comments Section

Computers are great at keeping track of large amounts of information

##### 

**Database Management Systems (DBMS)**

A special software program that helps users create and maintain database
-   Make it easy to manage large amounts of information
-   Handles Security
-   Backups
-   Importing/exporting data
-   Concurrency
-   Interacts with software applications
    -   Programming Languages
        

**C.R.U.D**

Create, Read, Update, Delete

##### 

**Two Types of Databases**

**Relational Databases (****SQL****)**

-   Organize data into one or more tables
    -   Each table has columns and rows
    -   A unique key identifies each row
        

![[SQL/SQL img/8f26158e-728a-4caf-8ad4-c4e154c9e5e3.png]]

##### 

**Non-Relational (noSQL / not just** **SQL****)**

-   Organizing data is anything but a traditional table
    -   Key-value stores
    -   Documents (JSON, XML, etc)
    -   Graphs
    -   Flexible Tables

**Relational Databases (****SQL****)**

-   Relational Database Management Systems(RDBMS)
    -   Help users create and maintain a relational database
        -   mySQL, Oracle, postgreSQL, mariaDB, etc.

-   Structured Query Language (SQL)
    -   Standardized language for interacting with RDBMS
    -   Used to perform C.R.U.D operations, as well as other administrative tasks (user management, security, backup, etc)
    -   Used to define tables and structures
    -   SQL code used on one RDBMS is not always portable to another without modification.

Non-Relational Databases (noSQL / not just SQL)

-   Non-Relational Database Management systems (NRDBMS)
    -   Help users create and maintain a non-relational database
        -   Mongo, dynamoDB, apache cassandra, firebase, etc

-   Implementation Specific
    
    -   Any non-relational database falls under this category, so there's no set language standard.
    -   Most NRDBMS will implement their own language for performing C.R.U.D and administrative operations on the database.

**Database Queries**

Queries are requests made to the database management system for specific information

As the database's structure becomes more and more complex, it becomes more difficult to get the specific pieces of information we want.

A google search is a query

**Wrap Up**
-   Database is any collection of related information
-   Computer are great for storing databases
-   Database Management System (DBMS) make it easy to create, maintain and secure a database
-   DBMS allow you to perform the C.R.U.D operations and other administrative tasks
-   Two types of Databses, Relational & Non-Relational
-   Relational databses use SQL and store data in tables with rows and columns
-   Non-Relational data store data using other data structures

### 

Tables and Keys
-   Column
-   Row

**Primary Key**
-   Surrogate Key - ID, no mapping to anything in the real world
-   Natural Key - SSN, email
-   Foreign Key - primary key in another database table

### Structured Query Language (SQL)

SQL is a language used for interacting with Relational Database Management Systems (RDBMS)

-   You can use SQL to get the RDBMS to do things for you
    -   Create, retrieve, update & delete data
    -   Create & manage databases
    -   Design & create database tables
    -   Perform administration tasks (security, user management, import/export, etc.)
-   SQL implementations vary between systems
    -   Not all RDBMS follow the SQL standard to a 'T'
    -   The concepts are the same but the implementation may vary
-   SQL is actually a hybrid language, it's basically 4 types of languages in one
    -   **Data Query language (DQL)**
        -   Used to query the database for infomation
        -   Get information that is already stored there
    -   **Data Definition Language (****DDL****)**
        -   Used for defining database schemas
    -   **Data Control Language (****DCL****)**
        -   Used for controlling access to data in the database
        -   User & permissions management
    -   **Data Manipulation Language (****DML****)**
        -   Used for inserting, updating and deleting data from the database
-   **Queries**
    -   A query is a set of instructions given to the RDBMS (written is SQL) that tell the RDBMS what information you want it to retrieve for you.
        -   TONS of data in a DB
        -   Often hidden in a complex schema
        -   Goal is to only get the data you need

```
SELECT employee.name, employee.age
FROM employee
WHERE employee.salary > 30000;
```

```
### Installation

**MacOS**

https://dev.mysql.com/downloads/mysql/
```

```SQL
echo 'export PATH=/usr/local/mysql/bin:$PATH'>>~/.bash_profile

. ~/.bash_profile

mysql

mysql -u root -p
```

```SQL
create database giraffe; -- create new database
```

### Creating Tables

```SQL
INT             -- Whole Number
DECIMAL(M,N)    -- Deciamal Numbers -- Exact Value M-Total Digit N Digit after decimal
VARCHAR(1)      -- String of text of length 1
BLOB            -- Binary Large Object, Stores large data
DATA            -- 'YYYY-MM-DD'
TIMESTAMP       -- 'YYYY-MM-DD HH:MM:SS' - used for recording time
```


PostgreSQL - open sourced
object relational database (custom type)

| PostgreSQL                                                                                                           | mySQL                                    |
| -------------------------------------------------------------------------------------------------------------------- | ---------------------------------------- |
| Enterprise Level                                                                                                     | Small Website                            |
| - performance<br>- MVCC,  multi-version concurrency control<br>multiple transaction at the same time<br>- continuity | - easy to use<br>- fast<br>- Scalability |
