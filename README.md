# SQL Guide

github repository: https://github.com/isaac-evs/SQL_Guide

This guide provides a comprehensive overview of SQL operators, commands, and concepts with examples.

## Basic Operators and Clauses

### WHERE
**Description**: Filters records based on specified conditions.
```sql
SELECT * FROM employees WHERE salary > 50000;
```

### JOIN
**Description**: Combines rows from two or more tables based on a related column.
```sql
SELECT orders.order_id, customers.name
FROM orders
JOIN customers ON orders.customer_id = customers.id;
```

### GROUP BY
**Description**: Groups rows that have the same values into summary rows.
```sql
SELECT department, COUNT(*) as employee_count
FROM employees
GROUP BY department;
```

### ORDER BY
**Description**: Sorts the result set in ascending or descending order.
```sql
SELECT name, age FROM users ORDER BY age DESC;
```

### INSERT INTO
**Description**: Adds new records into a table.
```sql
INSERT INTO employees (name, salary, department)
VALUES ('John Doe', 60000, 'IT');
```

### UPDATE
**Description**: Modifies existing records in a table.
```sql
UPDATE employees
SET salary = 65000
WHERE name = 'John Doe';
```

### DELETE
**Description**: Removes records from a table.
```sql
DELETE FROM employees WHERE department = 'IT';
```

## Table Operations

### CREATE TABLE
**Description**: Creates a new table in the database.
```sql
CREATE TABLE employees (
    id INT PRIMARY KEY,
    name VARCHAR(100),
    salary DECIMAL(10,2)
);
```

### ALTER TABLE
**Description**: Modifies an existing table structure.
```sql
ALTER TABLE employees
ADD COLUMN email VARCHAR(100);
```

### DROP TABLE
**Description**: Removes a table from the database.
```sql
DROP TABLE employees;
```

## Views and Indexes

### VIEW
**Description**: Creates a virtual table based on a SELECT statement.
```sql
CREATE VIEW high_salary_employees AS
SELECT * FROM employees WHERE salary > 70000;
```

### INDEX
**Description**: Creates an index for faster data retrieval.
```sql
CREATE INDEX idx_employee_name
ON employees(name);
```

## Set Operations

### UNION
**Description**: Combines result sets of multiple SELECT statements and removes duplicates.
```sql
SELECT city FROM customers
UNION
SELECT city FROM suppliers;
```

## Advanced Queries

### SUBQUERY
**Description**: A query nested inside another query.
```sql
SELECT name FROM employees
WHERE salary > (SELECT AVG(salary) FROM employees);
```

### HAVING
**Description**: Filters group results based on aggregate functions.
```sql
SELECT department, AVG(salary)
FROM employees
GROUP BY department
HAVING AVG(salary) > 60000;
```

### DISTINCT
**Description**: Returns only unique values in the result set.
```sql
SELECT DISTINCT department FROM employees;
```

## Pagination

### LIMIT
**Description**: Specifies the maximum number of records to return.
```sql
SELECT * FROM employees LIMIT 10;
```

### OFFSET
**Description**: Skips a specified number of records.
```sql
SELECT * FROM employees LIMIT 10 OFFSET 20;
```

## Pattern Matching and Comparisons

### LIKE
**Description**: Searches for a specified pattern in a column.
```sql
SELECT * FROM employees WHERE name LIKE 'J%';
```

### IN
**Description**: Specifies multiple possible values for a column.
```sql
SELECT * FROM employees WHERE department IN ('IT', 'HR', 'Sales');
```

### BETWEEN
**Description**: Selects values within a given range.
```sql
SELECT * FROM employees WHERE salary BETWEEN 50000 AND 70000;
```

## NULL Operations

### NULL
**Description**: Represents a missing or unknown value.
```sql
SELECT * FROM employees WHERE manager_id IS NULL;
```

## Aliases and Transformations

### AS
**Description**: Creates an alias for a column or table.
```sql
SELECT name AS employee_name FROM employees;
```

### CASE
**Description**: Creates different outputs based on conditions.
```sql
SELECT name,
    CASE
        WHEN salary > 70000 THEN 'High'
        WHEN salary > 50000 THEN 'Medium'
        ELSE 'Low'
    END AS salary_category
FROM employees;
```

### CAST
**Description**: Converts a value from one data type to another.
```sql
SELECT CAST(price AS INTEGER) FROM products;
```

### COALESCE
**Description**: Returns the first non-null value in a list.
```sql
SELECT COALESCE(phone, email, 'No Contact') FROM employees;
```

## Existence Tests

### EXISTS
**Description**: Tests for the existence of records in a subquery.
```sql
SELECT * FROM departments
WHERE EXISTS (
    SELECT 1 FROM employees
    WHERE employees.dept_id = departments.id
);
```

## Join Types

### INNER JOIN
**Description**: Returns only the matching rows between tables.
```sql
SELECT * FROM orders
INNER JOIN customers ON orders.customer_id = customers.id;
```

### LEFT JOIN
**Description**: Returns all records from the left table and matching records from the right table.
```sql
SELECT * FROM employees
LEFT JOIN departments ON employees.dept_id = departments.id;
```

### RIGHT JOIN
**Description**: Returns all records from the right table and matching records from the left table.
```sql
SELECT * FROM employees
RIGHT JOIN departments ON employees.dept_id = departments.id;
```

### FULL OUTER JOIN
**Description**: Returns all records when there's a match in either left or right table.
```sql
SELECT * FROM employees
FULL OUTER JOIN departments ON employees.dept_id = departments.id;
```

### CROSS JOIN
**Description**: Returns the Cartesian product of both tables.
```sql
SELECT * FROM sizes CROSS JOIN colors;
```

### SELF JOIN
**Description**: Joins a table with itself.
```sql
SELECT e1.name as employee, e2.name as manager
FROM employees e1
LEFT JOIN employees e2 ON e1.manager_id = e2.id;
```

## Constraints

### PRIMARY KEY
**Description**: Uniquely identifies each record in a table.
```sql
CREATE TABLE users (
    id INT PRIMARY KEY,
    username VARCHAR(50)
);
```

### FOREIGN KEY
**Description**: Creates a link between tables based on a column.
```sql
CREATE TABLE orders (
    id INT PRIMARY KEY,
    user_id INT,
    FOREIGN KEY (user_id) REFERENCES users(id)
);
```

### UNIQUE
**Description**: Ensures all values in a column are different.
```sql
CREATE TABLE users (
    email VARCHAR(100) UNIQUE,
    username VARCHAR(50)
);
```

### CHECK
**Description**: Ensures all values in a column satisfy certain conditions.
```sql
CREATE TABLE employees (
    salary DECIMAL CHECK (salary > 0)
);
```

### DEFAULT
**Description**: Sets a default value for a column.
```sql
CREATE TABLE posts (
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

## Data Management

### TRUNCATE
**Description**: Quickly removes all records from a table.
```sql
TRUNCATE TABLE log_entries;
```

## Transaction Control

### TRANSACTION
**Description**: Groups a set of database operations into a single unit.
```sql
BEGIN TRANSACTION;
    UPDATE accounts SET balance = balance - 100 WHERE id = 1;
    UPDATE accounts SET balance = balance + 100 WHERE id = 2;
COMMIT;
```

### COMMIT
**Description**: Saves all transactions to the database.
```sql
COMMIT;
```

### ROLLBACK
**Description**: Reverts all transactions since the last commit.
```sql
ROLLBACK;
```

## Security

### GRANT
**Description**: Gives specific privileges to users.
```sql
GRANT SELECT, INSERT ON employees TO user_role;
```

### REVOKE
**Description**: Removes specific privileges from users.
```sql
REVOKE INSERT ON employees FROM user_role;
```

## Performance and Analysis

### EXPLAIN
**Description**: Shows the execution plan of a query.
```sql
EXPLAIN SELECT * FROM employees WHERE salary > 50000;
```

## Auto-Incrementing

### AUTO_INCREMENT
**Description**: Automatically generates unique values for a column.
```sql
CREATE TABLE users (
    id INT AUTO_INCREMENT PRIMARY KEY,
    username VARCHAR(50)
);
```

### SERIAL
**Description**: PostgreSQL's version of AUTO_INCREMENT.
```sql
CREATE TABLE users (
    id SERIAL PRIMARY KEY,
    username VARCHAR(50)
);
```

## Advanced Table Operations

### TEMPORARY TABLE
**Description**: Creates a table that exists only for the current session.
```sql
CREATE TEMPORARY TABLE temp_results AS
SELECT * FROM large_table WHERE status = 'pending';
```

### COMMON TABLE EXPRESSION (CTE)
**Description**: Creates a named temporary result set.
```sql
WITH high_salary_emp AS (
    SELECT * FROM employees WHERE salary > 70000
)
SELECT department, COUNT(*) FROM high_salary_emp GROUP BY department;
```

### WINDOW FUNCTIONS
**Description**: Performs calculations across a set of rows.
```sql
SELECT name, salary,
    RANK() OVER (ORDER BY salary DESC) as salary_rank
FROM employees;
```

## Data Transformation

### PIVOT
**Description**: Converts rows into columns.
```sql
SELECT *
FROM (
    SELECT department, quarter, sales
    FROM sales_data
) AS source
PIVOT (
    SUM(sales)
    FOR quarter IN (Q1, Q2, Q3, Q4)
) AS pivot_table;
```

### MERGE
**Description**: Performs INSERT, UPDATE, or DELETE operations based on conditions.
```sql
MERGE INTO target_table t
USING source_table s
ON (t.id = s.id)
WHEN MATCHED THEN UPDATE SET t.value = s.value
WHEN NOT MATCHED THEN INSERT (id, value) VALUES (s.id, s.value);
```

## JSON Operations

### JSON Functions
**Description**: Manipulates JSON data in the database.
```sql
SELECT JSON_EXTRACT(data, '$.name') as name
FROM users_json;
```

## Database Procedures

### Stored Procedures
**Description**: Saved SQL code that can be reused.
```sql
CREATE PROCEDURE get_employee_count()
BEGIN
    SELECT COUNT(*) FROM employees;
END;
```

### Triggers
**Description**: SQL code that automatically executes in response to certain events.
```sql
CREATE TRIGGER update_timestamp
BEFORE UPDATE ON employees
FOR EACH ROW
SET NEW.updated_at = CURRENT_TIMESTAMP;
```

### Functions
**Description**: Returns a single value based on input parameters.
```sql
CREATE FUNCTION calculate_bonus(salary DECIMAL)
RETURNS DECIMAL
BEGIN
    RETURN salary * 0.1;
END;
```

## Database Design Concepts

### Normalization
**Description**: Process of organizing tables to reduce data redundancy.
- First Normal Form (1NF): Eliminate repeating groups
- Second Normal Form (2NF): Remove partial dependencies
- Third Normal Form (3NF): Remove transitive dependencies

### Denormalization
**Description**: Process of combining tables to improve query performance at the expense of data redundancy.

### ACID Properties
**Description**: Properties ensuring reliable database transactions:
- Atomicity: Transactions are all or nothing
- Consistency: Database remains in a valid state
- Isolation: Transactions don't interfere with each other
- Durability: Completed transactions are permanent

### Indexing Strategies
**Description**: Methods to optimize database performance:
- B-tree indexes
- Hash indexes
- Bitmap indexes
- Covering indexes

### Query Optimization
**Description**: Techniques to improve query performance:
- Index usage
- Join optimization
- Subquery optimization
- Query plan analysis

### Data Types
**Description**: Common SQL data types:
- Numeric: INT, DECIMAL, FLOAT
- String: VARCHAR, CHAR, TEXT
- Date/Time: DATE, TIMESTAMP
- Boolean: BOOLEAN
- Binary: BLOB, BINARY

### Constraints
**Description**: Rules enforced on data columns:
- NOT NULL
- UNIQUE
- PRIMARY KEY
- FOREIGN KEY
- CHECK
- DEFAULT

### Schema
**Description**: Logical container for database objects:
- Tables
- Views
- Procedures
- Functions
- Triggers

### Database Transactions
**Description**: Logical unit of work containing one or more SQL statements:
- BEGIN TRANSACTION
- COMMIT
- ROLLBACK
- SAVEPOINT

## Relational Algebra

Relational algebra is a fundamental set of operations used in relational databases. These operations form the theoretical foundation of SQL queries.

### Selection (σ)
**Description**: Filters tuples (rows) based on a condition.
**Notation**: σ<condition>(R)
**SQL Equivalent**:
```sql
-- Relational Algebra: σsalary>50000(employees)
SELECT * FROM employees WHERE salary > 50000;
```

### Projection (π)
**Description**: Selects specific attributes (columns) from a relation.
**Notation**: π<attributes>(R)
**SQL Equivalent**:
```sql
-- Relational Algebra: πname,salary(employees)
SELECT name, salary FROM employees;
```

### Union (∪)
**Description**: Combines two relations and removes duplicates.
**Notation**: R ∪ S
**SQL Equivalent**:
```sql
-- Relational Algebra: πcity(customers) ∪ πcity(suppliers)
SELECT city FROM customers
UNION
SELECT city FROM suppliers;
```

### Set Difference (-)
**Description**: Returns tuples in first relation but not in second.
**Notation**: R - S
**SQL Equivalent**:
```sql
-- Relational Algebra: πcity(customers) - πcity(suppliers)
SELECT city FROM customers
EXCEPT
SELECT city FROM suppliers;
```

### Cartesian Product (×)
**Description**: Combines every tuple from first relation with every tuple from second.
**Notation**: R × S
**SQL Equivalent**:
```sql
-- Relational Algebra: employees × departments
SELECT * FROM employees
CROSS JOIN departments;
```

### Natural Join (⋈)
**Description**: Joins relations based on common attributes.
**Notation**: R ⋈ S
**SQL Equivalent**:
```sql
-- Relational Algebra: employees ⋈ departments
SELECT * FROM employees
NATURAL JOIN departments;
```

### Theta Join (⋈θ)
**Description**: Joins relations based on a specific condition.
**Notation**: R ⋈θ S
**SQL Equivalent**:
```sql
-- Relational Algebra: employees ⋈(employees.dept_id = departments.id) departments
SELECT * FROM employees
JOIN departments ON employees.dept_id = departments.id;
```

### Division (÷)
**Description**: Returns elements from first relation that match all elements in second relation.
**Notation**: R ÷ S
**SQL Equivalent**:
```sql
-- Relational Algebra: suppliers ÷ products
-- Find suppliers who supply all products
SELECT s.supplier_id
FROM suppliers s
WHERE NOT EXISTS (
    SELECT p.product_id
    FROM products p
    WHERE NOT EXISTS (
        SELECT 1
        FROM supplies sup
        WHERE sup.supplier_id = s.supplier_id
        AND sup.product_id = p.product_id
    )
);
```

### Rename (ρ)
**Description**: Renames attributes or relations.
**Notation**: ρnew_name(R) or ρnew_name(attribute_list)(R)
**SQL Equivalent**:
```sql
-- Relational Algebra: ρmanager(employees)
SELECT e1.name as employee, e2.name as manager
FROM employees e1
JOIN employees e2 ON e1.manager_id = e2.id;
```

### Intersection (∩)
**Description**: Returns tuples that appear in both relations.
**Notation**: R ∩ S
**SQL Equivalent**:
```sql
-- Relational Algebra: πcity(customers) ∩ πcity(suppliers)
SELECT city FROM customers
INTERSECT
SELECT city FROM suppliers;
```

### Aggregation (γ)
**Description**: Groups and applies aggregate functions.
**Notation**: γcolumn_list,aggregate_function(R)
**SQL Equivalent**:
```sql
-- Relational Algebra: γdepartment,COUNT(*)(employees)
SELECT department, COUNT(*)
FROM employees
GROUP BY department;
```

### Extended Operators

#### Outer Join (⟕, ⟖, ⟗)
**Description**: Includes unmatched tuples with null values.
- Left Outer Join (⟕)
- Right Outer Join (⟖)
- Full Outer Join (⟗)
**SQL Equivalent**:
```sql
-- Relational Algebra: employees ⟕ departments
SELECT * FROM employees
LEFT OUTER JOIN departments ON employees.dept_id = departments.id;
```

#### Semi Join (⋉, ⋊)
**Description**: Joins relations but only keeps attributes from one relation.
**Notation**: R ⋉ S or R ⋊ S
**SQL Equivalent**:
```sql
-- Relational Algebra: employees ⋉ departments
SELECT DISTINCT employees.*
FROM employees
JOIN departments ON employees.dept_id = departments.id;
```

### Important Properties

1. **Closure Property**: Result of any relational operation is also a relation
2. **Commutative Property**:
   - R ∪ S = S ∪ R
   - R ∩ S = S ∩ R
   - R ⋈ S = S ⋈ R
3. **Associative Property**:
   - (R ∪ S) ∪ T = R ∪ (S ∪ T)
   - (R ∩ S) ∩ T = R ∩ (S ∩ T)
   - (R ⋈ S) ⋈ T = R ⋈ (S ⋈ T)
4. **Distributive Property**:
   - σc(R ∪ S) = σc(R) ∪ σc(S)
   - πa(R ∪ S) = πa(R) ∪ πa(S)
