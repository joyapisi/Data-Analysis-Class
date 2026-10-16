## CAT I and CAT II — 30 points

PART I: Data Fundamentals and Careers

Suggested duration: 30 minutes

- Explain the responsibilities of a data analyst. (3 points)
- Given the dataset below, identify its rows, columns, and variables. (6 points)
  
```sql
-- Create Customers Table
CREATE TABLE Customers (
    CustomerID INT PRIMARY KEY,
    FirstName VARCHAR(50),
    LastName VARCHAR(50),
    Email VARCHAR(100),
    Country VARCHAR(50),
    SignupDate DATE
);

-- Create Products Table
CREATE TABLE Products (
    ProductID INT PRIMARY KEY,
    ProductName VARCHAR(100),
    Category VARCHAR(50),
    Price DECIMAL(10, 2),
    StockQuantity INT
);

-- Create Orders Table
CREATE TABLE Orders (
    OrderID INT PRIMARY KEY,
    CustomerID INT,
    ProductID INT,
    OrderDate DATE,
    Quantity INT,
    TotalAmount DECIMAL(10, 2),
    FOREIGN KEY (CustomerID) REFERENCES Customers(CustomerID),
    FOREIGN KEY (ProductID) REFERENCES Products(ProductID)
);
```


- Interpret this simple chart and state two findings. (6 points)
<img width="968" height="563" alt="image" src="https://github.com/user-attachments/assets/a442059c-118e-41aa-8f8f-416188e1d86e" />


## 15

points

PART II: Practical Data Analysis

Suggested duration: 40–50 minutes

- Use WDI to import or open a supplied dataset. (5 points)
- Create an appropriate chart using ggplot2. (4 points)
- Identify a trend, comparison, or unusual observation. (3 points)

- Write a short evidence-based conclusion. (3 points)

## 5.  assessment schedule

| Assessment            | Suggested timing                                            | points |
| --------------------- | ----------------------------------------------------------- | ----- |
| CAT I                 | After the introductory careers and data concepts lessons    | 15    |
| CAT II                | After students have worked with datasets and visualizations | 15    |
| Total                 |                                                             | 30    |



