<!-- Start ChatGPT-AI-prompt -->

## **SQL**

<div align="right"><b><a href="../../README.md">↥ Back to home</a></b></div>

### Q 1. What is SQL?

SQL (Structured Query Language) is the language used to communicate with relational databases. It allows you to create, read, update, and delete data (CRUD operations), as well as perform filtering, sorting, grouping, and joining data from multiple tables.

<div align="right"><b><a href="#ChatGPT-AI-prompt">↥ Back to top</a></b></div>

### Q 2. What is the difference between WHERE and HAVING?

WHERE filters individual records before grouping, while HAVING filters grouped results after aggregation.

| WHERE                          | HAVING                      |
| ------------------------------ | --------------------------- |
| Filters rows                   | Filters groups              |
| Before GROUP BY                | After GROUP BY              |
| Cannot use aggregate functions | Can use aggregate functions |

<div align="right"><b><a href="#ChatGPT-AI-prompt">↥ Back to top</a></b></div>

### Q 3. Difference between DELETE, TRUNCATE and DROP?

**DELETE** removes specific rows from a table using a condition. If no condition is given, it removes all rows. It is a row-level operation, and every deleted row is logged, so it is slower but safe. And it can rollback if it is inside a transaction and not committed.

```sql
DELETE FROM Employees
WHERE Department = 'IT';
```

**TRUNCATE** removes all rows from a table instantly without logging individual row deletions. It is faster than DELETE but does not support conditional deletion. Usually TRUNCATE be rolled back, but in some databases it can be rolled back if used inside a transaction.

```sql
TRUNCATE TABLE Employees;
```

**DROP** completely removes the table structure along with its data. Once dropped, the table no longer exists in the database. We can't recover a dropped table.

```sql
DROP TABLE Employees;
```

- DELETE → Removing selected pages from a notebook
- TRUNCATE → Erasing all pages but keeping the notebook
- DROP → Throwing away the entire notebook

| Feature           | DELETE    | TRUNCATE                | DROP                  |
| ----------------- | --------- | ----------------------- | --------------------- |
| Level             | Row level | Table level (data only) | Database object level |
| WHERE support     | Yes       | No                      | No                    |
| Rollback          | Possible  | Limited/depends         | Not possible          |
| Speed             | Slow      | Fast                    | Fastest               |
| Resets identity   | No        | Yes                     | N/A                   |
| Structure removed | No        | No                      | Yes                   |

<div align="right"><b><a href="#ChatGPT-AI-prompt">↥ Back to top</a></b></div>

### Q 4. What is Constraints?

Constraints are rules applied to database columns to ensure data integrity and validity.
Primary Key uniquely identifies records, while Foreign Key maintains relationships between tables.
Other constraints like NOT NULL, UNIQUE, and CHECK enforce additional data rules.

1. **NOT NULL:** Prevents a column from having NULL (empty) values. It ensures that every record must have a valid value for that field.

2. **UNIQUE:** Ensures that all values in a column are different. No duplicate values are allowed in that column.

3. **PRIMARY KEY:** A constraint that uniquely identifies each record in a table. It is a combination of NOT NULL and UNIQUE, and only one primary key is allowed per table.

4. **FOREIGN KEY:** Establishes a relationship between two tables by referencing the primary key of another table. It ensures referential integrity.

5. **CHECK:** Ensures that all values in a column satisfy a specific condition or rule defined by the user.

6. **DEFAULT:** Provides a default value for a column when no value is specified during insertion.

<div align="right"><b><a href="#ChatGPT-AI-prompt">↥ Back to top</a></b></div>

### Q 5. Normalization?

Normalization is the process of organizing data into multiple related tables to reduce data duplication and improve data consistency.

`1NF` ensures each column contains a single value, `2NF` removes duplicate data by separating entities into related tables, and `3NF` removes transitive dependencies where a non-key column depends on another non-key column. Together, they reduce redundancy and improve data consistency.

<div align="right"><b><a href="#nodejs">↥ Back to top</a></b></div>

### Q 6. What is Denormalization?

Denormalization is the process of intentionally duplicating data to improve read performance. It reduces joins and speeds up queries at the cost of increased storage and maintenance complexity. It is commonly used in reporting systems, data warehouses, and NoSQL databases like MongoDB.

> Normalization = Remove duplicate data.\
> Denormalization = Add some duplicate data for faster queries

<div align="right"><b><a href="#nodejs">↥ Back to top</a></b></div>

### Q 7. What is GROUP BY and SORT BY?

`GROUP BY` is used to combine rows that have the same values in one or more columns and then apply aggregate functions like COUNT, SUM, AVG, etc.

```sql
SELECT Department, COUNT(*) AS TotalEmployees
FROM Employees
GROUP BY Department;
```

`ORDER BY` is used to sort the result set in ascending or descending order based on one or more columns.

```sql
SELECT Name, Salary
FROM Employees
ORDER BY Salary DESC;
```

<div align="right"><b><a href="#ChatGPT-AI-prompt">↥ Back to top</a></b></div>

### Q 8. What are Aggregate Functions?

Aggregate functions are SQL functions that perform a calculation on multiple rows and return a single result.

**Common Aggregate Functions**

1. **COUNT():** Counts the number of rows. `SELECT COUNT(*) FROM Employees;`. Returns total number of employees.

2. **SUM():** Calculates total sum of a numeric column. `SELECT SUM(Salary) FROM Employees;`. Returns total salary paid.

3. **AVG():** Calculates average value. `SELECT AVG(Salary) FROM Employees;`. Returns average salary.

4. **MIN():** Finds the smallest value. `SELECT MIN(Salary) FROM Employees;`. Returns lowest salary.

5. **MAX():** Finds the largest value. `SELECT MAX(Salary) FROM Employees;`. Returns highest salary.

<div align="right"><b><a href="#ChatGPT-AI-prompt">↥ Back to top</a></b></div>

### Q 9. What Index?

An Index is a data structure that improves query performance by allowing faster data retrieval. It reduces the need for full table scans and speeds up WHERE, JOIN, and ORDER BY operations. While indexes improve reads, they add overhead to INSERT, UPDATE, and DELETE operations.

- Advantages
  - Faster SELECT queries
  - Faster JOIN operations
  - Faster sorting (ORDER BY)
  - Faster filtering (WHERE)
- Disadvantages
  - Consumes additional storage
  - Slows INSERT, UPDATE, DELETE because indexes must also be updated

**Types of Indexes**

1. **Clustered Index:** A Clustered Index determines the physical order of data in a table. Since data can only be physically arranged one way, a table can have only one Clustered Index.

   ```sql
   CREATE CLUSTERED INDEX idx_empid
   ON Employees(EmployeeId);

   <!-- Use Case: Range searches: -->

   SELECT *
   FROM Employees
   WHERE EmployeeId BETWEEN 1000 AND 2000;
   ```

2. **Non-Clustered Index:** A Non-Clustered Index is a separate structure that stores indexed values and pointers to the actual rows. A table can have multiple Non-Clustered Indexes.

   ```sql
   CREATE INDEX idx_email
   ON Employees(Email);
   ```

   - Use Case: Searching by Email, Username, Phone Number, etc.

3. **Composite (Multi-Column) Index:** An index created on multiple columns.

   ```sql
   CREATE INDEX idx_dept_salary
   ON Employees(Department, Salary);

   <!-- Best For -->
   SELECT *
   FROM Employees
   WHERE Department='IT'
   AND Salary > 50000;
   ```

4. **Unique Index:** Ensures that duplicate values cannot exist in the indexed column.

   ```sql
   CREATE UNIQUE INDEX idx_email
   ON Employees(Email);
   ```

   - Use Case: Email, Username, PAN Number, Passport Number

<div align="right"><b><a href="#ChatGPT-AI-prompt">↥ Back to top</a></b></div>

### Q 10. What is a View?

A View is a virtual table created from the result of a SQL query.

Unlike a real table, a view does not usually store data itself. Instead, it stores the SQL query, and whenever you query the view, the database executes that query and returns the result.

**Why Use Views?**

1. **Security:** Hide sensitive columns. Instead of exposing: EmployeeId, Name, Salary, BankAccount. Create a view exposing only: EmployeeId, Name, Department.

2. **Simplify Complex Queries:** Instead of writing a long JOIN every time: Create a view once and reuse it.

   ```sql
   SELECT ...
   FROM Orders o
   JOIN Customers c ...
   JOIN Products p ...
   ```

<div align="right"><b><a href="#ChatGPT-AI-prompt">↥ Back to top</a></b></div>

### Q 11. What is a Trigger?

A Trigger is a database object that automatically executes when an INSERT, UPDATE, or DELETE event occurs. It is commonly used for auditing, validation, history tracking, and enforcing business rules. Since triggers run automatically, excessive use can affect performance and maintainability.

```sql
-- Suppose whenever a new employee is added, you want to record it in an audit table.

CREATE TRIGGER trg_AfterInsertEmployee
AFTER INSERT
ON Employees
FOR EACH ROW
INSERT INTO AuditLog(Message)
VALUES ('New Employee Added');

-- Now whenever a record is inserted into Employees:

INSERT INTO Employees(Name)
VALUES ('John');

-- The trigger runs automatically and inserts a record into AuditLog.
```

**Common Types of Triggers**

1. **BEFORE Trigger:** Executes before the actual operation. Use Case: Validate data before inserting.

2. **AFTER Trigger:** Executes after the operation completes successfully. Use Case: Audit logging, notifications, history tracking.

3. **INSTEAD OF Trigger:** Executes instead of the actual operation. Use Case: Custom business logic on views.

<div align="right"><b><a href="#ChatGPT-AI-prompt">↥ Back to top</a></b></div>

### Q 12. What is a Stored Procedure?

A Stored Procedure is a precompiled collection of SQL statements stored in the database. It improves reusability, security, and performance by centralizing business logic. Procedures can accept parameters and execute complex database operations.

```sql
CREATE PROCEDURE GetEmployees
AS
BEGIN
    SELECT *
    FROM Employees;
END;

-- Execute Procedure
EXEC GetEmployees;
```

<div align="right"><b><a href="#ChatGPT-AI-prompt">↥ Back to top</a></b></div>

### Q 13. Difference between Stored Procedure vs Functions?

Functions are primarily used for calculations and returning values, while Stored Procedures are used for performing database operations such as inserts, updates, deletes, and transactions. Functions can be called inside a SELECT statement, but Stored Procedures cannot.

<div align="right"><b><a href="#ChatGPT-AI-prompt">↥ Back to top</a></b></div>

### Q 14. SQL JOINs (INNER JOIN vs LEFT JOIN vs RIGHT JOIN vs FULL JOIN).?

Joins are used to combine data from multiple tables based on a related column.

```js
// Example Tables
// Users
id | name
-----------
1  | John
2  | Mike
3  | David
// Orders
id | user_id | product
----------------------
1  | 1       | Laptop
2  | 1       | Mouse
3  | 2       | Mobile
```

1. **INNER JOIN:** Returns only matching records from both tables. Use it When you only want records that exist in both tables.

   ```js
   SELECT u.name, o.product
   FROM users u
   INNER JOIN orders o
   ON u.id = o.user_id;

   // Result
   John   Laptop
   John   Mouse
   Mike   Mobile
   ```

2. **LEFT JOIN:** Returns all rows from the left table and matching rows from the right table.

   ```js
   // Query
   SELECT u.name, o.product
   FROM users u
   LEFT JOIN orders o
   ON u.id = o.user_id;

   // Result
   John   Laptop
   John   Mouse
   Mike   Mobile
   David  NULL
   ```

3. **RIGHT JOIN:** Returns all rows from the right table and matching rows from the left table.

   ```js
   // Query
   SELECT u.name, o.product
   FROM users u
   RIGHT JOIN orders o
   ON u.id = o.user_id;

   // Result

   John   Laptop
   John   Mouse
   Mike   Mobile
   ```

4. **FULL JOIN:** All rows from Left Table + All rows from Right Table. Whether matching or not.

   ```js
   // Query
   SELECT u.name, o.product
   FROM users u
   FULL JOIN orders o
   ON u.id = o.user_id;

   // Result
   John   Laptop
   John   Mouse
   Mike   Mobile
   David  NULL
   NULL   Tablet
   ```

<div align="right"><b><a href="#nodejs">↥ Back to top</a></b></div>

### Q 15. Database Transactions?

A Transaction is a group of database operations that are executed as a single unit of work.

Either: `All operations succeed` or `All operations fail (Rollback)`.

```js
// Bank Transfer: Suppose: John Account = ₹1000 and Mike Account = ₹500. John transfers: ₹200 → Mike

Steps:

1. Deduct ₹200 from John
2. Add ₹200 to Mike

// If step 1 succeeds and step 2 fails: John = ₹800 and Mike = ₹500. Money is lost ❌

// Using a transaction:

BEGIN;

UPDATE accounts
SET balance = balance - 200
WHERE id = 1;

UPDATE accounts
SET balance = balance + 200
WHERE id = 2;

COMMIT;

// If any step fails:

ROLLBACK;

// Database returns to the original state.
```

<div align="right"><b><a href="#nodejs">↥ Back to top</a></b></div>

### Q 16. ACID Properties?

ACID properties are implemented by the database engine, not manually by developers. In applications, we use transactions with BEGIN, COMMIT, and ROLLBACK to ensure Atomicity, while the database handles Consistency, Isolation, and Durability internally through constraints, isolation levels, and transaction logs.

- **A - Atomicity** Either everything happens or nothing happens.
- **C - Consistency** Data must always remain valid before and after a transaction.
- **I - Isolation** Multiple transactions should not interfere with each other. Example: Two users update the same account simultaneously. Database ensures transactions are handled safely.
- **D - Durability** Once committed, data is permanently stored even if the database crashes.

<div align="right"><b><a href="#nodejs">↥ Back to top</a></b></div>

### Q 17. Optimistic Locking vs Pessimistic Locking?

Both are techniques used to handle concurrent updates to the same data.

**Optimistic Locking:** Assumes conflicts are rare. Instead of locking the row, it checks whether someone else modified the data before saving. Usually implemented using a: version column or timestamp column. Used in E-commerce and Low chance of conflicts.

**Pessimistic Locking:** Assumes conflicts are likely. Locks the row immediately so nobody else can modify it. Used in Banking and Payment Systems.

| Feature           | Optimistic   | Pessimistic         |
| ----------------- | ------------ | ------------------- |
| Locks Data?       | No           | Yes                 |
| Performance       | Faster       | Slower              |
| Concurrency       | High         | Lower               |
| Conflict Handling | Detect Later | Prevent Immediately |
| Best For          | Web Apps     | Banking/Payments    |

<div align="right"><b><a href="#nodejs">↥ Back to top</a></b></div>

### Q 18. Database Scaling?

I usually start database scaling with query optimization, indexing, and connection pooling. If traffic continues to grow, I introduce Redis caching and read replicas to reduce database load. For very large systems, I consider sharding and horizontal database scaling.

1. **Connection Pooling:** Maintains a pool of reusable database connections instead of creating a new connection for every request. This reduces connection overhead and improves database performance.

2. **Redis Caching;** Stores frequently accessed data in memory so requests can be served faster without hitting the database. This reduces database load and improves response times.

3. **Read Replicas:** Creates one or more copies of the primary database to handle read queries. This helps distribute read traffic and reduces load on the primary database to INSERT, UPDATE, DELETE.

4. **Database Indexing:** Creates a data structure that allows the database to find records quickly without scanning the entire table. It improves read performance but can slow down writes.

5. **Query Optimization:** Improves SQL queries by reducing unnecessary scans, joins, and computations. Often the cheapest and most effective way to improve database performance.

6. **Sharding:** Splits data across multiple database servers based on a sharding key (e.g., User ID). Used when a single database can no longer handle the volume of data or traffic.

7. **Partitioning:** Divides a large table into smaller logical partitions within the same database. This improves query performance and makes large datasets easier to manage.

8. **Materialized Views:** Stores precomputed query results so expensive aggregations don't need to run repeatedly. Useful for reporting and analytics workloads.

9. **Denormalization:** Stores duplicate data to reduce joins and improve read performance. Common in high-read applications where performance is more important than storage efficiency.

10. **Archiving:** Moves old or rarely accessed data to separate storage or tables. This keeps active tables smaller and improves query performance.

> I use Partitioning when a table becomes very large but still fits within a single database server. I use Sharding when a single database server can no longer handle the storage, traffic, or resource requirements. Partitioning improves query performance, while Sharding improves overall scalability.

<div align="right"><b><a href="#nodejs">↥ Back to top</a></b></div>

<!-- ### Q 1. What?

<div align="right"><b><a href="#ChatGPT-AI-prompt">↥ Back to top</a></b></div> -->

##

## **MongoDB**

### Q 1. What is MongoDB?

MongoDB is a NoSQL document database. It stores data as BSON (Binary JSON) documents instead of rows and columns. MongoDB stores related data together in a single document. It is designed for flexibility, scalability, and high performance.

<div align="right"><b><a href="#ChatGPT-AI-prompt">↥ Back to top</a></b></div>

### Q 2. What is a Collection?

A Collection is a group of MongoDB documents. It is similar to a SQL table. Documents inside can have different structures.

<div align="right"><b><a href="#ChatGPT-AI-prompt">↥ Back to top</a></b></div>

### Q 3. What is a Document?

A document is a JSON-like data structure. It stores related data together. It is equivalent to a row in SQL.

<div align="right"><b><a href="#ChatGPT-AI-prompt">↥ Back to top</a></b></div>

### Q 4. What is BSON?

BSON stands for Binary JSON and is MongoDB's internal storage format. It extends JSON by supporting additional data types such as ObjectId, Date, and Decimal128. BSON is optimized for efficient storage, indexing, and fast document retrieval.

<div align="right"><b><a href="#ChatGPT-AI-prompt">↥ Back to top</a></b></div>

### Q 5. What is ObjectId and how is it generated in MongoDB?

ObjectId is MongoDB's default unique identifier used for the \_id field of a document. When you insert a document without specifying an \_id, MongoDB automatically generates an ObjectId.

```json
{
  "_id": ObjectId("507f1f77bcf86cd799439011"),
  "name": "John"
}
```

<div align="right"><b><a href="#ChatGPT-AI-prompt">↥ Back to top</a></b></div>

### Q 6. What is Embedding vs Referencing in MongoDB?

**Embedding** stores related data within a single document. It reduces lookups and improves read performance. Best for one-to-one and one-to-few relationships.

**Referencing** stores relationships using IDs. Similar to Foreign Keys in SQL. Best for large or frequently changing relationships.

| Embedding    | Referencing      |
| ------------ | ---------------- |
| Faster reads | Less duplication |
| One query    | Multiple queries |
| More storage | Less storage     |

<div align="right"><b><a href="#ChatGPT-AI-prompt">↥ Back to top</a></b></div>

### Q 7. What is Aggregation Pipeline?

Aggregation Pipeline is MongoDB's framework for data processing and analytics. It processes documents through stages such as `$match`, `$grou`p, `$sort`, `$project`, and `$lookup`. It is similar to SQL operations like `WHERE`, `GROUP BY`, `ORDER BY`, and `JOIN`.

| SQL      | MongoDB  |
| -------- | -------- |
| WHERE    | $match   |
| GROUP BY | $group   |
| ORDER BY | $sort    |
| SELECT   | $project |
| JOIN     | $lookup  |

```ts
db.orders.aggregate([
  // 1. Filter Orders
  {
    $match: {
      status: "Completed",
    },
  },

  // 2. Join Customer Data
  {
    $lookup: {
      from: "customers",
      localField: "customerId",
      foreignField: "_id",
      as: "customer",
    },
  },

  // 3. Select Required Fields
  {
    $project: {
      department: 1,
      amount: 1,
      customerName: {
        $arrayElemAt: ["$customer.name", 0],
      },
    },
  },

  // 4. Group Data
  {
    $group: {
      _id: "$department",
      totalRevenue: {
        $sum: "$amount",
      },
      totalOrders: {
        $sum: 1,
      },
    },
  },

  // 5. Sort Results
  {
    $sort: {
      totalRevenue: -1,
    },
  },
]);
```

<div align="right"><b><a href="#ChatGPT-AI-prompt">↥ Back to top</a></b></div>

### Q 8. Why MongoDB over PostgreSQL/MySQL?

MongoDB is preferred when we need flexible schemas, rapid development, and horizontal scalability. PostgreSQL/MySQL are preferred when we need strong relational modeling, complex joins, and highly structured transactional data.

<div align="right"><b><a href="#ChatGPT-AI-prompt">↥ Back to top</a></b></div>

### Q 9. How do you optimize slow MongoDB queries?

In production, my first step is to analyze the query using explain("executionStats") to identify collection scans. I then verify index usage, review compound index design, optimize aggregation stages by pushing $match early, reduce unnecessary fields with projections, and revisit schema design if excessive $lookup operations are involved.

<div align="right"><b><a href="#ChatGPT-AI-prompt">↥ Back to top</a></b></div>

<!-- ### Q 10. What is Sharding in MongoDB?

<div align="right"><b><a href="#ChatGPT-AI-prompt">↥ Back to top</a></b></div> -->

<!-- ### Q 1.

<div align="right"><b><a href="#ChatGPT-AI-prompt">↥ Back to top</a></b></div> -->

##
