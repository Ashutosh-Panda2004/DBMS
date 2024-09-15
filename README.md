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


---

### What is a Non-Key Attribute?

A **non-key attribute** is any attribute (column) in a database table that is **not part of a key**. In simple terms, it means that the attribute does not participate in uniquely identifying a record in a table.

#### Key vs Non-Key Attributes:
- **Key Attribute**: These are attributes (like primary keys or candidate keys) that can uniquely identify a record in the table.
- **Non-Key Attribute**: These are attributes that provide additional information about the record but **cannot** uniquely identify it by themselves.

#### Example:

Let’s consider a table with `Emp_Id` as the primary key:

| **Emp_Id** | **Emp_Name**  | **Emp_Address**    | **Emp_Department** |
|------------|---------------|--------------------|--------------------|
| 101        | John Doe      | 123 Elm St         | HR                 |
| 102        | Jane Smith    | 456 Oak St         | IT                 |

- **Key Attribute**: `Emp_Id` (It can uniquely identify each record).
- **Non-Key Attributes**: `Emp_Name`, `Emp_Address`, `Emp_Department` (These provide details about the employee but cannot uniquely identify them).

In this table, `Emp_Name`, `Emp_Address`, and `Emp_Department` are **non-key attributes** because they are not involved in uniquely identifying a record in the table.

### Why is it Important?

Non-key attributes are typically functionally dependent on key attributes. This relationship forms the basis for concepts like functional dependencies and normalization in database design.

---

# Important Facts and Laws about Keys in DBMS

Here are some key facts and laws related to various types of keys in DBMS, which are commonly asked in interviews and discussions:

1. **Every Superkey is a Key, but not every Key is a Superkey**:
   - A superkey is any set of attributes that can uniquely identify a record, but some may include extra, unnecessary attributes. A candidate key is a minimal version of a superkey.

2. **Every Candidate Key is a Superkey, but not every Superkey is a Candidate Key**:
   - Candidate keys are minimal superkeys, meaning no attribute can be removed while still uniquely identifying a record.

3. **Every Primary Key is a Candidate Key, but not every Candidate Key is a Primary Key**:
   - A primary key is a candidate key that has been selected to uniquely identify records in a table.

4. **A Table can have only One Primary Key, but it can have Multiple Candidate Keys**:
   - Although there can be many candidate keys in a table, only one is chosen as the primary key.

5. **Every Primary Key is Unique, but not every Unique Key is a Primary Key**:
   - A primary key must be unique and non-null, while a unique key can accept one null value and is not necessarily the primary identifier for a table.

6. **Foreign Keys enforce Referential Integrity**:
   - A foreign key links two tables together by referencing the primary key of another table, ensuring that the relationship between records remains consistent.

7. **Composite Keys contain Multiple Attributes**:
   - A composite key is made up of two or more columns that together uniquely identify a record. However, no single part of a composite key can uniquely identify the record on its own.

8. **Null Values are not allowed in Primary Keys**:
   - Primary keys cannot contain null values because they are used to uniquely identify records, and a null value would violate this requirement.

9. **Unique Keys allow One NULL Value**:
   - Unlike primary keys, unique keys can accept a single NULL value, but all other values must be unique.

10. **A Foreign Key can Reference a Primary Key or a Unique Key**:
    - Foreign keys usually reference primary keys in another table, but they can also reference a unique key.

11. **Order of Columns or Rows does not Matter in Relational Databases**:
    - In relational databases, the order of columns or rows in a table does not affect the data retrieval, as queries are based on key values rather than their position.

12. **A Superkey can Contain Redundant Attributes**:
    - A superkey may have more attributes than necessary to uniquely identify a row. Removing redundant attributes from a superkey results in a candidate key.

13. **Multiple Foreign Keys in One Table**:
    - A table can have more than one foreign key, linking it to multiple other tables, ensuring complex relationships are managed efficiently.

14. **Alternate Keys are Candidate Keys**:
    - An alternate key is simply a candidate key that was not selected as the primary key but can still be used to uniquely identify records.

15. **Every Key in a Table Must Uniquely Identify a Record**:
    - All types of keys (primary, candidate, alternate, composite, etc.) must serve the purpose of uniquely identifying records in the table.

16. **A Candidate Key Cannot Contain NULL Values**:
    - Similar to a primary key, candidate keys are minimal superkeys and must not contain NULL values because they are used to uniquely identify records.
    
17. **Foreign Keys Can Contain NULL Values**:
    - A foreign key can have null values if it represents optional relationships, where a row in one table may not necessarily have a matching row in another table.

18. **A Table Without a Candidate Key is not Well-Structured**:
    - A table must have at least one candidate key (minimal superkey) for it to be considered well-structured in relational databases.

19. **A Composite Key is formed when No Single Attribute Can Uniquely Identify the Record**:
    - In scenarios where a single attribute cannot uniquely identify a record, multiple attributes are combined to form a composite key.

20. **Primary Keys in Different Tables Can Share the Same Name**:
    - While primary keys uniquely identify rows within a table, different tables can have primary keys with the same name, such as `ID`, as long as their context (i.e., table) differs.
   









































































































---

# NORMALISATION

## Functional Dependency in DBMS

Functional dependency (FD) is a relationship that exists between two attributes in a database table. It explains how one attribute (or a set of attributes) can determine the value of another attribute.

## What is Functional Dependency?

Functional dependency is often defined between a **primary key** and a **non-key attribute**. It means that if we know the value of one attribute (the determinant), we can determine the value of another attribute (the dependent).

### Notation:

- **X → Y**  
  This means that attribute `X` determines the value of attribute `Y`. Here, `X` is the **determinant** (left side), and `Y` is the **dependent** (right side).

### Example:

Consider the following `Employee` table:

| **Emp_Id** | **Emp_Name** | **Emp_Address**   |
|------------|--------------|-------------------|
| 101        | Alice        | 123 Elm St        |
| 102        | Bob          | 456 Maple Ave     |
| 103        | Charlie      | 789 Oak Blvd      |

In this example, the `Emp_Id` uniquely identifies each employee's name (`Emp_Name`). So we can say:

- **Emp_Id → Emp_Name**  
  This means `Emp_Name` is **functionally dependent** on `Emp_Id` because for every `Emp_Id`, there is one specific `Emp_Name`.

## Types of Functional Dependencies

There are two main types of functional dependencies: **Trivial** and **Non-trivial** dependencies.

### 1. Trivial Functional Dependency

A functional dependency is considered **trivial** if the dependent (right side) is a subset of the determinant (left side). This includes cases where both sides are the same.

#### Examples:
- **A → A**  
  This is trivial because `A` determines itself.
  
- Consider a table with two columns: `Employee_Id` and `Employee_Name`.  
  `{Employee_Id, Employee_Name} → Employee_Id`  
  This is a trivial functional dependency because `Employee_Id` is part of `{Employee_Id, Employee_Name}`.

Trivial dependencies are simple cases where the dependent attribute is already part of the determinant, making them self-evident.

### 2. Non-trivial Functional Dependency

A functional dependency is **non-trivial** when the dependent attribute is **not** a subset of the determinant. In other words, the right side does not overlap with the left side.

#### Examples:
- **Emp_Id → Emp_Name**  
  This is non-trivial because `Emp_Name` is not a part of `Emp_Id`.

- **Name → DOB**  
  Here, knowing someone's `Name` can determine their `Date of Birth` (DOB), but `DOB` is not a part of `Name`, so it's non-trivial.

### Complete Non-trivial Functional Dependency:

A **complete non-trivial functional dependency** occurs when the intersection of the determinant and the dependent is `NULL` (they share no common attributes).

#### Example:
- **Emp_Id → Emp_Address**  
  Since `Emp_Id` and `Emp_Address` have no common attributes, this is a complete non-trivial functional dependency.

## Understanding Through Example

Let's consider another example to better understand functional dependency:

| **Student_ID** | **Student_Name** | **Course** | **DOB**       |
|----------------|------------------|------------|---------------|
| 1              | Alice            | Math       | 01-Jan-2000   |
| 2              | Bob              | Physics    | 15-Feb-1999   |
| 3              | Charlie          | Chemistry  | 10-Mar-2001   |

### Functional Dependencies:
- **Student_ID → Student_Name**  
  `Student_Name` is functionally dependent on `Student_ID`. Knowing the `Student_ID` uniquely identifies the student name.

- **Student_Name → DOB**  
  `DOB` is functionally dependent on `Student_Name`. Knowing the student's name gives us their date of birth.

### Trivial Dependency:
- **Student_ID → Student_ID**  
  This is a trivial functional dependency because `Student_ID` determines itself.

### Non-trivial Dependency:
- **Student_ID → Course**  
  This is a non-trivial dependency because `Course` is not part of `Student_ID`.

## Summary of Functional Dependencies:

| **Type**                      | **Definition**                                                                 | **Example**                                |
|-------------------------------|---------------------------------------------------------------------------------|--------------------------------------------|
| **Functional Dependency (FD)** | A relationship where one attribute determines another.                          | `Emp_Id → Emp_Name`                        |
| **Trivial Dependency**         | The dependent is a subset of the determinant or both are the same.              | `Employee_Id → Employee_Id`                |
| **Non-trivial Dependency**     | The dependent is not a subset of the determinant, and they are different.       | `Emp_Id → Emp_Name`                        |
| **Complete Non-trivial**       | No intersection between the determinant and the dependent (completely separate).| `Emp_Id → Emp_Address`                     |

## Key Points to Remember:
- Functional dependencies are crucial for understanding how attributes are related in a table.
- **Trivial dependencies** are obvious relationships (where an attribute determines itself).
- **Non-trivial dependencies** show meaningful relationships between different attributes.
- Proper understanding of functional dependencies helps with **database normalization**, which reduces redundancy and ensures data integrity.

