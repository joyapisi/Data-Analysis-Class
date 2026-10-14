# READ OPERATION IN CRUD
## SQL SELECT Statement Examples

This repository contains practical examples of the SQL `SELECT` statement and its primary clauses. All queries are designed to run against the sample database available on the [Programiz Online SQL Compiler](https://www.programiz.com/sql/online-compiler).

---

## 📊 Database Schema Reference

The examples below utilize three core tables from the compiler environment:

### `Customers`
* `customer_id` (int)
* `first_name` (varchar)
* `last_name` (varchar)
* `age` (int)
* `country` (varchar)

### `Orders`
* `order_id` (integer)
* `item` (varchar)
* `amount` (integer)
* `customer_id` (integer)

### `Shippings`
* `shipping_id` (integer)
* `status` (varchar)
* `customer` (integer)

---

## 🔍 SQL Query Examples

### 1. SELECT * (Retrieve Everything)
Fetches all columns and rows from the `Customers` table.
```sql
SELECT * FROM Customers;
```

### 2. SELECT DISTINCT (Unique Values)
Lists all unique countries where customers are located, removing duplicates.
```sql
SELECT DISTINCT country FROM Customers;
```

### 3. WHERE (Filtering Data)
Retrieves the names of customers who are exactly 31 years old.
```sql
SELECT first_name, last_name 
FROM Customers 
WHERE age = 31;
```

### 4. GROUP BY & Aggregate Functions (Summarizing Data)
Counts how many orders were placed for each specific item type.
```sql
SELECT item, COUNT(order_id) AS total_orders
FROM Orders
GROUP BY item;
```

### 5. HAVING (Filtering Groups)
Finds items that have been ordered more than once by filtering grouped results.
```sql
SELECT item, COUNT(order_id) AS total_orders
FROM Orders
GROUP BY item
HAVING COUNT(order_id) > 1;
```

### 6. ORDER BY (Sorting Results)
Lists customers sorted alphabetically by their last name.
```sql
SELECT first_name, last_name 
FROM Customers
ORDER BY last_name ASC;
```

### 7. LIMIT (Constraining Rows)
Returns only the top 3 highest-priced orders.
```sql
SELECT order_id, item, amount 
FROM Orders
ORDER BY amount DESC
LIMIT 3;
```

### 8. JOIN (Combining Tables)
Combines data from `Customers` and `Orders` to show what each customer bought.
```sql
SELECT Customers.first_name, Orders.item, Orders.amount
FROM Customers
JOIN Orders ON Customers.customer_id = Orders.customer_id;
```

---

## 🛠️ How to Test These Queries
1. Open the [Programiz Online SQL Compiler](https://www.programiz.com/sql/online-compiler).
2. Clear the default query in the editor.
3. Copy and paste any of the examples above.
4. Click the **Run SQL** button to view the output.

# UPDATE & DELETE OPERATIONS IN CRUD

This repository contains a structured, hands-on lab environment for mastering **Data Manipulation Language (DML)** operations using the default database instance provided in the [Programiz Online SQL Editor](https://www.programiz.com/sql/online-compiler/). 

---

## 📊 Database Schema Overview

The default Programiz compiler environment includes three connected tables:

1.  **`Customers`**: `customer_id` (PK), `first_name`, `last_name`, `age`, `country`
2.  **`Orders`**: `order_id` (PK), `item`, `amount`, `customer_id` (FK)
3.  **`Shippings`**: `shipping_id` (PK), `status`, `customer_id` (FK)

---

## 🛠️ Part 1: `UPDATE` Statements

The `UPDATE` statement modifies existing records matching specific criteria. Always ensure your `WHERE` clauses are precise to prevent accidental dataset rewrites.

### Practicals & Challenges

#### Task 1.1: Single Column Modification
**Scenario:** A customer named *John* wants to change his residence status. Update the record for the customer with `customer_id = 1` so that their country becomes `'UK'`.

```sql
UPDATE Customers 
SET country = 'UK' 
WHERE customer_id = 1;
```

#### Task 1.2: Multi-Column Modification
**Scenario:** Customer `customer_id = 4` has officially changed their legal name and updated their demographic profiles. Change their `first_name` to `'Robert'`, `last_name` to `'Downey'`, and `age` to `45`.

```sql
UPDATE Customers 
SET first_name = 'Robert', 
    last_name = 'Downey', 
    age = 45 
WHERE customer_id = 4;
```

#### Task 1.3: Calculation-Driven Updates
**Scenario:** Due to inflation and rising courier surcharges, update the `Orders` table to increase the order `amount` by **10%** for all items listed as a `'Keyboard'`.

```sql
UPDATE Orders 
SET amount = amount * 1.10 
WHERE item = 'Keyboard';
```

#### Task 1.4: Update via Conditional Strings
**Scenario:** The logistics vendor has updated their status naming conventions. Change any shipping records with a status of `'pending'` to read `'Processing'`.

```sql
UPDATE Shippings 
SET status = 'Processing' 
WHERE status = 'pending';
```

---

## 🗑️ Part 2: `DELETE` Statements

The `DELETE` statement permanently drops rows from target tables. 

> ⚠️ **Warning on Foreign Keys:** Since `Orders` and `Shippings` rely on `customer_id` values generated in the `Customers` table, deleting a customer that has active orders will violate referential integrity constraints. Clean up or reassign child dependencies first!

### Practicals & Challenges

#### Task 2.1: Simple Evaluated Deletion
**Scenario:** A customer has canceled their order before fulfillment. Delete the order record where `order_id = 3`.

```sql
DELETE FROM Orders 
WHERE order_id = 3;
```

#### Task 2.2: Conditional Multi-Row Deletion
**Scenario:** Clear out low-value orders from the database. Delete all orders from the `Orders` table where the transaction value (`amount`) is less than or equal to `400`.

```sql
DELETE FROM Orders 
WHERE amount <= 400;
```

#### Task 2.3: Deleting via Text Logic
**Scenario:** A distribution hub failed. Delete all delivery listings from the `Shippings` table that have a status explicitly set to `'fail'`.

```sql
DELETE FROM Shippings 
WHERE status = 'fail';
```

#### Task 2.4: Sequential Deletion (Handling Dependencies)
**Scenario:** You need to completely purge user `customer_id = 2` from the active schema. To avoid integrity errors, you must drop their linked orders and shipping statuses first.

```sql
-- Step 1: Remove dependent records from the Orders table
DELETE FROM Orders WHERE customer_id = 2;

-- Step 2: Remove dependent records from the Shippings table
DELETE FROM Shippings WHERE customer_id = 2;

-- Step 3: Safely remove the user profile from the primary table
DELETE FROM Customers WHERE customer_id = 2;
```

---

## 🚀 Execution Instructions
1. Navigate to the online [Programiz SQL Compiler](https://www.programiz.com/sql/online-compiler/).
2. Clear any default placeholder queries out of the input work area.
3. Copy one of the practice exercises from this document, paste it into the console, and click **"Run Code"**.
4. To verify the mutations, execute a global query right after your modifications, such as:
   ```sql
   SELECT * FROM Customers;
   ```


