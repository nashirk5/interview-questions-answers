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

### Q 1. Difference between DELETE, TRUNCATE and DROP?

<div align="right"><b><a href="#ChatGPT-AI-prompt">↥ Back to top</a></b></div>

### Q 59. SQL JOINs (INNER JOIN vs LEFT JOIN vs RIGHT JOIN vs FULL JOIN).?

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

### Q 54. Database Transactions?

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

### Q 55. ACID Properties?

ACID properties are implemented by the database engine, not manually by developers. In applications, we use transactions with BEGIN, COMMIT, and ROLLBACK to ensure Atomicity, while the database handles Consistency, Isolation, and Durability internally through constraints, isolation levels, and transaction logs.

- **A - Atomicity** Either everything happens or nothing happens.
- **C - Consistency** Data must always remain valid before and after a transaction.
- **I - Isolation** Multiple transactions should not interfere with each other. Example: Two users update the same account simultaneously. Database ensures transactions are handled safely.
- **D - Durability** Once committed, data is permanently stored even if the database crashes.

<div align="right"><b><a href="#nodejs">↥ Back to top</a></b></div>

### Q 57. Normalization?

Normalization is the process of organizing data into multiple related tables to reduce data duplication and improve data consistency.

`1NF` ensures each column contains a single value, `2NF` removes duplicate data by separating entities into related tables, and `3NF` removes transitive dependencies where a non-key column depends on another non-key column. Together, they reduce redundancy and improve data consistency.

<div align="right"><b><a href="#nodejs">↥ Back to top</a></b></div>

### Q 58. Optimistic Locking vs Pessimistic Locking?

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

### Q 51. Database Scaling?

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
