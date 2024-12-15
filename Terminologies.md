**Database Terminologies with Definitions and Examples**

---

### **1. Database**
- A collection of organized data that can be easily accessed, managed, and updated.
- **Example:** A school database storing student, teacher, and course information.

---

### **2. Table**
- A structure in a database that organizes data into rows and columns.
- **Example:** A `Students` table with columns: `StudentID`, `Name`, `Age`.

---

### **3. Row (Tuple)**
- A single record in a table.
- **Example:** `(1, 'Alice', 20)` is a tuple in the `Students` table.

---

### **4. Column (Attribute)**
- A field in a table that represents one type of data.
- **Example:** `Name` and `Age` are columns in the `Students` table.

---

### **5. Primary Key**
- A unique identifier for each row in a table.
- **Example:** `StudentID` in the `Students` table.

---

### **6. Foreign Key**
- A column in one table that links to the primary key in another table.
- **Example:** `CourseID` in the `Enrollments` table links to the `Courses` table.

---

### **7. Composite Key**
- A primary key made up of two or more columns to uniquely identify a row.
- **Example:** In a `Enrollments` table, `StudentID` and `CourseID` together can act as a composite key.

---

### **8. Candidate Key**
- A column or a set of columns that could be used as a primary key.
- **Example:** In a `Students` table, both `StudentID` and `Email` could be candidate keys.

---

### **9. Alternate Key**
- A candidate key that is not chosen as the primary key.
- **Example:** If `StudentID` is the primary key, `Email` becomes an alternate key.

---

### **10. Super Key**
- A set of one or more columns that uniquely identify a row in a table, including primary keys and candidate keys.
- **Example:** `StudentID` or `{StudentID, Name}` in the `Students` table.

---

### **11. Surrogate Key**
- A unique identifier for a row, often generated automatically by the system.
- **Example:** An auto-incremented `ID` column in a table.

---

### **12. Unique Key**
- Ensures that all values in a column are unique, but it can have one NULL value.
- **Example:** An `Email` column with a unique constraint in a `Users` table.

---

### **13. Schema**
- The structure of a database, including tables, columns, and their relationships.
- **Example:** A schema defining the `Students` and `Courses` tables and their relationship.

---

### **14. Query**
- A request to retrieve or manipulate data in a database.
- **Example:** `SELECT * FROM Students WHERE Age > 18;`

---

### **15. Index**
- A database optimization feature that speeds up data retrieval.
- **Example:** An index on the `Name` column in the `Students` table.

---

### **16. View**
- A virtual table based on a query result.
- **Example:** A view `AdultStudents` showing only students older than 18.

---

### **17. Transaction**
- A sequence of operations performed as a single logical unit.
- **Example:** Transferring money between accounts involves debiting one account and crediting another.

---

### **18. CRUD**
- The four basic operations: Create, Read, Update, Delete.
- **Example:** Adding a student, viewing their details, updating their age, or deleting their record.

---

### **19. Normalization**
- The process of organizing data to reduce redundancy.
- **Example:** Splitting a single table into `Students` and `Courses` to avoid duplicate course names.

---

### **20. Denormalization**
- The process of combining tables to improve read performance.
- **Example:** Merging `Students` and `Courses` for faster queries.

---

### **21. Relationship**
- The association between tables in a database.
- **Example:** `Students` and `Courses` are related through the `Enrollments` table.

---

### **22. One-to-One Relationship**
- A single row in one table is linked to a single row in another table.
- **Example:** One person has one passport.

---

### **23. One-to-Many Relationship**
- A single row in one table is linked to multiple rows in another table.
- **Example:** One teacher teaches many students.

---

### **24. Many-to-Many Relationship**
- Multiple rows in one table are linked to multiple rows in another table.
- **Example:** Students enroll in multiple courses, and courses have multiple students.

---

### **25. Stored Procedure**
- A reusable SQL code stored in the database.
- **Example:** A procedure to calculate the average age of students.

---

### **26. Trigger**
- An automatic action executed when a specific database event occurs.
- **Example:** Automatically logging changes when a record is updated.

---

### **27. Data Type**
- Specifies the type of data a column can hold.
- **Example:** `INT`, `VARCHAR`, `DATE`.

---

### **28. Constraints**
- Rules enforced on data in a table.
- **Example:** `NOT NULL`, `UNIQUE`, `FOREIGN KEY`.

---

### **29. Aggregate Function**
- Performs a calculation on multiple rows.
- **Example:** `AVG`, `SUM`, `COUNT`, `MAX`, `MIN`.

---

### **30. Join**
- Combines rows from two or more tables.
- **Example:** `SELECT S.Name, C.CourseName FROM Students S JOIN Enrollments E ON S.StudentID = E.StudentID;`

---

### **31. Backup**
- A copy of database data used for recovery.
- **Example:** Creating a backup of the `Students` table daily.

---

### **32. Data Warehouse**
- A system used for storing and analyzing large datasets.
- **Example:** A company analyzing customer purchases from multiple regions.

---

### **33. OLTP (Online Transaction Processing)**
- Focuses on transaction-oriented tasks.
- **Example:** A banking system handling deposits and withdrawals.

---

### **34. OLAP (Online Analytical Processing)**
- Focuses on complex queries for data analysis.
- **Example:** Analyzing sales trends over a year.

---

### **35. ACID Properties**
- Ensures reliable transactions: Atomicity, Consistency, Isolation, Durability.
- **Example:** Ensuring a money transfer completes fully or not at all.

---

### **36. Data Integrity**
- Ensures accuracy and consistency of data.
- **Example:** Ensuring `StudentID` is unique in the `Students` table.

---

