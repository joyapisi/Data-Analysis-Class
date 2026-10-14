# CREATE OPERATION IN CRUD
## Creating a New Table in Programiz
Visit https://www.programiz.com/sql/online-compiler

Remove any commands present in the INPUT section and follow the steps below:
-- Step 1: Create the Payments table
```sql

CREATE TABLE Payments (
    payment_id INTEGER PRIMARY KEY,
    order_id INTEGER,
    payment_method VARCHAR(50),
    payment_status VARCHAR(50)
);
```

```sql
-- Step 2: Insert one transaction record for the Payments table
INSERT INTO Payments (payment_id, order_id, payment_method, payment_status) VALUES
(101, 1, 'Credit Card', 'Completed'),
```

```sql
-- Step 3: Insert multiple transaction records for the Payments table
INSERT INTO Payments (payment_id, order_id, payment_method, payment_status) VALUES
(102, 2, 'MPESA', 'Completed'),
(103, 3, 'Debit Card', 'Pending'),
(104, 4, 'Crypto', 'Failed'),
```
#### Class Assignment
```sql
-- Step 4: Insert the last transaction record for the Payments table
```

### In week 6&7, we'll learn how to insert Large Amounts of Entities using what we call a SCHEMA FILE.
