# SQL SELECT Statement Examples

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

## Someting Else

