# VCIF Project Database

## Introduction

This repository documents the development process of a database for the VCIF project. Our team is tasked with selecting the most suitable database system to accommodate the diverse needs of our data and applications. The options considered include NoSQL (e.g., MongoDB), SQL (e.g., PostgreSQL), and RDF (Resource Description Framework) databases, each offering unique capabilities and advantages.

## Database Systems Overview

### RDF (Resource Description Framework)

RDF is a graph data model designed to represent semantics formally. It structures data into triplets consisting of a subject, predicate, and object. This model is particularly powerful for representing relationships and metadata. Data manipulation is handled through SPARQL, a specialized query language for RDF. RDF's strength lies in its ability to handle complex, interlinked data and support rich metadata through ontologies.

### SQL Databases

SQL databases like PostgreSQL are ideal for structured data with well-defined schemas. They excel in environments where ACID (Atomicity, Consistency, Isolation, Durability) compliance is required. SQL databases are typically easier to manage for vertical scaling and are highly effective when operating on a single server with substantial resources.

#### Advantages of SQL:

- **Structured Data Handling**: Optimal for data that fits well into tables and rows with fixed schemas.
- **ACID Compliance**: Ensures reliable transaction processing.
- **Vertical Scalability**: Excels in environments where increasing server capabilities can meet scaling needs.

### NoSQL Databases

NoSQL databases offer flexibility for handling unstructured or semi-structured data such as JSON or XML documents. They are designed to provide high performance with low-latency operations and are suited for environments where data is distributed across multiple servers or nodes.

#### Advantages of NoSQL:

- **Flexibility**: Manages unstructured or semi-structured data efficiently.
- **Horizontal Scalability**: Supports scaling out across many servers or nodes.
- **Performance**: Optimized for rapid data retrieval and effective use of various data formats.

## Decision Criteria

The selection of the database technology will be guided by:
- The nature of the data (structured vs. unstructured)
- The requirements for scalability (vertical vs. horizontal)
- The need for speed and low latency in operations
- Compliance with ACID properties for transactional integrity

## Decision

### PostgreSQL: A Hybrid Approach

PostgreSQL is a versatile, open-source database system that supports SQL and NoSQL data types. It offers a hybrid approach, accommodating traditional and dynamic data models with its support for JSON and JSONB data types. This flexibility makes PostgreSQL an excellent choice for projects that require the ability to handle a variety of data formats effectively.


*Notes:*   

ACID compliance refers to a group of principles that ensure the reliability of database transactions, encompassing Atomicity, Consistency, Isolation, and Durability. These properties collectively ensure that all database transactions are processed reliably and maintain data integrity despite errors, power outages, and other unexpected challenges. Specifically, a transaction in database systems is a series of operations that must either all succeed together or fail together, preserving the state of your data:

- **Atomicity** guarantees that each transaction is treated as a single "unit," which either completes in its entirety or does not occur at all.
- **Consistency** ensures that a transaction can only bring the database from one valid state to another, maintaining database invariants.
- **Isolation** ensures that concurrent transactions occur independently without interference.
- **Durability** guarantees that once a transaction is committed, it will remain so, even in the event of a system failure.

These characteristics are fundamental to designing reliable database systems and are crucial for applications requiring robust data integrity and error resilience.


## References:
- [Introduction to RDF Databases](https://medium.com/@brkyataman/introduction-to-rdf-databases-e54c1fc8c51d)
- [What is an RDF Triplestore?](https://www.ontotext.com/knowledgehub/fundamentals/what-is-rdf-triplestore/)
- [Cool things I do with RDF](https://medium.com/@dallemang/jug-o-cool-things-i-do-with-rdf-3cdb5b059192)
- [NoSQL vs PostgreSQL](https://medium.com/@antzwo/nosql-vs-postgresql-6b8a6854550)
- [Bridging the Gap Between SQL and NoSQL in PostgreSQL](https://medium.com/the-table-sql-and-devtalk/bridging-the-gap-between-sql-and-nosql-in-postgresql-8aa4e35cebcd)
- [MariaDB vs PostgreSQL: 14 Critical Differences](https://kinsta.com/blog/mariadb-vs-postgresql/#:~:text=MariaDB%20is%20deemed%20suitable%20for,to%20outperform%20MariaDB's%20query%20cache.)