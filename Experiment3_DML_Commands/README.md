# Experiment 3: DML Commands

## AIM
To study and implement DML (Data Manipulation Language) commands.

## THEORY

### 1. INSERT INTO
Used to add records into a relation.
These are three type of INSERT INTO queries which are as
A)Inserting a single record
**Syntax (Single Row):**
```sql
INSERT INTO table_name (field_1, field_2, ...) VALUES (value_1, value_2, ...);
```
**Syntax (Multiple Rows):**
```sql
INSERT INTO table_name (field_1, field_2, ...) VALUES
(value_1, value_2, ...),
(value_3, value_4, ...);
```
**Syntax (Insert from another table):**
```sql
INSERT INTO table_name SELECT * FROM other_table WHERE condition;
```
### 2. UPDATE
Used to modify records in a relation.
Syntax:
```sql
UPDATE table_name SET column1 = value1, column2 = value2 WHERE condition;
```
### 3. DELETE
Used to delete records from a relation.
**Syntax (All rows):**
```sql
DELETE FROM table_name;
```
**Syntax (Specific condition):**
```sql
DELETE FROM table_name WHERE condition;
```
### 4. SELECT
Used to retrieve records from a table.
**Syntax:**
```sql
SELECT column1, column2 FROM table_name WHERE condition;
```
**Question 1**

Write a SQL statement to Update the per_unit_price to 25 and total_price accordingly in purchases table where purchase_date is '2022-08-15' and product_id is 12.

```sql

UPDATE purchases
SET per_unit_price = 25
WHERE purchase_date = '2022-08-15' AND product_id = 12;

UPDATE purchases
SET total_price = quantity * per_unit_price
WHERE purchase_date = '2022-08-15' AND product_id = 12;

```

**Output:**

<img width="1233" height="615" alt="image" src="https://github.com/user-attachments/assets/45d98aa5-6da5-45e6-83c2-958b7f667eb3" />


**Question 2**

Write a SQL statement to Increase quantity of all products by 10% to adjust for surplus stock counted

Products table

---------------
product_id
product_name
category
cost_price
sell_price
reorder_lvl
quantity
supplier_id

```sql

UPDATE Products
SET quantity = quantity * 1.10;

```

**Output:**

<img width="1223" height="712" alt="image" src="https://github.com/user-attachments/assets/fcf94a45-3107-4a7d-98e8-34736c0743b8" />

**Question 3**

Write a SQL query to reduce the reorder level by 30% where cost price is more than 50 and quantity in stock is less than 100 in the products table.

Products Table 

name          type       
----------    ---------- 
product_id     INT PRIMARY KEY        
product_name   VARCHAR(10) 
category       VARCHAR(50) 
cost_price     DECIMAL(10) 
sell_price     DECIMAL(10) 
reorder_lvl    INT        
quantity       INT        
supplier_id    INT               
For example:

```sql

UPDATE Products
SET reorder_lvl = reorder_lvl * 0.70
WHERE cost_price > 50 AND quantity < 100;

```

**Output:**

<img width="1232" height="539" alt="image" src="https://github.com/user-attachments/assets/a49be8ce-ca9c-4617-9c61-3d47fd2cc273" />


**Question 4**

Write a SQL statement to Update the reorder level to 20 where the quantity in stock is less than 10 and product category is 'Snacks' in the products table.

Products table

---------------
product_id
product_name
category
cost_price
sell_price
reorder_lvl
quantity
supplier_id

```sql

UPDATE Products
SET reorder_lvl = 20
WHERE quantity < 10 AND category = 'Snacks';

```

**Output:**

<img width="1234" height="665" alt="image" src="https://github.com/user-attachments/assets/9dc428fe-6f06-4c68-b5ec-583873876764" />

**Question 5**

Change the supplier name to upper case where contact person contains ' Singh' in suppliers table.

name               type
-----------------  ---------------
supplier_id        INT
supplier_name      VARCHAR(100)
contact_person     VARCHAR(100)
phone_number       VARCHAR(20)
email              VARCHAR(100)
address            VARCHAR(250)

```sql

UPDATE suppliers
SET supplier_name = UPPER(supplier_name)
WHERE contact_person LIKE '%Singh%';

```

**Output:**

<img width="1236" height="447" alt="image" src="https://github.com/user-attachments/assets/926d4119-2bcb-4cf4-982c-0360bd34c3e4" />

**Question 6**

Write a SQL query to Delete customers with 'CUST_COUNTRY' 'UK' and 'WORKING_AREA' 'London' whose 'GRADE' is less than 3

Sample table: Customer

| CUST_CODE | CUST_NAME | CUST_CITY | WORKING_AREA | CUST_COUNTRY | GRADE | OPENING_AMT | RECEIVE_AMT | PAYMENT_AMT | OUTSTANDING_AMT | PHONE_NO | AGENT_CODE |
|------------|------------|------------|----------------|----------------|--------|----------------|----------------|----------------|------------------|--------------|--------------|
| C00013 | Holmes | London | London | UK | 2 | 6000.00 | 5000.00 | 7000.00 | 4000.00 | BBBBBBB | A003 |
| C00001 | Micheal | New York | New York | USA | 2 | 3000.00 | 5000.00 | 2000.00 | 6000.00 | CCCCCCC | A008 |
| C00020 | Albert | New York | New York | USA | 3 | 5000.00 | 7000.00 | 6000.00 | 6000.00 | BBBBSBB | A008 |


```sql

DELETE FROM Customer
WHERE CUST_COUNTRY = 'UK' AND WORKING_AREA = 'London' AND GRADE < 3;

```

**Output:**

<img width="1235" height="565" alt="image" src="https://github.com/user-attachments/assets/8730f23f-94ac-4032-ac79-ad3ef9fe9ab3" />

**Question 7**

Write a SQL query to delete a specific doctor from Doctors table whose ID is 1.

Sample table: Doctors

attributes : doctor_id, first_name, last_name, specialization

```sql

DELETE FROM Doctors
WHERE doctor_id = 1;

```

**Output:**

<img width="1235" height="353" alt="image" src="https://github.com/user-attachments/assets/82f86ac4-b72a-4518-a520-83924f992264" />

**Question 8**

Write a SQL query to Delete customers with 'GRADE' 2 and 'CUST_NAME' starting with 'M', and whose 'PAYMENT_AMT' is less than 3000

Sample table: Customer

| CUST_CODE | CUST_NAME | CUST_CITY | WORKING_AREA | CUST_COUNTRY | GRADE | OPENING_AMT | RECEIVE_AMT | PAYMENT_AMT | OUTSTANDING_AMT | PHONE_NO | AGENT_CODE |
|------------|------------|------------|----------------|----------------|--------|----------------|----------------|----------------|------------------|--------------|--------------|
| C00013 | Holmes | London | London | UK | 2 | 6000.00 | 5000.00 | 7000.00 | 4000.00 | BBBBBBB | A003 |
| C00001 | Micheal | New York | New York | USA | 2 | 3000.00 | 5000.00 | 2000.00 | 6000.00 | CCCCCCC | A008 |
| C00020 | Albert | New York | New York | USA | 3 | 5000.00 | 7000.00 | 6000.00 | 6000.00 | BBBBSBB | A008 |


```sql

DELETE FROM Customer
WHERE GRADE = 2 AND CUST_NAME LIKE '%M%' AND PAYMENT_AMT < 3000;

```

**Output:**

<img width="1233" height="487" alt="image" src="https://github.com/user-attachments/assets/ddd01495-1e61-4956-a560-b55a94ff041a" />

**Question 9**

Write a SQL query to Delete customers from 'customer' table where 'GRADE' is odd.

Sample table: Customer

| CUST_CODE | CUST_NAME | CUST_CITY | WORKING_AREA | CUST_COUNTRY | GRADE | OPENING_AMT | RECEIVE_AMT | PAYMENT_AMT | OUTSTANDING_AMT | PHONE_NO | AGENT_CODE |
|------------|------------|------------|----------------|----------------|--------|----------------|----------------|----------------|------------------|--------------|--------------|
| C00013 | Holmes | London | London | UK | 2 | 6000.00 | 5000.00 | 7000.00 | 4000.00 | BBBBBBB | A003 |
| C00001 | Micheal | New York | New York | USA | 2 | 3000.00 | 5000.00 | 2000.00 | 6000.00 | CCCCCCC | A008 |
| C00020 | Albert | New York | New York | USA | 3 | 5000.00 | 7000.00 | 6000.00 | 6000.00 | BBBBSBB | A008 |


```sql

DELETE FROM Customer
WHERE GRADE % 2 = 1;


```

**Output:**

<img width="1235" height="520" alt="image" src="https://github.com/user-attachments/assets/5650922c-47d1-4694-91be-ff40c6ab77bc" />

**Question 10**

Write a SQL query to Delete customers from 'customer' table where 'CUST_NAME' has exactly 6 characters.

Sample table: Customer

| CUST_CODE | CUST_NAME | CUST_CITY | WORKING_AREA | CUST_COUNTRY | GRADE | OPENING_AMT | RECEIVE_AMT | PAYMENT_AMT | OUTSTANDING_AMT | PHONE_NO | AGENT_CODE |
|------------|------------|------------|----------------|----------------|--------|----------------|----------------|----------------|------------------|--------------|--------------|
| C00013 | Holmes | London | London | UK | 2 | 6000.00 | 5000.00 | 7000.00 | 4000.00 | BBBBBBB | A003 |
| C00001 | Micheal | New York | New York | USA | 2 | 3000.00 | 5000.00 | 2000.00 | 6000.00 | CCCCCCC | A008 |
| C00020 | Albert | New York | New York | USA | 3 | 5000.00 | 7000.00 | 6000.00 | 6000.00 | BBBBSBB | A008 |


```sql

DELETE FROM Customer
WHERE LENGTH(CUST_NAME) = 6;

```

**Output:**

<img width="1232" height="834" alt="image" src="https://github.com/user-attachments/assets/f36c1803-e1d4-4562-8ba8-c313132e73f1" />

## RESULT
Thus, the SQL queries to implement DML commands have been executed successfully.
