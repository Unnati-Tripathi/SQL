# Assignment - 2

# Proublem Statement

Database Selection Framework
	For each category below, compare the options, explain when you would pick one over the other, and justify your choice with a real-world scenario:
	Relational Databases - compare available options, when would you pick one over another and why?
	NoSQL Databases - compare available options, what is the fundamental difference in data patterns between them?
	Cloud Data Warehouses - compare available options, what are the pricing and architectural differences that drive your choice?
	In-Memory Databases - compare available options, what completely different problems do they solve?
	Object Storage - compare available options, when does vendor lock-in become a real concern?
 
-------------------------------------------------------------------------------------------------------

# Solution

Different types of databases are designed for different kinds of problems.  
Choosing the correct database depends on factors like data structure, scalability, performance, pricing, consistency, and real-world business requirements.

-------------------------------------------------------------------------------------------------------

# 1. Relational Databases

Relational databases store data in tables using rows and columns.  
They are best suited for structured data and applications where relationships between data are important.

## Common Options

- MySQL
- PostgreSQL
- Oracle Database
- Microsoft SQL Server

---

## Comparison

### MySQL
MySQL is simple, fast, and widely used in web applications.  
It is a good choice for small to medium-scale projects where simplicity and speed are important.

### PostgreSQL
PostgreSQL is more advanced and feature-rich.  
It supports complex queries, JSON data, advanced indexing, and better standards compliance.

### Oracle Database
Oracle is mainly used in large enterprise systems where extremely high reliability, security, and large-scale transaction handling are required.

### SQL Server
SQL Server is commonly used in enterprise environments that are heavily dependent on Microsoft technologies.

---

## When Would I Choose One Over Another? Lets compare..

- I would choose **MySQL** for a startup web application or an e-commerce website because it is lightweight and easy to manage.
- I would choose **PostgreSQL** when the application requires complex queries, analytics, or advanced database features.
- I would choose **Oracle** for banking or enterprise financial systems where security and transaction consistency are critical.
- I would choose **SQL Server** in organizations already using Microsoft Azure or other Microsoft services.

---

## Real-World Scenario

For an online shopping website like Amazon:
- product orders,
- payment details,
- customer accounts,
- inventory management

would be best handled using a relational database because relationships between data are very important.

-------------------------------------------------------------------------------------------------------





# 2. NoSQL Databases

NoSQL databases are designed for flexible and large-scale data handling.  
Unlike relational databases, they do not always require fixed schemas.

## Common Types

- Document Databases → MongoDB
- Key-Value Databases → Redis
- Column-Based Databases → Cassandra
- Graph Databases → Neo4j

---

# Fundamental Difference in Data Patterns

The biggest difference between NoSQL databases is the way they store and access data.

---

## Document Databases (MongoDB)

Store data in JSON-like documents.

Best for:
- flexible schemas
- changing application structures
- web and mobile applications

### Example
User profiles in a social media app where every user may have slightly different data.

---

## Key-Value Databases (Redis)

Store data as simple key-value pairs.

Best for:
- caching
- session management
- extremely fast lookups

### Example
Storing login sessions for users in a website.

---

## Column-Based Databases (Cassandra)

Store data column-wise and are optimized for huge distributed systems.

Best for:
- big data
- write-heavy applications
- distributed environments

### Example
IoT systems collecting millions of sensor readings every minute.

---

## Graph Databases (Neo4j)

Store relationships between data very efficiently.

Best for:
- connected data
- recommendation systems
- social networks

### Example
LinkedIn connection recommendations.

-------------------------------------------------------------------------------------------------------





# 3. Cloud Data Warehouses

Cloud data warehouses are mainly used for analytics and reporting on massive datasets.

## Common Options

- Snowflake
- Google BigQuery
- Amazon Redshift

---

# Comparison

## Snowflake

- Fully managed
- Separate storage and compute
- Easy scaling
- Good cross-cloud support

### Best For
Organizations wanting flexibility and easy maintenance.

---

## Google BigQuery

- Serverless architecture
- Pay-per-query pricing
- Very fast analytics

### Best For
Large analytical workloads where infrastructure management should be minimal.

---

## Amazon Redshift

- Strong AWS integration
- Good performance for structured analytics
- Cluster-based architecture

### Best For
Companies already deeply using AWS services.

---

# Real-World Scenario

A company like Netflix analyzing viewing behavior of millions of users would use a cloud data warehouse for reporting, trends, and analytics.

-------------------------------------------------------------------------------------------------------





# 4. In-Memory Databases

In-memory databases store data directly in RAM instead of disk, making them extremely fast.

## Common Options

- Redis
- SAP HANA

---

# What Different Problems Do They Solve?

## Redis

Used for:
- caching
- session storage
- real-time analytics
- message queues

### Example
Reducing database load in a high-traffic website.

---

## SAP HANA

Enterprise-grade in-memory database designed for real-time business analytics.

### Example
Real-time financial reporting in large enterprises.

---

# Key Difference

Traditional databases focus on permanent storage and consistency, while in-memory databases mainly focus on ultra-fast access speed and temporary high-performance operations.

-------------------------------------------------------------------------------------------------------





# 5. Object Storage

Object storage is used for storing large unstructured files like:
- images
- videos
- backups
- documents

## Common Options

- Amazon S3
- Google Cloud Storage
- Azure Blob Storage

---

# Comparison

## Amazon S3

Most popular and highly scalable object storage service with strong AWS ecosystem integration.

---

## Google Cloud Storage

Good for analytics-heavy systems and Google Cloud integration.

---

## Azure Blob Storage

Best suited for organizations heavily dependent on Microsoft Azure services.

---

# When Does Vendor Lock-In Become a Concern?

Vendor lock-in becomes a serious concern when:
- applications rely heavily on provider-specific APIs
- migration costs become very high
- storage architecture depends completely on one cloud provider

For example:
- moving petabytes of data from AWS S3 to another cloud can be expensive and time-consuming
- applications using AWS-specific storage features may require code changes after migration

---

# Conclusion

There is no single perfect database for every system.

- Relational databases are best for structured and consistent transactional systems.
- NoSQL databases are better for scalability and flexible data structures.
- Cloud data warehouses are optimized for analytics.
- In-memory databases solve high-speed access problems.
- Object storage is ideal for large unstructured files.

The correct choice always depends on the application's requirements, scalability needs, budget, and data patterns.