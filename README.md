# Database Overview

## What is Data?
Data refers to raw facts or information about something.

## What is a Database?
A database is a collection of related data.

## What is a Database Management System (DBMS)?
A Database Management System is a software system that enables users to define, create, and maintain databases.

## What is a File System?
A file system stores data in a hierarchical form using a data structure called trees. Before DBMS, data was stored in file systems.

## Disadvantages of File Systems and How DBMS Overcomes Them

### Retrieval Speed
- **File System**: Data is stored in a flat, unstructured format, requiring a full scan to retrieve specific data.
- **DBMS**: Data is stored in a structured format (tables, rows, columns) with indexing. DBMS uses advanced structures like binary trees and hash tables for faster access.

### Data Redundancy and Inconsistency
- **File System**: Data duplication and inconsistency occur when the same data is stored in multiple files, and updates are not synchronized.
- **DBMS Solutions**:
  - **Single Storage Location**: Data is stored in one place (tables) and referenced everywhere, eliminating duplication.
  - **Automatic Updates**: Updates are propagated throughout the system, reducing inconsistency.
  - **Data Normalization**: Organizes data to minimize redundancy and store only essential information.

### Data Security
- **File System**: Lacks advanced control features and relies on basic file-level permissions.
- **DBMS**: Provides user authentication, role-based access control, and permissions to manage data access and modification.

### Concurrency Control
- **File System**: Limited or no concurrency control, which can lead to data corruption or inconsistencies.
- **DBMS**: Uses techniques like locking, transactions, and timestamps to manage simultaneous access and ensure data integrity.

## Types of Databases

### Relational Databases (RDBMS)
- **Definition**: Store data in a structured format using tables (rows and columns). Relationships between data are established through foreign keys.
- **Examples**: MySQL, PostgreSQL, Oracle
- **Use Cases**: Financial systems, e-commerce, enterprise applications where data consistency is critical.

### Non-Relational Databases (NoSQL)
- **Definition**: Store data in flexible formats like documents, key-value pairs, wide-column stores, or graphs. They do not rely on structured tables.
- **Examples**: MongoDB, Cassandra, Redis
- **Use Cases**: Big data, real-time analytics, unstructured data like social media or IoT data.

## Relational Database Terminologies

| **Term**       | **Description**                                                |
|----------------|----------------------------------------------------------------|
| **Columns/Fields/Attributes** | Represents characteristics of entities.                    |
| **Rows/Records/Tuples**      | Represents individual instances of data of an entity.        |
| **Degree**     | Number of columns in a table/number of attributes.              |
| **Cardinality** | Number of rows/records in a table.                             |

### Rules in Relational Databases

1. **Unique Rows**: Every row should be unique, meaning that at least one attribute of the entity should be different from others, even if the rest of the attributes are the same.
2. **Single Value per Cell**: Each cell can contain only a single value. For example, to handle multiple mobile numbers for a customer, create a separate table:

   **Customer Table**:
   | Customer ID | Customer Name | Phone Number | Address  |
   |-------------|---------------|--------------|----------|
   | 1           | John Doe      | 1234-5678    | 123 Elm St |

   **Mobile Numbers Table**:
   | Customer ID | Mobile Number |
   |-------------|---------------|
   | 1           | 555-1234      |
   | 1           | 555-5678      |

3. **Column Order**: The order of columns does not matter in a relational database because data is accessed by column names, not their positions.
4. **Row Order**: The order of rows does not matter because each row is uniquely identified by a primary key. Data is queried based on the key, not the row's position.

## Conclusion

Databases are essential for managing data efficiently, and DBMSs provide significant advantages over traditional file systems in terms of speed, redundancy, security, and concurrency control. Understanding these concepts and terminologies is crucial for working with relational and non-relational databases effectively.
