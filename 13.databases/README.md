# Introduction to Databases
A database is an organized collection of structured data that is stored and managed electronically. Databases are essential tools for managing, storing, and retrieving data efficiently, and they play a vital role in modern applications.

## Database Management Systems (DBMS)
A Database Management System (DBMS) is software that interacts with users, applications, and the database itself to capture, store, and manage data. It provides an interface for performing various operations on the data, such as inserting, updating, deleting, and retrieving data. The primary goal of a DBMS is to ensure that data remains consistent, secure, and easily accessible.

There are two main types of DBMSs:

- Relational Database Management Systems (RDBMS): These systems store data in tables with predefined relationships between them. The most common query language for RDBMSs is SQL (Structured Query Language).

- Non-Relational Database Management Systems (NoSQL): These systems store data in various formats, such as key-value, document, column-family, or graph. NoSQL databases are known for their ability to scale horizontally and handle unstructured or semi-structured data.

## Overview of SQL and NoSQL databases
Databases can be broadly classified into two categories: SQL (Structured Query Language) and NoSQL (Not only SQL) databases. SQL databases, also known as relational databases, are based on the relational model, where data is stored in tables with predefined schema and relationships between them. Some popular SQL databases include MySQL, PostgreSQL, Microsoft SQL Server, and Oracle. SQL databases are known for their consistency, reliability, and powerful query capabilities.

On the other hand, NoSQL databases are a diverse group of non-relational databases that prioritize flexibility, scalability, and performance under specific workloads. NoSQL databases can be further categorized into document databases, key-value stores, column-family stores, and graph databases, each with their unique data models and use cases. Some widely-used NoSQL databases are MongoDB, Redis, Apache Cassandra, and Neo4j.

## High level differences between SQL and NoSQL
1. Storage: SQL stores data in tables where each row represents an entity and each column represents a data point about that entity; for example, if we are storing a car entity in a table, different columns could be ‘Color’, ‘Make’, ‘Model’, and so on.

NoSQL databases have different data storage models. The main ones are key-value, document, graph, and columnar. We will discuss differences between these databases below.

2. Schema: In SQL, each record conforms to a fixed schema, meaning the columns must be decided and chosen before data entry and each row must have data for each column. The schema can be altered later, but it involves modifying the whole database and going offline.

In NoSQL, schemas are dynamic. Columns can be added on the fly and each ‘row’ (or equivalent) doesn’t have to contain data for each ‘column.'

3. Querying: SQL databases use SQL (structured query language) for defining and manipulating the data, which is very powerful. In a NoSQL database, queries are focused on a collection of documents. Sometimes it is also called UnQL (Unstructured Query Language). Different databases have different syntax for using UnQL.

4. Scalability: In most common situations, SQL databases are vertically scalable, i.e., by increasing the horsepower (higher Memory, CPU, etc.) of the hardware, which can get very expensive. It is possible to scale a relational database across multiple servers, but this is a challenging and time-consuming process.

On the other hand, NoSQL databases are horizontally scalable, meaning we can add more servers easily in our NoSQL database infrastructure to handle a lot of traffic. Any cheap commodity hardware or cloud instances can host NoSQL databases, thus making it a lot more cost-effective than vertical scaling. A lot of NoSQL technologies also distribute data across servers automatically.

5. Reliability or ACID Compliancy (Atomicity, Consistency, Isolation, Durability): The vast majority of relational databases are ACID compliant. So, when it comes to data reliability and safe guarantee of performing transactions, SQL databases are still the better bet.

Most of the NoSQL solutions sacrifice ACID compliance for availability, performance, and scalability.


# SQL Databases
SQL (Structured Query Language) databases, also known as **relational databases**, are the most commonly used type of databases in software applications. They store data in tables, where each table consists of rows and columns. Relationships between tables are established using primary and foreign keys. SQL databases follow the ACID properties (Atomicity, Consistency, Isolation, Durability) to ensure reliable data transactions.

## RDBMS Concepts
- Tables: The fundamental building blocks of relational databases, tables represent the structure of the data. Each table contains rows (records) and columns (fields) that store individual pieces of data.

- Primary Key: A unique identifier for each row in a table. A primary key enforces uniqueness and ensures that no two rows share the same identifier.

- Foreign Key: A column (or a set of columns) in a table that refers to the primary key of another table. Foreign keys are used to establish relationships between tables and enforce referential integrity.

- Indexes: Database indexes are data structures that help to speed up data retrieval operations. They work similarly to the index in a book, allowing for faster lookups and searches.

- Normalization: The process of organizing a database into tables, columns, and relationships to reduce data redundancy and improve data integrity.

## SQL Language
SQL is a standardized language for managing and querying relational databases. It provides a powerful and flexible way to interact with the data. The language consists of several components, including:

- Data Definition Language (DDL): Allows for the **creation, modification, and deletion of database structures**, such as tables, indexes, and constraints.

- Data Manipulation Language (DML): Enables **data insertion, updating, deletion, and retrieval operations** on database tables.

- Data Control Language (DCL): Deals with **user permissions and access control** for database objects.

- Transaction Control Language (TCL): Manages database transactions and ensures **ACID compliance**.

## Popular SQL Databases
Several well-known SQL databases are available, each with its own features and use cases. Some popular SQL databases include:

- MySQL: An open-source, widely used RDBMS, MySQL is popular for web applications and is a component of the LAMP (Linux, Apache, MySQL, PHP/Perl/Python) stack.

- PostgreSQL: Another open-source RDBMS that focuses on extensibility, standards compliance, and performance. PostgreSQL is well-regarded for its advanced features, such as support for custom data types, full-text search, and spatial data operations.

- Microsoft SQL Server: A commercial RDBMS developed by Microsoft, featuring a comprehensive set of tools and features for enterprise-level applications. SQL Server is known for its tight integration with other Microsoft products, security features, and business intelligence capabilities.

- Oracle Database: A widely-used commercial RDBMS that offers high performance, advanced features, and scalability. Oracle is popular in large organizations and mission-critical applications due to its robustness, reliability, and comprehensive toolset.

## Pros and cons of using SQL databases
- ACID properties and consistency: SQL databases adhere to the **ACID** (Atomicity, Consistency, Isolation, Durability) properties, which ensure the reliability of transactions and the consistency of the data. These properties guarantee that any operation on the data will either be completed in its entirety or not at all, and that the **data will always remain in a consistent state**.

- Structured schema: SQL databases enforce a **predefined schema** for the data, which ensures that the data is structured, consistent, and follows specific rules. This structured schema can make it easier to understand and maintain the data model, as well as optimize queries for performance.

- Query language and optimization: SQL is a powerful and expressive query language that allows developers to perform complex operations on the data, such as filtering, sorting, grouping, and joining multiple tables based on specified conditions. SQL databases also include query optimizers, which analyze and optimize queries for improved performance.

- Scalability and performance: SQL databases can be scaled vertically by adding more resources (such as CPU, memory, and storage) to a single server. However, horizontal scaling, or distributing the data across multiple servers, can be more challenging due to the relational nature of the data and the constraints imposed by the ACID properties. This can lead to performance bottlenecks and difficulties in scaling for large-scale applications with high write loads or massive amounts of data.