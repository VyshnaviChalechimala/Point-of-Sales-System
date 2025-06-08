# Point-of-Sales-System

# 🛒 Point-of-Sale (POS) System: End-to-End Relational to NoSQL Cloud Deployment

## 🌟 Project Overview

This repository showcases a comprehensive end-to-end development of a Point-of-Sale (POS) System, created as part of an advanced data management course at Texas A&M University. The project was designed to mirror real-world enterprise data environments—starting from relational schema design and ETL to advanced SQL programming, clustering for high availability, and eventually transitioning to NoSQL-based analytics using MongoDB.

Through 10 structured milestones, this project covers the full data lifecycle: cloud infrastructure setup on AWS, data ingestion and transformation, relational database design with MariaDB, automation using procedures and triggers, multi-node replication and clustering, and modern document-based querying via JSON exports and MongoDB integration.

> 📌 *Note: To maintain academic integrity, source files such as `.sql` scripts and CSVs are not publicly included. This documentation serves to outline the design, logic, and tools applied throughout the build.*

---

## 🎯 Core Objectives & Features

- **End-to-End Data Lifecycle Coverage:** From raw data ingestion to advanced database operations and NoSQL analytics.
- **ETL Development:** Designed robust SQL-based ETL pipelines for cleaning, transforming, and loading data.
- **Advanced SQL Engineering:** Built views, indexes, stored procedures, prepared statements, and triggers to automate business logic and enforce integrity.
- **Database Clustering & High Availability:**
  - Implemented **MariaDB Master-Replica Clustering** for read scaling.
  - Set up **MariaDB Galera Cluster** for synchronous multi-master replication.
- **Hybrid Data Strategy:** Exported relational data to JSON and queried it through **MongoDB** to simulate a NoSQL layer.
- **Cloud-Hosted Architecture:** All deployments were hosted on **AWS EC2** instances running Amazon Linux.

---

## 🏗️ System Architecture

The system is organized into four primary phases:

1. **Relational Design & Setup (MariaDB on AWS):**
   - Normalized schema design and data import from staged CSVs
   - ETL operations to clean and restructure raw data

2. **SQL Development & Optimization:**
   - Views and indexes for performance
   - Stored procedures and triggers for automation and consistency
   - Prepared statements and transactions for secure and consistent updates

3. **Scalability & Redundancy:**
   - Master-Replica setup for load distribution
   - Galera Cluster configuration for synchronous multi-master deployment

4. **NoSQL Transformation:**
   - Denormalized JSON exports using SQL JSON functions
   - MongoDB ingestion and analytical querying using `mongosh`

---

## 📄 Entity-Relationship Diagram (ERD)

The system’s schema supports a normalized relational model capturing customer, product, order, and city-level data with full referential integrity and extensibility.

![Architecture](https://github.com/user-attachments/assets/fc7251f5-5e5b-4dbe-b8d3-775c87845794)


### 🧱 Key Relational Entities

- **Product**  
  `id`, `name`, `currentPrice`, `availableQuantity`

- **City**  
  `zip` (Primary Key), `city`, `state`

- **Customer**  
  `id` (Primary Key), `firstName`, `lastName`, `email`, `address1`, `address2`, `phone`, `birthdate`, `zip` (Foreign Key to City)

- **Order**  
  `id` (Primary Key), `datePlaced`, `dateShipped`, `customer_id` (Foreign Key), `OrderSubtotal`, `SalesTax`, `OrderTotal`  
  *(virtual column: `OrderSubtotal + SalesTax`)*

- **OrderLine**  
  `order_id` (Foreign Key), `product_id` (Foreign Key), `quantity`, `UnitPrice`, `LineTotal`  
  *(virtual column: `Quantity * UnitPrice`)*

- **PriceHistory**  
  `ChangeID` (Primary Key, auto-increment), `product_id` (Foreign Key), `oldPrice`, `newPrice`, `changeDate` *(default `NOW()`)*

- **SalesTax**  
  `zip` (Primary Key, Foreign Key to City), `rate` *(DECIMAL for percentages)*
 

---

## 🚧 Milestone Breakdown

### Milestone 1: Infrastructure Setup (AWS & MariaDB)
- Launched EC2, installed MariaDB, created initial schema and user permissions

### Milestone 2: Extract, Transform, Load (ETL)
- Loaded raw CSVs, used staging tables and SQL scripts to clean/normalize data

### Milestone 3: Views & Indexes
- Built logical and materialized views; added indexes for optimized access

### Milestone 4: Transactions & Prepared Statements
- Implemented atomic operations and dynamic SQL execution for safe inserts/updates

### Milestone 5: Stored Procedures
- Encapsulated key logic into reusable procedures for calculating totals and refreshing views

### Milestone 6: Triggers
- Added BEFORE/AFTER triggers to manage inventory, audit changes, and maintain business rules

### Milestone 7: Master-Replica Clustering (MariaDB)
- Configured one primary and two read replicas; validated replication behavior

### Milestone 8: Galera Cluster Setup
- Built a 3-node multi-master synchronous cluster for fault tolerance and load distribution

### Milestone 9: JSON Export for MongoDB
- Used `JSON_OBJECT` and `JSON_ARRAYAGG` to export data into structured documents

### Milestone 10: MongoDB Integration
- Imported JSON into MongoDB, ran business queries using document-based traversal

---

## 🛠️ Technologies & Tools

- **Cloud:** AWS EC2 (Linux)  
- **Relational Database:** MariaDB (SQL)  
- **Clustering Tools:** MariaDB Replication, Galera Cluster  
- **NoSQL:** MongoDB (`mongoimport`, `mongosh`)  
- **Languages & Formats:** SQL, Shell Script, JSON  
- **ETL & Query Tools:** Stored Procedures, Views, Triggers, JSON Functions (`JSON_OBJECT`, `JSON_ARRAYAGG`)  
- **Security:** Key-based SSH access  
- **Version Control:** Git & GitHub (for documentation and versioning)

---

## 💭 Reflections & Takeaways

This project was one of the most hands-on and rewarding academic experiences I’ve had. It pushed me to not only apply SQL and database concepts in a real-world setting but also explore NoSQL technologies and cloud deployment practices. The structured milestones gave me the confidence to handle diverse data management challenges—from schema design and automation to high availability and hybrid querying.

Beyond technical implementation, I gained a deeper understanding of how to choose the right persistence layer for different use cases, and how relational and document-based models complement each other in modern architectures.
