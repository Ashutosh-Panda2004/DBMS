**Rules for Writing SQL Queries**

---

### **Best Practices for Writing SQL Queries**

When writing SQL queries, it is important to follow a consistent style to make the queries readable and maintainable. Below are the essential rules and best practices for writing structured query language (SQL):

---

### **1. Use Uppercase for SQL Keywords**
   - Always write SQL keywords like `SELECT`, `FROM`, `WHERE`, `INSERT`, `UPDATE`, etc., in uppercase to distinguish them from table names and columns.

   **Example:**
   ```sql
   SELECT Name, Age FROM Students WHERE Age > 18;
   ```

---

### **2. Use Proper Indentation**
   - Use indentation to structure queries clearly, especially when dealing with multiple clauses or nested queries.

   **Example:**
   ```sql
   SELECT Name, Age
   FROM Students
   WHERE Age > 18
   ORDER BY Name;
   ```

---

### **3. Use Table and Column Aliases Meaningfully**
   - Use aliases (`AS`) to shorten long table or column names while keeping them meaningful.

   **Example:**
   ```sql
   SELECT S.Name AS StudentName, C.CourseName
   FROM Students AS S
   JOIN Courses AS C ON S.CourseID = C.CourseID;
   ```

---

### **4. Use Single Quotes for String Literals**
   - Use single quotes (`'`) for string values, not double quotes.

   **Example:**
   ```sql
   SELECT * FROM Students WHERE Name = 'Alice';
   ```

---

### **5. Use Comments for Clarity**
   - Add comments to explain complex queries or logic.
   - Use `--` for single-line comments and `/* */` for multi-line comments.

   **Example:**
   ```sql
   -- Fetch all students older than 18
   SELECT Name, Age FROM Students WHERE Age > 18;

   /*
   Get all students who are enrolled in the 'Math' course.
   */
   SELECT S.Name
   FROM Students AS S
   JOIN Enrollments AS E ON S.StudentID = E.StudentID
   WHERE E.CourseName = 'Math';
   ```

---

### **6. Write Keywords on Separate Lines**
   - For better readability, write SQL keywords like `SELECT`, `FROM`, `WHERE`, `JOIN` on separate lines.

   **Example:**
   ```sql
   SELECT Name, Age
   FROM Students
   WHERE Age > 18
   ORDER BY Name;
   ```

---

### **7. Avoid Using SELECT ***
   - Instead of `SELECT *`, specify the columns you need to improve performance and readability.

   **Example:**
   ```sql
   -- Avoid this:
   SELECT * FROM Students;

   -- Use this:
   SELECT Name, Age FROM Students;
   ```

---

### **8. Use Consistent Naming Conventions**
   - Use snake_case or PascalCase consistently for table and column names.

   **Example:**
   ```sql
   CREATE TABLE student_courses (
       StudentID INT,
       CourseName VARCHAR(100)
   );
   ```

---

### **9. Avoid Hardcoding Values in Queries**
   - Use parameters or variables instead of hardcoded values to improve flexibility.

   **Example:**
   ```sql
   SELECT * FROM Students WHERE Age = @age;
   ```

---

### **10. Test Queries Before Execution**
   - Always test queries on a development or test environment to avoid accidental data loss or corruption.

   **Example:**
   ```sql
   -- Test the DELETE query
   SELECT * FROM Students WHERE StudentID = 1;

   -- Then execute the actual DELETE
   DELETE FROM Students WHERE StudentID = 1;
   ```

---

### **Summary Example**

Combining the rules, here is a well-structured query:

```sql
-- Retrieve all students enrolled in the Math course
SELECT S.Name AS StudentName, C.CourseName
FROM Students AS S
JOIN Enrollments AS E ON S.StudentID = E.StudentID
JOIN Courses AS C ON E.CourseID = C.CourseID
WHERE C.CourseName = 'Math'
ORDER BY S.Name;
```

