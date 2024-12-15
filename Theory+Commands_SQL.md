**Difference Between DBMS and RDBMS**

---

### **DBMS (Database Management System):**

1. **Definition:** DBMS is software used to store and manage data. It does not organize data into related tables.

2. **Key Feature:** It does not support relationships between tables. Each dataset is stored separately, making it harder to link data.

3. **Examples:**
   - Microsoft Access
   - FileMaker Pro
   - A simple file system like a text file or an Excel sheet where data is stored without relationships.

4. **Example in DBMS:**
   Imagine a library database:
   - **Books File**: Contains book details (e.g., Book Name, Author).
   - **Borrowers File**: Contains borrower details (e.g., Borrower Name, Date).

   However, there is no connection between these two files. You cannot easily determine which borrower has borrowed which book.

---

### **RDBMS (Relational Database Management System):**

1. **Definition:** RDBMS is a type of DBMS that organizes data into tables with rows and columns. These tables are related to each other, enabling structured queries.

2. **Key Features:**
   - Supports relationships between tables using primary keys and foreign keys.
   - Ensures data integrity and eliminates redundancy through normalization.
   - Allows multi-user access and transaction management.
   - Provides scalability and data security.

3. **Supported Languages:** RDBMS supports various programming languages for database interaction, including:
   - SQL (Structured Query Language)
   - PL/SQL (Procedural Language/SQL, used in Oracle)
   - T-SQL (Transact-SQL, used in Microsoft SQL Server).

4. **Examples of RDBMS Software:**
   - MySQL
   - PostgreSQL
   - Oracle Database
   - Microsoft SQL Server

5. **Software to Interact with RDBMS:** These tools, known as Database Management Tools or SQL Clients, allow users to interact with RDBMS:
   - phpMyAdmin
   - MySQL Workbench
   - pgAdmin (for PostgreSQL)
   - SQL Server Management Studio (SSMS for SQL Server)
   - Oracle SQL Developer (for Oracle Database)

6. **Example in RDBMS:**
   In the same library system:
   - **Books Table:** Stores book details (columns: BookID, Title, Author).
   - **Borrowers Table:** Stores borrower details (columns: BorrowerID, Name).
   - **Transactions Table:** Links the two tables with relationships using BorrowerID and BookID.

   With this structure, you can easily query:
   - "Which book did John borrow?"
   - "Who borrowed the book 'Harry Potter'?"

---

### **API Layer in RDBMS:**

RDBMS systems provide an API (Application Programming Interface) layer that allows users to interact with the database. When we write SQL queries, these queries are processed through the API layer. The API layer acts as a mediator, translating our requests into commands that the database can understand. It handles the interaction with the database to perform CRUD (Create, Read, Update, Delete) operations. This architecture ensures that the underlying database structure is abstracted, making it easier for developers to work with the data.

---

### **SQL (Structured Query Language):**

1. **Definition:** SQL is a standardized programming language used to interact with relational databases. It is used to perform tasks such as querying data, inserting records, updating existing data, and deleting records from a database.

2. **Key Features:**
   - Easy to learn and use.
   - Allows complex queries to retrieve specific data.
   - Provides commands for managing database structures and user access.

3. **Types of SQL Commands:**
   - **DDL (Data Definition Language):** Commands like `CREATE`, `ALTER`, `DROP` to define and manage database structures.
   - **DML (Data Manipulation Language):** Commands like `SELECT`, `INSERT`, `UPDATE`, `DELETE` to manipulate data.
   - **DCL (Data Control Language):** Commands like `GRANT`, `REVOKE` to control access.
   - **TCL (Transaction Control Language):** Commands like `COMMIT`, `ROLLBACK` to manage transactions.

4. **Example:**
   ```sql
   -- Create a table
   CREATE TABLE Books (
       BookID INT PRIMARY KEY,
       Title VARCHAR(100),
       Author VARCHAR(50)
   );

   -- Insert data into the table
   INSERT INTO Books (BookID, Title, Author)
   VALUES (1, 'Harry Potter', 'J.K. Rowling');

   -- Query data from the table
   SELECT * FROM Books;
   ```

   This example creates a table, inserts data, and retrieves it using SQL.

---

### **Creating an ER Diagram and Database:**

1. **Identify Entities:** List the main objects in the system (e.g., Students, Courses, Teachers).
2. **Define Relationships:** Determine how these entities are related (e.g., Students enroll in Courses).
3. **Draw the Diagram:** Use tools like Lucidchart or pen and paper to map entities, attributes, and relationships.
4. **Assign Keys:** Add primary keys to uniquely identify records in each entity.
5. **Add Cardinality:** Specify how many records in one entity relate to records in another.
   - **One-to-One:** Each record in Entity A relates to only one record in Entity B, and vice versa (e.g., one person has one passport).
   - **One-to-Many:** A single record in Entity A can relate to multiple records in Entity B (e.g., one teacher teaches many students).
   - **Many-to-One:** Multiple records in Entity A relate to a single record in Entity B (e.g., many students enrolled in one course).
   - **Many-to-Many:** Multiple records in Entity A can relate to multiple records in Entity B (e.g., students can enroll in multiple courses, and courses can have multiple students).
6. **Convert Entities to Tables:** Create tables for each entity, including their attributes as columns.
7. **Define Relationships in Tables:** Use foreign keys to establish connections between related tables.
8. **Normalize Data:** Remove redundancy by ensuring each table stores unique and relevant data.
9. **Create the Database:** Use SQL to create the database structure based on the ER diagram.
10. **Populate the Database:** Insert sample data into the tables to test the relationships and queries.

---

### **Example: Creating an ER Diagram and Converting to a Database**

**Scenario:** A university system needs to track students, courses, and enrollments.

1. **ER Diagram:**
   - **Entities:**
     - `Students` (StudentID, Name, Age)
     - `Courses` (CourseID, CourseName, Credits)
     - `Enrollments` (EnrollmentID, StudentID, CourseID)
   - **Relationships:**
     - `Students` enroll in `Courses` (Many-to-Many relationship).
   - **Diagram Representation:**
     - `Students` and `Courses` are linked through `Enrollments`.

2. **Database Tables:**
   ```sql
   -- Students Table
   CREATE TABLE Students (
       StudentID INT PRIMARY KEY,
       Name VARCHAR(100),
       Age INT
   );

   -- Courses Table
   CREATE TABLE Courses (
       CourseID INT PRIMARY KEY,
       CourseName VARCHAR(100),
       Credits INT
   );

   -- Enrollments Table
   CREATE TABLE Enrollments (
       EnrollmentID INT PRIMARY KEY,
       StudentID INT,
       CourseID INT,
       FOREIGN KEY (StudentID) REFERENCES Students(StudentID),
       FOREIGN KEY (CourseID) REFERENCES Courses(CourseID)
   );
   ```

3. **Populating Data:**
   ```sql
   -- Insert Students
   INSERT INTO Students (StudentID, Name, Age) VALUES (1, 'Alice', 20);
   INSERT INTO Students (StudentID, Name, Age) VALUES (2, 'Bob', 22);

   -- Insert Courses
   INSERT INTO Courses (CourseID, CourseName, Credits) VALUES (101, 'Math', 3);
   INSERT INTO Courses (CourseID, CourseName, Credits) VALUES (102, 'Science', 4);

   -- Insert Enrollments
   INSERT INTO Enrollments (EnrollmentID, StudentID, CourseID) VALUES (1, 1, 101);
   INSERT INTO Enrollments (EnrollmentID, StudentID, CourseID) VALUES (2, 2, 102);
   ```

This structure allows querying relationships like "Which courses is Alice enrolled in?" or "How many students are in the Math course?"

---

**MySQL: An Open-Source Database Management Tool**

---

### **Why MySQL is Preferred**

1. **Open Source:** MySQL is open-source, meaning its source code is freely available and can be modified to suit specific business needs.
2. **Cost-Effective:** Being open source, it is free to use, making it a popular choice for startups and enterprises.
3. **Flexibility:** Users can customize it to meet their application requirements, providing flexibility not always available with proprietary systems.
4. **Widely Supported:** It has a large community for support and frequent updates, making it reliable and robust.
5. **Cross-Platform:** MySQL works on various operating systems like Windows, Linux, and macOS.

---

### **Difference Between SQL and MySQL**

1. **Definition:**
   - **SQL:** Structured Query Language, a standard programming language for managing relational databases.
   - **MySQL:** A specific open-source relational database management system (RDBMS) that uses SQL for database interactions.

2. **Purpose:**
   - **SQL:** A language used to write queries for interacting with any relational database.
   - **MySQL:** A database management tool where SQL is used to manage data.

3. **Type:**
   - **SQL:** A language or syntax.
   - **MySQL:** A software or application.

4. **Installation:**
   - **SQL:** No installation required; it is a language.
   - **MySQL:** Needs installation as it is database software.

5. **Features:**
   - **SQL:** Only focuses on querying and managing data.
   - **MySQL:** Provides features like data storage, backup, replication, and multi-user access.

6. **Use Cases:**
   - **SQL:** Universal; works with various database management systems like MySQL, PostgreSQL, Oracle, and SQL Server.
   - **MySQL:** Specifically for managing databases using the MySQL RDBMS.

---

### **Tools to Work with MySQL**

1. **MySQL Workbench:** A graphical user interface (GUI) for database design, administration, and querying.
2. **phpMyAdmin:** A web-based tool for managing MySQL databases, often used with web hosting services.
3. **HeidiSQL:** A lightweight, open-source client for managing MySQL databases.
4. **DBeaver:** A universal database tool supporting MySQL and other RDBMS.
5. **Navicat:** A commercial database management tool for MySQL with advanced features like data modeling.

---

### **Advantages of Using MySQL**

1. **Ease of Use:** User-friendly with comprehensive documentation and community support.
2. **High Performance:** Optimized for read-heavy workloads and supports millions of rows in tables.
3. **Scalability:** Supports large-scale applications and can handle multiple databases on a single server.
4. **Security:** Provides strong data encryption and user access control features.
5. **Replication:** Supports master-slave replication for high availability and load balancing.

---

**CRUD Operations and How to Perform Them Using SQL**

---

### **What are CRUD Operations?**

CRUD stands for **Create, Read, Update, and Delete**, which are the four basic operations performed on databases. These operations are essential for managing and manipulating data.

1. **Create:** Add new records to a database.
2. **Read:** Retrieve existing data from a database.
3. **Update:** Modify existing records in a database.
4. **Delete:** Remove records from a database.

---

### **How to Perform CRUD Operations Using SQL**

#### **1. Create Operation**
   - Use the `INSERT` statement to add new records to a table.
   
   **Syntax:**
   ```sql
   INSERT INTO table_name (column1, column2, ...)
   VALUES (value1, value2, ...);
   ```

   **Example:**
   ```sql
   INSERT INTO Students (StudentID, Name, Age)
   VALUES (1, 'Alice', 20);
   ```
   This adds a new student named Alice with age 20 to the `Students` table.

#### **2. Read Operation**
   - Use the `SELECT` statement to retrieve data from a table.

   **Syntax:**
   ```sql
   SELECT column1, column2, ...
   FROM table_name
   WHERE condition;
   ```

   **Example:**
   ```sql
   SELECT * FROM Students;
   ```
   This retrieves all records and columns from the `Students` table.

   **Example with Condition:**
   ```sql
   SELECT Name, Age FROM Students WHERE Age > 18;
   ```
   This retrieves the names and ages of students older than 18.

#### **3. Update Operation**
   - Use the `UPDATE` statement to modify existing records in a table.

   **Syntax:**
   ```sql
   UPDATE table_name
   SET column1 = value1, column2 = value2, ...
   WHERE condition;
   ```

   **Example:**
   ```sql
   UPDATE Students
   SET Age = 21
   WHERE StudentID = 1;
   ```
   This updates the age of the student with `StudentID = 1` to 21.

#### **4. Delete Operation**
   - Use the `DELETE` statement to remove records from a table.

   **Syntax:**
   ```sql
   DELETE FROM table_name
   WHERE condition;
   ```

   **Example:**
   ```sql
   DELETE FROM Students
   WHERE StudentID = 1;
   ```
   This removes the record of the student with `StudentID = 1` from the `Students` table.

   **Caution:** Omitting the `WHERE` clause deletes all records from the table.
   ```sql
   DELETE FROM Students;
   ```

---

### **Combining CRUD Operations**

CRUD operations can be combined to manage the entire lifecycle of data. For example:
1. **Create:** Add a new student to the `Students` table.
2. **Read:** Retrieve the details of students aged above 20.
3. **Update:** Modify the age of a specific student.
4. **Delete:** Remove a student who has graduated.

---

### **Example Scenario**

#### **Table Creation**
```sql
CREATE TABLE Students (
   StudentID INT PRIMARY KEY,
   Name VARCHAR(100),
   Age INT
);
```

#### **CRUD Operations on the Students Table**
1. **Create:**
   ```sql
   INSERT INTO Students (StudentID, Name, Age)
   VALUES (1, 'Alice', 20);
   ```

2. **Read:**
   ```sql
   SELECT * FROM Students;
   ```

3. **Update:**
   ```sql
   UPDATE Students
   SET Age = 22
   WHERE StudentID = 1;
   ```

4. **Delete:**
   ```sql
   DELETE FROM Students
   WHERE StudentID = 1;
   ```

---

**SQL Data Types and Difference Between CHAR and VARCHAR**

---

### **SQL Data Types Table**

| **DATATYPE**   | **Description**                                    |
|----------------|--------------------------------------------------|
| **CHAR**       | (Fixed-length string, size 0-255 bytes. Takes the full 255 bytes, regardless of input size.) |
| **VARCHAR**    | (Variable-length string, size 0-255 bytes. Takes only the actual size of the input plus extra 1-2 bytes for length storage.) |
| **TINYTEXT**   | (String, size 0-255 bytes)                       |
| **TEXT**       | (String, size 0-65,535 bytes)                    |
| **BLOB**       | (Binary large object, size 0-65,535 bytes)       |
| **MEDIUMTEXT** | (String, size 0-16,777,215 bytes)                |
| **MEDIUMBLOB** | (Binary large object, size 0-16,777,215 bytes)   |
| **LONGTEXT**   | (String, size 0-4,294,967,295 bytes)             |
| **LONGBLOB**   | (Binary large object, size 0-4,294,967,295 bytes)|
| **TINYINT**    | (Integer range -128 to 127)                     |
| **SMALLINT**   | (Integer range -32,768 to 32,767)               |
| **MEDIUMINT**  | (Integer range -8,388,608 to 8,388,607)         |
| **INT**        | (Integer range -2,147,483,648 to 2,147,483,647) |
| **BIGINT**     | (Integer with a very large range)               |
| **FLOAT**      | (Decimal number with precision 0-23 digits)     |
| **DOUBLE**     | (Decimal number with precision 0-53 digits)     |

---

### **Difference Between CHAR and VARCHAR**

| **Feature**            | **CHAR**                          | **VARCHAR**                      |
|------------------------|----------------------------------|----------------------------------|
| **Storage**            | Fixed space, takes complete 255 bytes regardless of input size. | Takes actual word size + 1-2 bytes for length. |
| **Speed**              | Faster due to fixed size.         | Slower because size varies.       |
| **Example**            | If "CAT" is stored in CHAR(255), it takes full 255 bytes: `CAT__________________`. | If "CAT" is stored in VARCHAR(255), it takes only 3 + 1 = 4 bytes: `CAT`. |

---

### **Simple Explanation**
- **CHAR:** Reserves **fixed space** in memory for data, filling unused space up to its defined size.
  - **Example:** In CHAR(255), storing "CAT" uses the full 255 bytes: `CAT` with extra spaces.

- **VARCHAR:** Uses **variable space** based on the word length, adding 1-2 bytes for storage.
  - **Example:** In VARCHAR(255), storing "CAT" uses only 4 bytes (3 for `CAT` + 1 for length).
  - **Note:** For `VARCHAR(0-255)`, 1 byte is used to store the length. For `VARCHAR(>255)`, 2 bytes are used to store the length.

---

**SQL Data Types with Definitions and Examples**

---

### **1. DECIMAL**
- **Definition:** A fixed-point number stored as a string to ensure precision.
- **Example:** Store a product price with precision.

```sql
CREATE TABLE Products (
   Price DECIMAL(5,2)
);
INSERT INTO Products (Price) VALUES (19.99);
```
- **What data looks like:** `19.99`
- **Variable Initialization (SQL):**
```sql
DECLARE @price DECIMAL(5,2);
SET @price = 19.99;
```

---

### **2. DATE**
- **Definition:** Stores a date in `YYYY-MM-DD` format.
- **Example:** Store a birth date.

```sql
CREATE TABLE Employees (
   BirthDate DATE
);
INSERT INTO Employees (BirthDate) VALUES ('2000-05-15');
```
- **What data looks like:** `2000-05-15`
- **Variable Initialization (SQL):**
```sql
DECLARE @birthDate DATE;
SET @birthDate = '2000-05-15';
```

---

### **3. DATETIME**
- **Definition:** Stores date and time in `YYYY-MM-DD HH:MM:SS` format.
- **Example:** Store an event timestamp.

```sql
CREATE TABLE Events (
   EventTime DATETIME
);
INSERT INTO Events (EventTime) VALUES ('2024-06-15 14:30:00');
```
- **What data looks like:** `2024-06-15 14:30:00`
- **Variable Initialization (SQL):**
```sql
DECLARE @eventTime DATETIME;
SET @eventTime = '2024-06-15 14:30:00';
```

---

### **4. TIMESTAMP**
- **Definition:** Stores date and time automatically, often for logging.
- **Example:** Record last update time.

```sql
CREATE TABLE Logs (
   UpdateTime TIMESTAMP
);
INSERT INTO Logs (UpdateTime) VALUES (CURRENT_TIMESTAMP);
```
- **What data looks like:** `20240615143000` (formatted internally).
- **Variable Initialization (SQL):**
```sql
DECLARE @updateTime TIMESTAMP;
```
*Note: TIMESTAMP values are often system-generated.*

---

### **5. TIME**
- **Definition:** Stores only time in `HH:MM:SS` format.
- **Example:** Store a meeting duration.

```sql
CREATE TABLE Meetings (
   StartTime TIME
);
INSERT INTO Meetings (StartTime) VALUES ('10:30:00');
```
- **What data looks like:** `10:30:00`
- **Variable Initialization (SQL):**
```sql
DECLARE @startTime TIME;
SET @startTime = '10:30:00';
```

---

### **6. ENUM**
- **Definition:** Stores one value from a predefined list.
- **Example:** Specify gender.

```sql
CREATE TABLE Users (
   Gender ENUM('Male', 'Female', 'Other')
);
INSERT INTO Users (Gender) VALUES ('Male');
```
- **What data looks like:** `Male`
- **Variable Initialization (SQL):**
```sql
DECLARE @gender ENUM('Male', 'Female', 'Other');
SET @gender = 'Male';
```

---

### **7. SET**
- **Definition:** Stores multiple values from a predefined list.
- **Example:** Select multiple skills for a user.

```sql
CREATE TABLE UserSkills (
   Skills SET('Java', 'Python', 'SQL')
);
INSERT INTO UserSkills (Skills) VALUES ('Java,SQL');
```
- **What data looks like:** `Java,SQL`
- **Variable Initialization (SQL):**
```sql
DECLARE @skills SET('Java', 'Python', 'SQL');
SET @skills = 'Java,SQL';
```

---

### **8. BOOLEAN**
- **Definition:** Stores true/false values as `1` (true) or `0` (false).
- **Example:** Specify if an account is active.

```sql
CREATE TABLE Accounts (
   IsActive BOOLEAN
);
INSERT INTO Accounts (IsActive) VALUES (1);
```
- **What data looks like:** `1` (for true), `0` (for false)
- **Variable Initialization (SQL):**
```sql
DECLARE @isActive BOOLEAN;
SET @isActive = 1;
```

---

### **9. BIT**
- **Definition:** Stores values in binary format, up to 64 bits.
- **Example:** Track user preferences with flags.

```sql
CREATE TABLE Preferences (
   Settings BIT(3)
);
INSERT INTO Preferences (Settings) VALUES (5);
```
- **What data looks like:** `101` (binary representation of 5).
- **Variable Initialization (SQL):**
```sql
DECLARE @settings BIT(3);
SET @settings = 5;
```

**SQL Commands: Full Example with Explanations**

---

### **1. DDL (Data Definition Language): Defining the Schema**

#### **1.1 CREATE: Create a Database and Table**
- **Explanation:** Create a new database and a table to store employee records.

**Syntax 1:**
```sql
-- Create a new database named 'CompanyDB'
CREATE DATABASE CompanyDB;

-- Use the created database
USE CompanyDB;

-- Create a table named 'Employees' with basic columns
CREATE TABLE Employees (
    EmpID INT PRIMARY KEY,       -- Unique ID for each employee
    Name VARCHAR(50),            -- Name of the employee
    Age INT,                     -- Age of the employee
    Department VARCHAR(50)       -- Employee department
);
```

**Syntax 2:** Combined CREATE DATABASE and USE (Alternate Syntax)
```sql
CREATE DATABASE IF NOT EXISTS CompanyDB;
USE CompanyDB;
```

---

#### **1.2 ALTER TABLE: Modify Table Structure**
- **Explanation:** Add a new column `Salary` to the `Employees` table.

**Syntax 1:**
```sql
-- Add a new column 'Salary' to the Employees table
ALTER TABLE Employees
ADD Salary DECIMAL(10,2);
```

**Syntax 2:** Add Multiple Columns at Once
```sql
-- Add multiple new columns to Employees table
ALTER TABLE Employees
ADD Salary DECIMAL(10,2),
ADD JoiningDate DATE;
```

---

#### **1.3 DROP: Delete the Table**
- **Explanation:** Drop the `Employees` table (use with caution).

**Syntax 1:**
```sql
-- Drop the Employees table
DROP TABLE Employees;
```

**Syntax 2:** Drop Table if it Exists
```sql
-- Drop the Employees table if it exists
DROP TABLE IF EXISTS Employees;
```

---

#### **1.4 TRUNCATE: Remove All Data**
- **Explanation:** Remove all rows (data) from the `Employees` table without deleting its structure.

**Syntax:**
```sql
-- Truncate all records from Employees table
TRUNCATE TABLE Employees;
```

---

#### **1.5 RENAME: Rename Table**
- **Explanation:** Rename the `Employees` table to `Staff`.

**Syntax:**
```sql
-- Rename Employees table to Staff
RENAME TABLE Employees TO Staff;
```

---

### **2. DRL/DQL (Data Query Language): Retrieve Data**

#### **SELECT: Retrieve Data**
- **Explanation:** Fetch data from the table using the `SELECT` statement.

**Syntax 1:**
```sql
-- Select all columns from the Employees table
SELECT * FROM Employees;

-- Select specific columns
SELECT Name, Department, Salary FROM Employees;
```

**Syntax 2:** Using Aliases
```sql
-- Select with aliases for table and column names
SELECT E.Name AS EmployeeName, E.Salary AS EmployeeSalary
FROM Employees AS E;
```

---

### **3. DML (Data Manipulation Language): Modify Data**

#### **3.1 INSERT: Add Data to Table**
- **Explanation:** Add new records to the `Employees` table.

**Syntax 1:**
```sql
-- Insert data into Employees table specifying column names
INSERT INTO Employees (EmpID, Name, Age, Department, Salary)
VALUES (1, 'John Doe', 30, 'HR', 50000.00);
```

**Syntax 2:**
```sql
-- Insert data into all columns without specifying column names
INSERT INTO Employees
VALUES (2, 'Jane Smith', 25, 'IT', 60000.00);
```

---

#### **3.2 UPDATE: Update Data in Table**
- **Explanation:** Update the salary of a specific employee.

**Syntax 1:**
```sql
-- Update the salary of John Doe to 55000.00
UPDATE Employees
SET Salary = 55000.00
WHERE EmpID = 1;
```

**Syntax 2:** Update Multiple Columns
```sql
-- Update salary and department for a specific employee
UPDATE Employees
SET Salary = 60000.00, Department = 'Finance'
WHERE EmpID = 1;
```

---

#### **3.3 DELETE: Remove Specific Data**
- **Explanation:** Delete a specific record from the `Employees` table.

**Syntax 1:**
```sql
-- Delete the record of Jane Smith
DELETE FROM Employees
WHERE EmpID = 2;
```

**Syntax 2:** Delete All Records
```sql
-- Delete all records from the Employees table
DELETE FROM Employees;
```

---

### **4. DCL (Data Control Language): Manage User Permissions**

#### **4.1 GRANT: Provide Access**
- **Explanation:** Grant `SELECT` permission to a user named `user1`.

**Syntax:**
```sql
-- Grant SELECT privilege to user1
GRANT SELECT ON Employees TO 'user1';
```

---

#### **4.2 REVOKE: Remove Access**
- **Explanation:** Revoke `SELECT` permission from `user1`.

**Syntax:**
```sql
-- Revoke SELECT privilege from user1
REVOKE SELECT ON Employees FROM 'user1';
```

---

### **5. TCL (Transaction Control Language): Manage Transactions**

#### **5.1 START TRANSACTION: Begin a Transaction**
- **Explanation:** Start a new transaction to modify data safely.

**Syntax:**
```sql
-- Start a transaction
START TRANSACTION;
```

---

#### **5.2 COMMIT: Save Changes**
- **Explanation:** Save all changes made during the transaction.

**Syntax:**
```sql
-- Commit the changes to the database
COMMIT;
```

---

#### **5.3 ROLLBACK: Undo Changes**
- **Explanation:** Revert changes made during the current transaction.

**Syntax:**
```sql
-- Rollback changes if an error occurs
ROLLBACK;
```

---

#### **5.4 SAVEPOINT: Create a Checkpoint**
- **Explanation:** Set a point within a transaction to roll back to later.

**Syntax:**
```sql
-- Set a savepoint after inserting data
SAVEPOINT BeforeUpdate;

-- Update the table
UPDATE Employees
SET Salary = 60000.00
WHERE EmpID = 1;

-- Rollback to the savepoint if needed
ROLLBACK TO BeforeUpdate;
```

---

### **Full Summary of Operations in Sequence**
1. **CREATE**: Created the `CompanyDB` database and `Employees` table.
2. **ALTER TABLE**: Added a new column `Salary`.
3. **DROP**: Dropped the table (optional for understanding).
4. **TRUNCATE**: Removed all data without deleting the table.
5. **RENAME**: Renamed the table to `Staff`.
6. **SELECT**: Retrieved data using queries (including aliases).
7. **INSERT**: Inserted new records with and without column names.
8. **UPDATE**: Updated specific data and multiple columns.
9. **DELETE**: Deleted specific and all records.
10. **GRANT/REVOKE**: Managed permissions for a user.
11. **TCL Commands**: 
    - Began a transaction (`START TRANSACTION`).
    - Saved changes (`COMMIT`).
    - Undid changes (`ROLLBACK`).
    - Set a checkpoint (`SAVEPOINT`).

---

### **Key Notes**
- Use `COMMIT` to save changes permanently.
- Use `ROLLBACK` to undo changes during errors.
- Always test commands on a development database first to avoid data loss.

---

**SQL Operations Example for DRL Commands**

---

### **Step 1: Syntax for SELECT Statement**
- **Explanation:** Use the SELECT statement to retrieve specific data from a table.

```sql
-- Select specific columns from the Customers table
SELECT Name, Age FROM Customers;

-- Select all columns
SELECT * FROM Customers;
```

**Expected Output:**
- The first query will show only the `Name` and `Age` columns.
- The second query will display all data in the table.

**Output:**
1. For `SELECT Name, Age FROM Customers`:
```
+------------+-----+
| Name       | Age |
+------------+-----+
| John Doe   | 28  |
| Jane Smith | 35  |
| Ali Khan   | 40  |
| Emma Watson| 25  |
| Sara Lee   | 50  |
+------------+-----+
```
2. For `SELECT * FROM Customers`:
```
+------------+------------+-----+----------+-------------+
| CustomerID | Name       | Age | Country  | prime_status|
+------------+------------+-----+----------+-------------+
| 1          | John Doe   | 28  | USA      | 1           |
| 2          | Jane Smith | 35  | Canada   | 0           |
| 3          | Ali Khan   | 40  | Pakistan | 1           |
| 4          | Emma Watson| 25  | NULL     | 0           |
| 5          | Sara Lee   | 50  | UK       | 1           |
+------------+------------+-----+----------+-------------+
```

---

### **Step 2: Order of Execution (RIGHT to LEFT)**
- **Explanation:** SQL executes expressions or calculations logically.

```sql
-- Example of an expression SELECT query without a FROM clause
SELECT 55 + 11;
```

**Expected Output:**
- The output will show the result of the addition.

**Output:**
```
+--------+
| 55 + 11|
+--------+
| 66     |
+--------+
```

---

### **Step 3: SELECT without FROM Clause (DUAL Table)**
- **Explanation:** Use DUAL tables for dummy operations like calculations or function calls.

```sql
-- Perform calculations
SELECT 55 + 11;

-- Get the current date and time
SELECT NOW();

-- Convert text to uppercase
SELECT UCASE('hello');
```

**Expected Output:**
1. For `SELECT 55 + 11`:
```
+--------+
| 55 + 11|
+--------+
| 66     |
+--------+
```
2. For `SELECT NOW()`:
```
+---------------------+
| NOW()               |
+---------------------+
| 2024-06-15 12:00:00 |
+---------------------+
```
3. For `SELECT UCASE('hello')`:
```
+---------+
| UCASE   |
+---------+
| HELLO   |
+---------+
```

---

### **Step 4: WHERE Clause**
- **Explanation:** Filter rows based on specific conditions.

```sql
-- Retrieve customers older than 30
SELECT * FROM Customers WHERE Age > 30;

-- Retrieve prime customers
SELECT * FROM Customers WHERE prime_status = 1;
```

**Expected Output:**
1. Customers older than 30:
```
+------------+------------+-----+----------+-------------+
| CustomerID | Name       | Age | Country  | prime_status|
+------------+------------+-----+----------+-------------+
| 2          | Jane Smith | 35  | Canada   | 0           |
| 3          | Ali Khan   | 40  | Pakistan | 1           |
| 5          | Sara Lee   | 50  | UK       | 1           |
+------------+------------+-----+----------+-------------+
```
2. Prime customers:
```
+------------+------------+-----+----------+-------------+
| CustomerID | Name       | Age | Country  | prime_status|
+------------+------------+-----+----------+-------------+
| 1          | John Doe   | 28  | USA      | 1           |
| 3          | Ali Khan   | 40  | Pakistan | 1           |
| 5          | Sara Lee   | 50  | UK       | 1           |
+------------+------------+-----+----------+-------------+
```

---

### **Step 5: BETWEEN Operator**
- **Explanation:** Retrieve rows with column values in a specified range.

```sql
-- Retrieve customers with Age between 30 and 50
SELECT * FROM Customers WHERE Age BETWEEN 30 AND 50;
```

**Expected Output:**
```
+------------+------------+-----+----------+-------------+
| CustomerID | Name       | Age | Country  | prime_status|
+------------+------------+-----+----------+-------------+
| 2          | Jane Smith | 35  | Canada   | 0           |
| 3          | Ali Khan   | 40  | Pakistan | 1           |
+------------+------------+-----+----------+-------------+
```

---


### **Step 6: IN Operator**
- **Explanation:** Simplify multiple `OR` conditions to filter rows.

```sql
-- Retrieve customers from specific countries (USA, UK, and Canada)
SELECT * FROM Customers WHERE Country IN ('USA', 'UK', 'Canada');
```

**Expected Output:**
- The query will return all customers whose country is USA, UK, or Canada.

**Output:**
```
+------------+------------+-----+----------+-------------+
| CustomerID | Name       | Age | Country  | prime_status|
+------------+------------+-----+----------+-------------+
| 1          | John Doe   | 28  | USA      | 1           |
| 2          | Jane Smith | 35  | Canada   | 0           |
| 5          | Sara Lee   | 50  | UK       | 1           |
+------------+------------+-----+----------+-------------+
```

---

### **Step 7: AND, OR, NOT Operators**
- **Explanation:** Combine logical conditions to filter data effectively.

```sql
-- Retrieve customers older than 30 AND from Pakistan
SELECT * FROM Customers WHERE Age > 30 AND Country = 'Pakistan';

-- Retrieve customers who are NOT prime members
SELECT * FROM Customers WHERE prime_status = 0;

-- Retrieve customers who are from Canada OR UK
SELECT * FROM Customers WHERE Country = 'Canada' OR Country = 'UK';
```

**Expected Output:**
1. **Customers older than 30 AND from Pakistan:**
```
+------------+------------+-----+----------+-------------+
| CustomerID | Name       | Age | Country  | prime_status|
+------------+------------+-----+----------+-------------+
| 3          | Ali Khan   | 40  | Pakistan | 1           |
+------------+------------+-----+----------+-------------+
```

2. **Customers who are NOT prime members:**
```
+------------+--------------+-----+----------+-------------+
| CustomerID | Name         | Age | Country  | prime_status|
+------------+--------------+-----+----------+-------------+
| 2          | Jane Smith   | 35  | Canada   | 0           |
| 4          | Emma Watson  | 25  | NULL     | 0           |
+------------+--------------+-----+----------+-------------+
```

3. **Customers from Canada OR UK:**
```
+------------+------------+-----+----------+-------------+
| CustomerID | Name       | Age | Country  | prime_status|
+------------+------------+-----+----------+-------------+
| 2          | Jane Smith | 35  | Canada   | 0           |
| 5          | Sara Lee   | 50  | UK       | 1           |
+------------+------------+-----+----------+-------------+
```

---

### **Step 8: IS NULL Condition**
- **Explanation:** Retrieve rows where specific column values are NULL.

```sql
-- Retrieve customers where the Country is NULL
SELECT * FROM Customers WHERE Country IS NULL;
```

**Expected Output:**
- The query will return customers where the `Country` column has a NULL value.

**Output:**
```
+------------+--------------+-----+---------+-------------+
| CustomerID | Name         | Age | Country | prime_status|
+------------+--------------+-----+---------+-------------+
| 4          | Emma Watson  | 25  | NULL    | 0           |
+------------+--------------+-----+---------+-------------+
```

---

### **Step 9: Pattern Searching with LIKE Operator**
- **Explanation:** Use `LIKE` with wildcards (`%` for multiple characters, `_` for single character) to match patterns.

```sql
-- Retrieve customers whose names start with 'J'
SELECT * FROM Customers WHERE Name LIKE 'J%';

-- Retrieve customers whose names end with 'n'
SELECT * FROM Customers WHERE Name LIKE '%n';

-- Retrieve customers whose names have 'a' as the second character
SELECT * FROM Customers WHERE Name LIKE '_a%';
```

**Expected Output:**
1. **Names starting with 'J':**
```
+------------+------------+-----+----------+-------------+
| CustomerID | Name       | Age | Country  | prime_status|
+------------+------------+-----+----------+-------------+
| 1          | John Doe   | 28  | USA      | 1           |
| 2          | Jane Smith | 35  | Canada   | 0           |
+------------+------------+-----+----------+-------------+
```

2. **Names ending with 'n':**
```
+------------+------------+-----+----------+-------------+
| CustomerID | Name       | Age | Country  | prime_status|
+------------+------------+-----+----------+-------------+
| 3          | Ali Khan   | 40  | Pakistan | 1           |
+------------+------------+-----+----------+-------------+
```

3. **Names with 'a' as the second character:**
```
+------------+------------+-----+----------+-------------+
| CustomerID | Name       | Age | Country  | prime_status|
+------------+------------+-----+----------+-------------+
| 3          | Ali Khan   | 40  | Pakistan | 1           |
| 5          | Sara Lee   | 50  | UK       | 1           |
+------------+------------+-----+----------+-------------+
```

---

### **Step 10: ORDER BY Clause**
- **Explanation:** Sort query results in ascending (`ASC`) or descending (`DESC`) order.

```sql
-- Retrieve all customers sorted by Age in descending order
SELECT * FROM Customers ORDER BY Age DESC;

-- Retrieve all customers sorted by Name in ascending order
SELECT * FROM Customers ORDER BY Name ASC;

-- Retrieve all customers sorted by Country in descending order
SELECT * FROM Customers ORDER BY Country DESC;
```

**Expected Output:**
1. **Sorted by Age (DESC):**
- The output will show customers sorted from oldest to youngest.
```
+------------+------------+-----+----------+-------------+
| CustomerID | Name       | Age | Country  | prime_status|
+------------+------------+-----+----------+-------------+
| 5          | Sara Lee   | 50  | UK       | 1           |
| 3          | Ali Khan   | 40  | Pakistan | 1           |
| 2          | Jane Smith | 35  | Canada   | 0           |
| 1          | John Doe   | 28  | USA      | 1           |
| 4          | Emma Watson| 25  | NULL     | 0           |
+------------+------------+-----+----------+-------------+
```

2. **Sorted by Name (ASC):**
- Names are sorted alphabetically in ascending order (A-Z).
```
+------------+------------+-----+----------+-------------+
| CustomerID | Name       | Age | Country  | prime_status|
+------------+------------+-----+----------+-------------+
| 3          | Ali Khan   | 40  | Pakistan | 1           |
| 4          | Emma Watson| 25  | NULL     | 0           |
| 2          | Jane Smith | 35  | Canada   | 0           |
| 1          | John Doe   | 28  | USA      | 1           |
| 5          | Sara Lee   | 50  | UK       | 1           |
+------------+------------+-----+----------+-------------+
```

3. **Sorted by Country (DESC):**
- Strings are sorted in reverse alphabetical order (Z-A), and NULL comes last.
```
+------------+------------+-----+----------+-------------+
| CustomerID | Name       | Age | Country  | prime_status|
+------------+------------+-----+----------+-------------+
| 5          | Sara Lee   | 50  | UK       | 1           |
| 1          | John Doe   | 28  | USA      | 1           |
| 3          | Ali Khan   | 40  | Pakistan | 1           |
| 2          | Jane Smith | 35  | Canada   | 0           |
| 4          | Emma Watson| 25  | NULL     | 0           |
+------------+------------+-----+----------+-------------+
```

---

### **Step 11: GROUP BY Clause**
- **Explanation:** Group rows based on column values and use aggregate functions to summarize data.

```sql
-- Count the number of customers from each country
SELECT Country, COUNT(*) AS Total_Customers
FROM Customers
GROUP BY Country;

-- Find the average age of customers in each country
SELECT Country, AVG(Age) AS Average_Age
FROM Customers
GROUP BY Country;
```

**Expected Output:**
1. **Count of customers grouped by Country:**
```
+----------+----------------+
| Country  | Total_Customers|
+----------+----------------+
| USA      | 1              |
| Canada   | 1              |
| Pakistan | 1              |
| NULL     | 1              |
| UK       | 1              |
+----------+----------------+
```
2. **Average age of customers in each Country:**
```
+----------+-------------+
| Country  | Average_Age |
+----------+-------------+
| USA      | 28.00       |
| Canada   | 35.00       |
| Pakistan | 40.00       |
| NULL     | 25.00       |
| UK       | 50.00       |
+----------+-------------+
```

---

### **Step 12: DISTINCT Clause**
- **Explanation:** Retrieve unique values from a specified column.

```sql
-- Retrieve unique countries from the Customers table
SELECT DISTINCT Country FROM Customers;
```

**Expected Output:**
- Unique country names from the table:
```
+----------+
| Country  |
+----------+
| USA      |
| Canada   |
| Pakistan |
| NULL     |
| UK       |
+----------+
```

---

### **Step 13: GROUP BY with HAVING Clause**
- **Explanation:** Filter grouped results based on a condition. `HAVING` works like `WHERE`, but on aggregated data.

```sql
-- Retrieve countries with more than 1 customer
SELECT Country, COUNT(*) AS Total_Customers
FROM Customers
GROUP BY Country
HAVING COUNT(*) > 1;

-- Find countries where the average age of customers is greater than 30
SELECT Country, AVG(Age) AS Average_Age
FROM Customers
GROUP BY Country
HAVING AVG(Age) > 30;
```

**Expected Output:**
1. **Countries with more than 1 customer:**
- Since no country has more than one customer, the result will be:
```
Empty set (No records found)
```

2. **Countries where average age > 30:**
```
+----------+-------------+
| Country  | Average_Age |
+----------+-------------+
| Canada   | 35.00       |
| Pakistan | 40.00       |
| UK       | 50.00       |
+----------+-------------+
```

---

### **Step 14: WHERE vs HAVING**
- **Explanation:** `WHERE` filters rows **before grouping**, while `HAVING` filters **after grouping**.

```sql
-- Use WHERE to filter rows before grouping
SELECT Country, COUNT(*) AS Total_Customers
FROM Customers
WHERE Age > 30
GROUP BY Country;

-- Use HAVING to filter after grouping
SELECT Country, COUNT(*) AS Total_Customers
FROM Customers
GROUP BY Country
HAVING COUNT(*) > 0;
```

**Expected Output:**
1. **WHERE clause filtering before GROUP BY:**
- Rows where Age > 30 are grouped by country:
```
+----------+----------------+
| Country  | Total_Customers|
+----------+----------------+
| Canada   | 1              |
| Pakistan | 1              |
| UK       | 1              |
+----------+----------------+
```

2. **HAVING clause filtering after GROUP BY:**
- All groups are retained because the condition `COUNT(*) > 0` is true for all:
```
+----------+----------------+
| Country  | Total_Customers|
+----------+----------------+
| USA      | 1              |
| Canada   | 1              |
| Pakistan | 1              |
| NULL     | 1              |
| UK       | 1              |
+----------+----------------+
```

---



### **Summary of Steps**
1. **GROUP BY:** Groups rows based on column values and performs aggregation.
2. **DISTINCT:** Retrieves unique values.
3. **HAVING:** Filters aggregated results after grouping.
4. **WHERE vs HAVING:** WHERE filters rows before grouping; HAVING filters after grouping.

This concludes the complete set of SQL operations for DRL commands with practical examples and outputs for clarity.

---

**Understanding Primary Key, Foreign Key, Candidate Key, and Other Important Keys**

---

### **1. Primary Key**
- **Definition:** A primary key is a column (or set of columns) that uniquely identifies each row in a table. It ensures that no two rows have the same value for the primary key column, and it cannot contain NULL values.

**Real-Life Example:**
Consider a `Students` table in a school database:

| StudentID | Name       | Age | Class |
|-----------|------------|-----|-------|
| 1         | John Doe   | 14  | 9     |
| 2         | Jane Smith | 13  | 8     |
| 3         | Ali Khan   | 15  | 10    |

- Here, `StudentID` is the **Primary Key** because it uniquely identifies each student. No two students can have the same `StudentID`, and it cannot be left blank.

**Two Ways to Declare a Primary Key:**

**Way 1: Inline Primary Key Declaration**
```sql
CREATE TABLE Students (
    StudentID INT PRIMARY KEY,   -- Primary Key declared inline
    Name VARCHAR(50),
    Age INT,
    Class INT
);
```

**Way 2: Table-Level Primary Key Declaration**
```sql
CREATE TABLE Students (
    StudentID INT,       -- Column defined without primary key constraint initially
    Name VARCHAR(50),
    Age INT,
    Class INT,
    PRIMARY KEY (StudentID)  -- Table-level primary key declaration
);
```

Both methods produce the same result; you can choose either approach.

---

### **2. Foreign Key**
- **Definition:** A foreign key is a column (or set of columns) in one table that establishes a relationship with the primary key of another table. It allows linking the data between tables.

**Real-Life Example:**
Consider two tables in a school database:

**`Students` Table:**
| StudentID | Name       | Age | Class |
|-----------|------------|-----|-------|
| 1         | John Doe   | 14  | 9     |
| 2         | Jane Smith | 13  | 8     |
| 3         | Ali Khan   | 15  | 10    |

**`Marks` Table:**
| MarksID | StudentID | Subject  | Marks |
|---------|-----------|----------|-------|
| 101     | 1         | Math     | 85    |
| 102     | 2         | Science  | 90    |
| 103     | 3         | English  | 88    |

- Here, `StudentID` in the `Marks` table is the **Foreign Key** because it refers to the `StudentID` primary key in the `Students` table.
- This links each mark entry to a specific student.

**SQL Example:**
```sql
CREATE TABLE Marks (
    MarksID INT PRIMARY KEY,
    StudentID INT,
    Subject VARCHAR(50),
    Marks INT,
    FOREIGN KEY (StudentID) REFERENCES Students(StudentID)
);
```

---

### **3. Candidate Key**
- **Definition:** A candidate key is any column (or combination of columns) that can uniquely identify rows in a table. From these candidate keys, one is chosen as the primary key.

**Real-Life Example:**
Consider an `Employees` table in a company database:

| EmployeeID | SSN         | Name       | Department |
|------------|-------------|------------|------------|
| 101        | 123-45-6789 | John Smith | HR         |
| 102        | 987-65-4321 | Jane Doe   | IT         |
| 103        | 456-78-9012 | Ali Khan   | Finance    |

- Both `EmployeeID` and `SSN` are **Candidate Keys** because both can uniquely identify employees.
- Typically, one of these is chosen as the **Primary Key** (e.g., `EmployeeID`).

**SQL Example:**
```sql
CREATE TABLE Employees (
    EmployeeID INT,        -- Candidate Key 1
    SSN VARCHAR(11),       -- Candidate Key 2
    Name VARCHAR(50),
    Department VARCHAR(50),
    PRIMARY KEY (EmployeeID)
);
```

---

### **4. Alternate Key**
- **Definition:** An alternate key is any candidate key that is not chosen as the primary key.

**Real-Life Example:**
From the `Employees` table above, if `EmployeeID` is the primary key, then `SSN` becomes the **Alternate Key**.

**SQL Example:**
```sql
CREATE TABLE Employees (
    EmployeeID INT PRIMARY KEY,  -- Chosen Primary Key
    SSN VARCHAR(11) UNIQUE,      -- Alternate Key
    Name VARCHAR(50),
    Department VARCHAR(50)
);
```

---

### **5. Composite Key**
- **Definition:** A composite key is a key that consists of two or more columns to uniquely identify rows in a table.

**Real-Life Example:**
Consider a `Course_Enrollment` table in a university database:

| StudentID | CourseID | EnrollmentDate |
|-----------|----------|----------------|
| 1         | C101     | 2024-01-15     |
| 2         | C102     | 2024-01-16     |
| 1         | C102     | 2024-01-17     |

- Here, `StudentID` and `CourseID` together form the **Composite Key** because a student can enroll in multiple courses, but the combination of `StudentID` and `CourseID` is unique.

**SQL Example:**
```sql
CREATE TABLE Course_Enrollment (
    StudentID INT,
    CourseID VARCHAR(10),
    EnrollmentDate DATE,
    PRIMARY KEY (StudentID, CourseID)  -- Composite Key
);
```

---

### **6. Super Key**
- **Definition:** A super key is a set of one or more columns that can uniquely identify rows in a table. A super key includes the primary key but can also include additional columns.

**Real-Life Example:**
In the `Employees` table:
| EmployeeID | SSN         | Name       | Department |
|------------|-------------|------------|------------|

- `EmployeeID` alone is a super key.
- `(EmployeeID, Name)` is also a super key because it still uniquely identifies rows, even with an extra column.

**Note:** Super keys are not minimal. Candidate keys are derived by removing unnecessary columns from super keys.

**SQL Example:**
- Super keys are not directly implemented but exist conceptually during table design.

---

### **Summary of Keys in Databases**

| **Key Type**       | **Definition**                                                    | **Example**                       |
|---------------------|------------------------------------------------------------------|-----------------------------------|
| **Primary Key**     | Uniquely identifies rows in a table, cannot be NULL.             | `StudentID` in `Students` table.  |
| **Foreign Key**     | Establishes relationships between tables.                       | `StudentID` in `Marks` table.     |
| **Candidate Key**   | Columns that can uniquely identify rows (potential primary key).| `EmployeeID` and `SSN`.           |
| **Alternate Key**   | A candidate key not chosen as the primary key.                  | `SSN` in `Employees`.             |
| **Composite Key**   | A combination of columns that uniquely identifies rows.         | `(StudentID, CourseID)` in `Course_Enrollment`. |
| **Super Key**       | A set of columns that uniquely identify rows (not minimal).     | `(EmployeeID, Name)`.             |

---

### **Why Keys are Important in Databases?**
1. **Uniqueness:** Ensure that each row is uniquely identifiable.
2. **Data Integrity:** Maintain consistent and accurate data across tables.
3. **Relationships:** Enable linking of data between multiple tables.
4. **Efficiency:** Improve query performance with indexing on keys.

---

