# Experiment 2: DDL Commands

## AIM
To study and implement DDL commands and different types of constraints.

## THEORY

### 1. CREATE
Used to create a new relation (table).

**Syntax:**
```sql
CREATE TABLE (
  field_1 data_type(size),
  field_2 data_type(size),
  ...
);
```
### 2. ALTER
Used to add, modify, drop, or rename fields in an existing relation.
(a) ADD
```sql
ALTER TABLE std ADD (Address CHAR(10));
```
(b) MODIFY
```sql
ALTER TABLE relation_name MODIFY (field_1 new_data_type(size));
```
(c) DROP
```sql
ALTER TABLE relation_name DROP COLUMN field_name;
```
(d) RENAME
```sql
ALTER TABLE relation_name RENAME COLUMN old_field_name TO new_field_name;
```
### 3. DROP TABLE
Used to permanently delete the structure and data of a table.
```sql
DROP TABLE relation_name;
```
### 4. RENAME
Used to rename an existing database object.
```sql
RENAME TABLE old_relation_name TO new_relation_name;
```
### CONSTRAINTS
Constraints are used to specify rules for the data in a table. If there is any violation between the constraint and the data action, the action is aborted by the constraint. It can be specified when the table is created (using CREATE TABLE) or after it is created (using ALTER TABLE).
### 1. NOT NULL
When a column is defined as NOT NULL, it becomes mandatory to enter a value in that column.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) NOT NULL
);
```
### 2. UNIQUE
Ensures that values in a column are unique.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) UNIQUE
);
```
### 3. CHECK
Specifies a condition that each row must satisfy.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) CHECK (logical_expression)
);
```
### 4. PRIMARY KEY
Used to uniquely identify each record in a table.
Properties:
Must contain unique values.
Cannot be null.
Should contain minimal fields.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) PRIMARY KEY
);
```
### 5. FOREIGN KEY
Used to reference the primary key of another table.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size),
  FOREIGN KEY (column_name) REFERENCES other_table(column)
);
```
### 6. DEFAULT
Used to insert a default value into a column if no value is specified.

Syntax:
```sql
CREATE TABLE Table_Name (
  col_name1 data_type,
  col_name2 data_type,
  col_name3 data_type DEFAULT 'default_value'
);
```

**Question 1**

Write a SQL Query  to add attribute ISBN as varchar(30) and domain_dept as varchar(30) in the table 'books'

```sql

ALTER TABLE books
ADD COLUMN ISBN varchar(30);

ALTER TABLE books
ADD COLUMN domain_dept varchar(30);

```

**Output:**

<img width="1231" height="501" alt="image" src="https://github.com/user-attachments/assets/28c4ba8a-5d40-4f99-ab6d-02cdc20f0990" />

**Question 2**

Create a table named Employees with the following constraints:

EmployeeID should be the primary key.
FirstName and LastName should be NOT NULL.
Email should be unique.
Salary should be greater than 0.
DepartmentID should be a foreign key referencing the Departments table.

```sql

CREATE TABLE Employees(
EmployeeID INT PRIMARY KEY,
FirstName TEXT NOT NULL,
LastName TEXT NOT NULL,
Email TEXT UNIQUE,
Salary INT CHECK(Salary > 0),
DepartmentID INT,
FOREIGN KEY(DepartmentID) REFERENCES Departments
);

```

**Output:**

<img width="1237" height="542" alt="image" src="https://github.com/user-attachments/assets/58a21621-76a8-44e1-9b7c-7b43c589f37d" />

**Question 3**

In the Products table, insert a record where some fields are NULL, another record where all fields are filled without any NULL values, and a third record where some fields are filled, and others are left as NULL.

| ProductID | Name             | Category     | Price   | Stock |
|------------|------------------|--------------|---------|-------|
| 106        | Fitness Tracker  | Wearables    |         |       |
| 107        | Laptop           | Electronics  | 999.99  | 50    |
| 108        | Wireless Earbuds | Accessories  |         | 100   |

```sql

INSERT INTO Products(ProductID,Name,Category,Price,Stock)
VALUES(106,'Fitness Tracker','Wearables',NULL,NULL),
(107,'Laptop','Electronics',999.99,50),
(108,'Wireless Earbuds','Accessories',NULL,100);

```

**Output:**

<img width="1240" height="409" alt="image" src="https://github.com/user-attachments/assets/80ad7bd3-a29c-4509-a239-d7b8e3da092a" />

**Question 4**

Insert the below data into the Customers table, allowing the City and ZipCode columns to take their default values.

| CustomerID | Name          | Address   |
|-------------|---------------|-----------|
| 304         | Peter Parker  | Spider St |
      

```sql

INSERT INTO Customers(CustomerID,Name,Address)
VALUES(304,'Peter Parker','Spider St');

```

**Output:**

<img width="1237" height="428" alt="image" src="https://github.com/user-attachments/assets/adc2743f-53c5-4502-81ab-1a07dcf2807a" />

**Question 5**

Create a table named Reviews with the following columns:

ReviewID as INTEGER
ProductID as INTEGER
Rating as REAL
ReviewText as TEXT

```sql

CREATE TABLE Reviews(
ReviewID INTEGER,
ProductID INTEGER,
Rating REAL,
ReviewText TEXT
);

```

**Output:**

<img width="1240" height="521" alt="image" src="https://github.com/user-attachments/assets/194b323f-4237-4ce9-b0d1-380be112e194" />

**Question 6**

Create a table named Invoices with the following constraints:

InvoiceID as INTEGER should be the primary key.
InvoiceDate as DATE.
DueDate as DATE should be greater than the InvoiceDate.
Amount as REAL should be greater than 0.

```sql

CREATE TABLE Invoices(
InvoiceID INTEGER PRIMARY KEY,
InvoiceDate DATE,
DueDate DATE CHECK(DueDate > InvoiceDate),
Amount REAL CHECK(Amount > 0)
);

```

**Output:**

<img width="1239" height="407" alt="image" src="https://github.com/user-attachments/assets/c0bbfd47-2896-472a-9663-daca6bae2914" />

**Question 7**

Create a table named Orders with the following constraints:
OrderID as INTEGER should be the primary key.
OrderDate as DATE should be not NULL.
CustomerID as INTEGER should be a foreign key referencing Customers(CustomerID).

```sql

CREATE TABLE Orders(
OrderID INTEGER PRIMARY KEY,
OrderDate DATE NOT NULL,
CustomerID INTEGER,
FOREIGN KEY(CustomerID) REFERENCES Customers(CustomerID)
);

```

**Output:**

<img width="1231" height="403" alt="image" src="https://github.com/user-attachments/assets/ce3b4bdd-6378-4706-899f-d78f9ff20eee" />

**Question 8**

Insert all customers from Old_customers into Customers

Table attributes are CustomerID, Name, Address, Email

```sql

INSERT INTO Customers
SELECT CustomerID,Name,Address,Email
FROM Old_customers;

```

**Output:**

<img width="1236" height="422" alt="image" src="https://github.com/user-attachments/assets/8ac2a7a4-62b9-47c6-8d65-4b71bdc9477e" />

**Question 9**

Write a SQL query to Add a new column named "discount" with the data type DECIMAL(5,2) to the "customer" table.

Sample table: customer

| customer_id | cust_name    | city        | grade | salesman_id |
|--------------|--------------|-------------|--------|--------------|
| 3002         | Nick Rimando | New York    | 100    | 5001         |
| 3007         | Brad Davis   | New York    | 200    | 5001         |
| 3005         | Graham Zusi  | California  | 200    | 5002         |


```sql

ALTER TABLE customer
ADD COLUMN discount DECIMAL(5,2);

```

**Output:**

<img width="1237" height="480" alt="image" src="https://github.com/user-attachments/assets/ff151fd7-8176-48c2-9b8d-07cb365ac698" />

**Question 10**

Create a table named Bonuses with the following constraints:
BonusID as INTEGER should be the primary key.
EmployeeID as INTEGER should be a foreign key referencing Employees(EmployeeID).
BonusAmount as REAL should be greater than 0.
BonusDate as DATE.
Reason as TEXT should not be NULL.

```sql

CREATE TABLE Bonuses(
BonusID INTEGER PRIMARY KEY,
EmployeeID INTEGER,
BonusAmount REAL CHECK(BonusAmount > 0),
BonusDate DATE,
Reason TEXT NOT NULL,
FOREIGN KEY(EmployeeID) REFERENCES Employees(EmployeeID)
);

```

**Output:**

<img width="1232" height="406" alt="image" src="https://github.com/user-attachments/assets/eaa10659-2eeb-4d18-89c2-d5be242f17be" />

## RESULT
Thus, the SQL queries to implement different types of constraints and DDL commands have been executed successfully.
