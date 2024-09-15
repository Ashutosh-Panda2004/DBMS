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

---

# Keys in DBMS (Database Management System)

**Keys** are fundamental to database design and management. They help maintain data integrity and enable efficient data retrieval by uniquely identifying records in a table. Each type of key has a specific role in organizing and managing relational databases.

Let’s consider the following `Student` table for explanation:

| **Student ID** | **Name**  | **Email**             | **Phone**   | **Dept**    |
|----------------|-----------|-----------------------|-------------|-------------|
| 101            | Alice     | alice@example.com      | 9876543210  | CS          |
| 102            | Bob       | bob@example.com        | 8765432109  | IT          |
| 103            | Charlie   | charlie@example.com    | 7654321098  | CS          |

## Types of Keys:

### 1. Superkey
A **superkey** is a set of one or more attributes (columns) that can uniquely identify each row in a table. It may contain unnecessary (redundant) attributes.

- **Example**: `{Student ID}`, `{Student ID, Email}`, or `{Email, Phone}`.  
  In the above table, any combination that includes `Student ID` or `Email` is a superkey because both attributes are unique for each student.

### 2. Candidate Key
A **candidate key** is a minimal superkey, meaning it uniquely identifies a row without any redundant attributes. It is the smallest set of attributes that can uniquely identify a record.

- **Example**: `{Student ID}`, `{Email}`.  
  Both `Student ID` and `Email` can individually identify a student, but no attribute can be removed from them while still maintaining uniqueness. Therefore, they are **candidate keys**.

### 3. Primary Key
A **primary key** is a special candidate key that is chosen by the database designer to uniquely identify records in a table. The primary key must be unique and cannot contain NULL values.

- **Example**: `{Student ID}`.  
  In this case, `Student ID` is chosen as the **primary key** because it uniquely identifies each student and cannot be NULL.

### 4. Alternate Key
An **alternate key** is any candidate key that is not selected as the primary key. While it could serve the same purpose as the primary key, it is not used for that role.

- **Example**: `{Email}`.  
  Since `Student ID` was chosen as the primary key, `Email` becomes the **alternate key** because it can also uniquely identify students.

### 5. Foreign Key
A **foreign key** is an attribute (or set of attributes) in one table that references the **primary key** in another table. It is used to maintain relationships between tables and ensure referential integrity.

- **Example**: If we have an `Enrollment` table:
  
  | **Enrollment ID** | **Student ID** | **Course**  |
  |-------------------|----------------|-------------|
  | 1                 | 101            | Database    |
  | 2                 | 102            | Networks    |

  Here, `Student ID` in the `Enrollment` table is a **foreign key** that links to the `Student ID` in the `Student` table. This ensures that each enrollment record is associated with a valid student.

### 6. Composite Key
A **composite key** is a key that consists of two or more attributes that together uniquely identify a record in a table. None of the individual attributes can uniquely identify a row on their own.

- **Example**: `{Student ID, Dept}`.  
  In a scenario where students can be enrolled in multiple departments, the combination of `Student ID` and `Dept` can be used as a **composite key** to uniquely identify each student-department relationship.

### 7. Unique Key
A **unique key** ensures that all values in a column or set of columns are unique. Unlike a primary key, a unique key can accept one NULL value.

- **Example**: `{Phone}`.  
  The `Phone` column can be a **unique key** because each student's phone number is unique, but it can also be NULL for a student who does not provide a phone number.

## Key Relationships Example:
Consider we have another table, `Course Enrollment`, where we track which courses students are enrolled in:

| **Enrollment ID** | **Student ID** | **Course ID** |
|-------------------|----------------|---------------|
| 1                 | 101            | CS101         |
| 2                 | 102            | IT201         |

- `Student ID` in `Course Enrollment` is a **foreign key** that references the **primary key** in the `Student` table.
- A **composite key** of `{Student ID, Course ID}` could uniquely identify which student is enrolled in which course.

## Summary of Key Definitions:

| **Key Type**     | **Definition**                                                                                       | **Example in `Student` Table**                                  |
|------------------|------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------|
| **Superkey**     | A set of one or more attributes that uniquely identify a row.                                         | `{Student ID}`, `{Student ID, Email}`, `{Email, Phone}`         |
| **Candidate Key**| A minimal superkey that uniquely identifies a row.                                                   | `{Student ID}`, `{Email}`                                       |
| **Primary Key**  | A candidate key chosen to uniquely identify rows; cannot be NULL.                                     | `{Student ID}`                                                  |
| **Alternate Key**| A candidate key that was not chosen as the primary key.                                               | `{Email}`                                                       |
| **Foreign Key**  | An attribute in one table that references the primary key of another table.                           | `Student ID` in the `Enrollment` table links to the `Student` table. |
| **Composite Key**| A key that consists of two or more attributes to uniquely identify a record.                         | `{Student ID, Dept}`                                            |
| **Unique Key**   | Ensures all values in a column/set of columns are unique but can contain a NULL value.                | `{Phone}`                                                       |

