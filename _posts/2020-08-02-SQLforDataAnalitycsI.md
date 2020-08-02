---
title: "SQL for Data Analytics I"
date: 2020-08-02
tags: [SQL]
excerpt: "SQL for Data Analytics I"
mathjax: "True"
---

# Notes on SQL for Data Analytics -- 

- [1. Basic SQL and DB Concepts](#1)
- [2. Installing PostgreSQL MAC](#2)
- [3. Queries and Statements](#3)
- [4. Logical Operators](#4)
- [5. Joins](#5)
- [6. Keys](#6)
- [7. Alias](#7)

<a name='1'></a>
### Entity Relational Diagrams

An Entity Relational Diagram (ERD) is a common way to view data in a database. These diagrams help us visualize data and they include:
1.   The names of the tables
2.   The columns in each table
3.   The way the tables work together

We normally store data in spreadsheets. We can have multiple data fields spread spread across multiple spreadheets. We can use an ERD to make sense of these data, where each spreasheet is represented by a table.  At the top of the diagram we'll see the name of the spreadsheet/table and below the column names will be lsited. Using SQL we can access to all of these data by querying one or multiple tables. 

### Structured Query Language
**SQL** is the standard way to access data stored is relational databases and it has many advantages:
*   SQL is relatively easy to understand and learn
*   It allows us to access large amounts of data directly where it is stored without the need to copy the data into some other program to view it and it reduces overload, meaning 'spreadsheet won't crash while handling large volumes of data'
*   It is easy to audit and replicate. For instance, in Excel we'd need to click at individual cells to see how they are calculated whereas in SQL we can read a query from top to bottom. 
*   SQL can run queries across multiple tables at once which is great for performing aggregations that are similar to Pivot tables in Excel with a majot difference that Excel maxes out at ~1 millon rows and SQL can perform these operations across billions of rows at the time. 

### Attributes of SQL

*   Data Integrity is ensured -- only the data we want to enter is entered and only certain people are able to write to the database (**db**)
*   Data can be accessed quickly -- SQL quickly returns results/data from the db and code can be optimized to improve performance
*   Data can be easily shared -- multiple people within an organization can access the data concurrently. Every user would get exactly the same data ensuring consistency. 

### Key points about the data stored in SQL

*   Data in dbs are stored in tables -- just like in Excel spreadhseets
*   All the data in the same column must be of the same datatype (str, int, boolean). If a columnn has numeric/quantitative data then every element of the column must be the same. If we have text in a quantitative column we cannot perform any aggregations (mean, sum, etc.) and would get errors.  
*   Consistent datatypes makes working with dbs fast. 

### Types of SQL Databases

There are several SQL databases such as MySQL, Access, Oracle, Microsoft SQLServer, Postgres SQL.
Fundamentally, all these databases are the same and code can be applied across different paltforms but there are subtle differences in syntax and functions. SQL can also be written in other platforms such as Python, Scala and HaDoop.
The exercises in this notebook are based on Postgres SQL.

## SQL Elements

SQL has different elements. The most basic of them is the ***Statement***. A statement is simply a piece of SQL code. Statements tell the db what we want to do with the data. For instance:
*   CREATE stament -- is used to make a new table in the db
*   DROP TABLE -- is used to remove a table from the db
*   SELECT -- is used to read and display data. SELECT staments are commonly referred as queries. 

Let's look at the **SELECT** statement in more detail. 

We can think of the SELECT stament as a form we have to fill to retrieve data. The form contains questions such as : Where do you want to get your datafrom? What elements from that table would you like to retrieve? We get the idea. These questions are structured in the same order, every time. Some of them are mandatory and other optional. When writing a SELECT stament, these questions are represented by a single word, such as ```SELECT``` and ```FROM``` These words are called ***clauses***. 

The ```FROM``` clause tells the query which data/table to use.
The ```SELECT``` clause tells the query which columns to read from the table. We can select multiple columns from a table by passing the table names separated by commas and we can also select **ALL** columns by passing an asterisk ```*```. 
The ```SELECT``` and ```FROM``` clauses are **mandatory**

``` SELECT *
       FROM db.table ```

<a name='2'></a>
### Installing PostgreSQL (MAC-OS)

In the shell run:

```brew install postgresql```

### Getting Started

Start PostgreSQL. In the shell run:

```brew services start postgresql```

To stop:

```brew services stop postgresql```

Once PostgreSQL has been started:

```psql postgres```

If executed successfully we are now working inside the psql terminal.
To create a new user and password:

```CREATE ROLE newuser WITH LOGIN PASSWORD 'password'```

```ALTER ROLE newuser CREATEDB;```

New user has been created, we can now exit the psql terminal so we can login into it again with the new user. 

```$ psql postgres -U newuser```

We shoudl now see:

```postgres=>```

To create a new database:

```postgres=> CREATE DATABASE database_name:```

Exit the current terminal ```\q```

Access the recently created db by:

```psql database_name```

To create a table in that db:

```database_name=# CREATE TABLE table_name (column_1 INTEGER, column_2 VARCHAR);```

I have data in a .csv file that I want to copy to my postgresql database. 
The csv contains made-up accounts data. It's name is accounts and this is just one table of the database. To copy the csv into the databse first:
*   Create the table in the database -- think of it as create a spreadsheet.
*   Create the columns in the table. They have to match what we have in the spreadsheet. 
*   Once the table is set up type the following commands:
    *   ```COPY table_name``` # the table we want to copy into
    *   ```FROM 'absolute_path_to_your_speadsheet'```
    *   ```DELIMITER ',' CSV HEADER;```

If executed successfully, we will see a message: ```COPY 100``` or whatever number of records that were copied. 

