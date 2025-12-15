

# Student Course Management SQL Project

## 📌 Project Overview

This project demonstrates a **relational database design and SQL query practice** for a simple **Student Course Management System**. It covers database creation, table relationships, CRUD operations, joins, subqueries, aggregate functions, and advanced SQL features like window functions.

This project is suitable for:

* SQL beginners & data analyst learners
* Academic practice
* GitHub portfolio projects

---

## 🗄️ Database Details

**Database Name:** `Final`

```sql
CREATE DATABASE Final;
USE Final;
```

---

## 📋 Tables Structure

### 1️⃣ Students Table

Stores basic student information.

**Columns:**

* `StudentID` (Primary Key)
* `FirstName`
* `LastName`
* `Email`
* `BirthDate`
* `EnrollmentDate`

---

### 2️⃣ Courses Table

Stores course-related details.

**Columns:**

* `CourseID` (Primary Key)
* `CourseName`
* `DepartmentID` (Foreign Key)
* `Credits`

---

### 3️⃣ Departments Table

Stores department information.

**Columns:**

* `DepartmentID` (Primary Key)
* `DepartmentName`

---

### 4️⃣ emp Table (Enrollment Table)

Acts as a **junction table** between Students and Courses.

**Columns:**

* `EnrolmentID` (Primary Key)
* `StudentID` (Foreign Key)
* `CourseID` (Foreign Key)
* `EnrollmentDate`

---

## 🔗 Relationships

* One **Student** can enroll in multiple **Courses**
* One **Course** can have multiple **Students**
* Each **Course** belongs to one **Department**

---

## ✏️ CRUD Operations

### ✔️ Create

* Insert student, course, department, and enrollment records

### ✔️ Read

```sql
SELECT * FROM Students;
SELECT * FROM Courses;
SELECT * FROM Departments;
SELECT * FROM emp;
```

### ✔️ Update

```sql
UPDATE Students
SET Email = 'john.new@email.com'
WHERE StudentID = 1;
```

### ✔️ Delete

```sql
DELETE FROM emp
WHERE EnrolmentID = 2;
```

---

## 🔍 Queries Implemented

### 1️⃣ Students enrolled after 2022

```sql
SELECT * FROM Students
WHERE EnrollmentDate > '2022-01-01';
```

---

### 2️⃣ Courses offered by Mathematics Department

```sql
SELECT c.CourseID, c.CourseName
FROM Courses c
JOIN Departments d ON c.DepartmentID = d.DepartmentID
WHERE d.DepartmentName = 'Mathematics'
LIMIT 5;
```

---

### 3️⃣ Students count per course (HAVING clause)

```sql
SELECT c.CourseName, COUNT(e.StudentID) AS TotalStudents
FROM emp e
JOIN Courses c ON e.CourseID = c.CourseID
GROUP BY c.CourseName
HAVING COUNT(e.StudentID) > 0;
```

---

### 4️⃣ Students enrolled in **both** courses

```sql
HAVING COUNT(DISTINCT c.CourseName) = 2;
```

---

### 5️⃣ Students enrolled in **either** course

Uses `IN` with `DISTINCT`.

---

### 6️⃣ Average course credits

```sql
SELECT AVG(Credits) AS AverageCredits FROM Courses;
```

---

### 7️⃣ Count students per department

Uses `JOIN`, `GROUP BY`, and `COUNT(DISTINCT)`.

---

### 8️⃣ INNER JOIN Example

Retrieves students with their enrolled courses.

---

### 9️⃣ LEFT JOIN Example

Retrieves **all students**, even if not enrolled in any course.

---

### 🔟 Subquery Example

Students enrolled in courses with more than 10 students.

---

### 1️⃣1️⃣ Extract Year from Enrollment Date

```sql
SELECT YEAR(EnrollmentDate) AS EnrollmentYear FROM Students;
```

---

### 1️⃣2️⃣ Running Total (Window Function)

```sql
SUM(COUNT(StudentID)) OVER (ORDER BY CourseID)
```

---

### 1️⃣3️⃣ Senior vs Junior Classification

```sql
CASE
  WHEN EnrollmentDate <= CURDATE() - INTERVAL 4 YEAR THEN 'Senior'
  ELSE 'Junior'
END
```

---




## 👨‍💻 Author

Created for **SQL learning and data analysis practice**.

Happy Learning! 🎯
