# SQL: Structured Query Language - Introduction

**Database** store and organize large amounts of data. Databases has data integrity and can handle massive amounts of data. Can support data for websites and application and can automate steps for re-use. Can combine multiple datasets. SQL is a Declarative Programming Language (Non-Procedural), **Spreadsheets** are good for one-time analysis and for reasonable dataset size. It is quick to use.  
<br>
**Data Definition Language** is a set of statements hat allow the user to define or modify data structures and objects such as tables. Commands include `CREATE`, `ALTER`, `DROP`, `RENAME`, `TRUNCATE`  
<br>
**Data Manipulation Language** allows us to manipulate the data in the tables of a database. Commands incude `SELECT`, `UPDATE`, `INSERT`,   `DELETE`   
<br>
**Data Control Language** allows us to manage the rights users have in a database.Commands include `GRANT`, `REVOKE`  
<br>
**Transaction Control Language**. `COMMIT` will save your change permanently. Saves the transaction in the database. `ROLLBACK` allows you to take a step back  
<br>
**Relational Databases** Each table has relation to one another. There is a structure defined as tables and has rows and columns. **Non-relational Databases** has no structure, no tables, no keys, no rows and columns.  
<br>
**Relational Schemas: Primary Key** column whose value exists and is unique for every record in table. Each table can have only one primary key. Combination of two column values can be considered as a primary key as long as its unique to other combination. Cannot contain `null` values.  
<br>
**Relational Schemas: Foreign Key** identifies the relationships between tables, not the tables themselves. They are the primary key on another table.  
<br>
**Relational Schemas: Unique Key & Null Values** uniques are used whenever we would like to specify that you don't want to see duplicate data in a given fields. Unique key can be `null`  
<br>
**Relationships** tell you how much of the data from a foreign key field can be seen in the primary key column of the table the data is related to and vice versa





