# Experiment 6: Joins

## AIM
To study and implement different types of joins.

## THEORY

SQL Joins are used to combine records from two or more tables based on a related column.

### 1. INNER JOIN
Returns records with matching values in both tables.

**Syntax:**
```sql
SELECT columns
FROM table1
INNER JOIN table2
ON table1.column = table2.column;
```

### 2. LEFT JOIN
Returns all records from the left table, and matched records from the right.

**Syntax:**

```sql
SELECT columns
FROM table1
LEFT JOIN table2
ON table1.column = table2.column;
```
### 3. RIGHT JOIN
Returns all records from the right table, and matched records from the left.

**Syntax:**

```sql
SELECT columns
FROM table1
RIGHT JOIN table2
ON table1.column = table2.column;
```
### 4. FULL OUTER JOIN
Returns all records when there is a match in either left or right table.

**Syntax:**

```sql
SELECT columns
FROM table1
FULL OUTER JOIN table2
ON table1.column = table2.column;
```

**Question 1**
From the following tables write a SQL query to display the customer name, customer city, grade, salesman, salesman city. The results should be sorted by ascending customer_id.  

Sample table: customer

| customer_id | cust_name      | city        | grade | salesman_id |
|--------------|----------------|-------------|--------|--------------|
| 3002         | Nick Rimando   | New York    | 100    | 5001         |
| 3007         | Brad Davis     | New York    | 200    | 5001         |
| 3005         | Graham Zusi    | California  | 200    | 5002         |
| 3008         | Julian Green   | London      | 300    | 5002         |
| 3004         | Fabian Johnson | Paris       | 300    | 5006         |
| 3009         | Geoff Cameron  | Berlin      | 100    | 5003         |
| 3003         | Jozy Altidor   | Moscow      | 200    | 5007         |
| 3001         | Brad Guzan     | London      |        | 5005         |

Sample table: salesman

| salesman_id | name        | city       | commission |
|--------------|-------------|------------|-------------|
| 5001         | James Hoog  | New York   | 0.15        |
| 5002         | Nail Knite  | Paris      | 0.13        |
| 5005         | Pit Alex    | London     | 0.11        |
| 5006         | Mc Lyon     | Paris      | 0.14        |
| 5007         | Paul Adam   | Rome       | 0.13        |
| 5003         | Lauson Hen  | San Jose   | 0.12        |


```sql

SELECT c.cust_name,
       c.city,
       c.grade,
       s.name AS Salesman,
       s.city
FROM customer c
JOIN salesman s ON c.salesman_id = s.salesman_id
ORDER BY c.customer_id ASC;


```

**Output:**

<img width="1338" height="754" alt="image" src="https://github.com/user-attachments/assets/08a468c1-5208-4a31-aa65-a6021873e3b8" />

**Question 2**

Write the SQL query that achieves the selection of the first name from the "patients" table and all columns from the "surgeries" table, with an inner join on the "patient_id" column. Include conditions to filter for patients discharged between '2024-03-01' and '2024-03-31' but not admitted during the same period.

PATIENTS TABLE:

name             type
---------------  ---------------
patient_id       INT
first_name       VARCHAR(50)
last_name        VARCHAR(50)
date_of_birth    DATE
admission_date   DATE
discharge_date   DATE
doctor_id        INT

SURGERIES TABLE:

name             type
---------------  ---------------
surgery_id       INT
patient_id       INT
surgeon_id       INT
surgery_date     DATE

```sql

SELECT p.first_name,
       s.surgery_id,
       s.patient_id,
       s.surgeon_id,
       s.surgery_date
FROM patients p
INNER JOIN surgeries s
ON p.patient_id = s.patient_id
WHERE p.discharge_date BETWEEN '2024-03-01' AND '2024-03-31'
  AND (p.admission_date < '2024-03-01' OR p.admission_date > '2024-03-31');

```

**Output:**

<img width="1334" height="395" alt="image" src="https://github.com/user-attachments/assets/278bcf00-367e-4957-b67b-ebc566b4f977" />

**Question 3**

Write the SQL query that achieves the selection of all columns from the "patients" table (aliased as "p"), with an inner join on the "patient_id" column and a condition filtering for appointments with an appointment date between '2024-02-01' and '2024-02-28'.

PATIENTS TABLE:

ATTRIBUTES - patient_id, first_name, last_name, date_of_birth, admission_date, discharge_date, doctor_id


APPOINTMENTS TABLE:

ATTRIBUTES - appointment_id, patient_id, doctor_id, appointment_date

```sql

SELECT p.*
FROM patients p
INNER JOIN appointments a
ON p.patient_id = a.patient_id
WHERE a.appointment_date BETWEEN '2024-02-01' AND '2024-02-28';

```

**Output:**

<img width="1330" height="415" alt="image" src="https://github.com/user-attachments/assets/f282c747-55f4-4cff-9d1a-d9dfdd284691" />

**Question 4**

Write the SQL query that achieves the selection of the "name" column from the "salesman" table (aliased as "salesman_name") and the "cust_name" column from the "customer" table (aliased as "customer_name"), with a left join on the "salesman_id" column.

Customer Table: (customer_id, cust_name, city, grade, salesman_id)

Salesman Table: (salesman_id, name, city, commission)

```sql

SELECT s.name AS salesman_name,
       c.cust_name AS customer_name
FROM salesman s
LEFT JOIN customer c
ON s.salesman_id = c.salesman_id;

```

**Output:**

<img width="713" height="813" alt="image" src="https://github.com/user-attachments/assets/4ee21790-306e-43a0-a7cd-812773c04805" />

**Question 5**

From the following tables write a SQL query to find those orders where the order amount exists between 500 and 2000. Return ord_no, purch_amt, cust_name, city.

Sample table: customer

| customer_id | cust_name      | city        | grade | salesman_id |
|--------------|----------------|-------------|--------|--------------|
| 3002         | Nick Rimando   | New York    | 100    | 5001         |
| 3007         | Brad Davis     | New York    | 200    | 5001         |
| 3005         | Graham Zusi    | California  | 200    | 5002         |
| 3008         | Julian Green   | London      | 300    | 5002         |
| 3004         | Fabian Johnson | Paris       | 300    | 5006         |
| 3009         | Geoff Cameron  | Berlin      | 100    | 5003         |
| 3003         | Jozy Altidor   | Moscow      | 200    | 5007         |
| 3001         | Brad Guzan     | London      |        | 5005         |

Sample table: orders

| ord_no | purch_amt | ord_date   | customer_id | salesman_id |
|--------|------------|------------|--------------|--------------|
| 70001  | 150.50     | 2012-10-05 | 3005         | 5002         |
| 70009  | 270.65     | 2012-09-10 | 3001         | 5005         |
| 70002  | 65.26      | 2012-10-05 | 3002         | 5001         |
| 70004  | 110.50     | 2012-08-17 | 3009         | 5003         |
| 70007  | 948.50     | 2012-09-10 | 3005         | 5002         |
| 70005  | 2400.60    | 2012-07-27 | 3007         | 5001         |
| 70008  | 5760.00    | 2012-09-10 | 3002         | 5001         |
| 70010  | 1983.43    | 2012-10-10 | 3004         | 5006         |
| 70003  | 2480.40    | 2012-10-10 | 3009         | 5003         |
| 70012  | 250.45     | 2012-06-27 | 3008         | 5002         |
| 70011  | 75.29      | 2012-08-17 | 3003         | 5007         |
| 70013  | 3045.60    | 2012-04-25 | 3002         | 5001         |


```sql

SELECT o.ord_no,
       o.purch_amt,
       c.cust_name,
       c.city
FROM orders o
JOIN customer c
ON o.customer_id = c.customer_id
WHERE o.purch_amt BETWEEN 500 AND 2000;

```

**Output:**

<img width="1324" height="453" alt="image" src="https://github.com/user-attachments/assets/aa16649a-1b90-478d-ae8c-acd8cdef1377" />

**Question 6**

write a SQL query to find the salesperson and customer who reside in the same city. Return Salesman, cust_name and city.

Sample table: salesman

| salesman_id | name        | city       | commission |
|--------------|-------------|------------|-------------|
| 5001         | James Hoog  | New York   | 0.15        |
| 5002         | Nail Knite  | Paris      | 0.13        |
| 5005         | Pit Alex    | London     | 0.11        |
| 5006         | Mc Lyon     | Paris      | 0.14        |
| 5007         | Paul Adam   | Rome       | 0.13        |
| 5003         | Lauson Hen  | San Jose   | 0.12        |

Sample table: customer

| customer_id | cust_name      | city        | grade | salesman_id |
|--------------|----------------|-------------|--------|--------------|
| 3002         | Nick Rimando   | New York    | 100    | 5001         |
| 3007         | Brad Davis     | New York    | 200    | 5001         |
| 3005         | Graham Zusi    | California  | 200    | 5002         |
| 3008         | Julian Green   | London      | 300    | 5002         |
| 3004         | Fabian Johnson | Paris       | 300    | 5006         |
| 3009         | Geoff Cameron  | Berlin      | 100    | 5003         |
| 3003         | Jozy Altidor   | Moscow      | 200    | 5007         |
| 3001         | Brad Guzan     | London      |        | 5005         |


```sql

SELECT s.name AS Salesman,
       c.cust_name,
       c.city
FROM salesman s
JOIN customer c
ON s.city = c.city;

```

**Output:**

<img width="998" height="630" alt="image" src="https://github.com/user-attachments/assets/de164e4c-d319-4474-865b-463872dde385" />

**Question 7**

From the following tables write a SQL query to find the salesperson(s) and the customer(s) he represents. Return Customer Name, city, Salesman, commission.

Sample table: customer

| customer_id | cust_name      | city        | grade | salesman_id |
|--------------|----------------|-------------|--------|--------------|
| 3002         | Nick Rimando   | New York    | 100    | 5001         |
| 3007         | Brad Davis     | New York    | 200    | 5001         |
| 3005         | Graham Zusi    | California  | 200    | 5002         |
| 3008         | Julian Green   | London      | 300    | 5002         |
| 3004         | Fabian Johnson | Paris       | 300    | 5006         |
| 3009         | Geoff Cameron  | Berlin      | 100    | 5003         |
| 3003         | Jozy Altidor   | Moscow      | 200    | 5007         |
| 3001         | Brad Guzan     | London      |        | 5005         |

Sample table: salesman

| salesman_id | name        | city       | commission |
|--------------|-------------|------------|-------------|
| 5001         | James Hoog  | New York   | 0.15        |
| 5002         | Nail Knite  | Paris      | 0.13        |
| 5005         | Pit Alex    | London     | 0.11        |
| 5006         | Mc Lyon     | Paris      | 0.14        |
| 5007         | Paul Adam   | Rome       | 0.13        |
| 5003         | Lauson Hen  | San Jose   | 0.12        |


```sql

SELECT c.cust_name AS "Customer Name",
       c.city,
       s.name AS "Salesman",
       s.commission
FROM customer c
JOIN salesman s
ON c.salesman_id = s.salesman_id;

```

**Output:**

<img width="1331" height="811" alt="image" src="https://github.com/user-attachments/assets/2cd9af31-974e-4eac-bd7b-e3f7656a84c6" />

**Question 8**

Write a SQL statement to make a report with customer name, city, order number, order date, and order amount in ascending order according to the order date to determine whether any of the existing customers have placed an order or not.

Sample table: orders

| ord_no | purch_amt | ord_date   | customer_id | salesman_id |
|--------|------------|------------|--------------|--------------|
| 70001  | 150.50     | 2012-10-05 | 3005         | 5002         |
| 70009  | 270.65     | 2012-09-10 | 3001         | 5005         |
| 70002  | 65.26      | 2012-10-05 | 3002         | 5001         |
| 70004  | 110.50     | 2012-08-17 | 3009         | 5003         |
| 70007  | 948.50     | 2012-09-10 | 3005         | 5002         |
| 70005  | 2400.60    | 2012-07-27 | 3007         | 5001         |
| 70008  | 5760.00    | 2012-09-10 | 3002         | 5001         |
| 70010  | 1983.43    | 2012-10-10 | 3004         | 5006         |
| 70003  | 2480.40    | 2012-10-10 | 3009         | 5003         |
| 70012  | 250.45     | 2012-06-27 | 3008         | 5002         |
| 70011  | 75.29      | 2012-08-17 | 3003         | 5007         |
| 70013  | 3045.60    | 2012-04-25 | 3002         | 5001         |

Sample table: customer

| customer_id | cust_name      | city        | grade | salesman_id |
|--------------|----------------|-------------|--------|--------------|
| 3002         | Nick Rimando   | New York    | 100    | 5001         |
| 3007         | Brad Davis     | New York    | 200    | 5001         |
| 3005         | Graham Zusi    | California  | 200    | 5002         |
| 3008         | Julian Green   | London      | 300    | 5002         |
| 3004         | Fabian Johnson | Paris       | 300    | 5006         |
| 3009         | Geoff Cameron  | Berlin      | 100    | 5003         |
| 3003         | Jozy Altidor   | Moscow      | 200    | 5007         |
| 3001         | Brad Guzan     | London      |        | 5005         |

```sql

SELECT c.cust_name,
       c.city,
       o.ord_no,
       o.ord_date,
       o.purch_amt AS "Order Amount"
FROM customer c
LEFT JOIN orders o
ON c.customer_id = o.customer_id
ORDER BY o.ord_date ASC;

```

**Output:**

<img width="1095" height="861" alt="image" src="https://github.com/user-attachments/assets/fb9f66ab-6272-4eec-9c62-f85377941050" />

**Question 9**

Write an SQL query that retrieves all columns from the 'customer' table (using the alias 'c'), performs a LEFT JOIN with the 'orders' table on the 'customer_id' column, and includes only those orders with an order date after '2012-08-17'.

'customer' Table: (customer_id, cust_name, city, grade, salesman_id)

'orders' Table: (ord_no, purch_amt, ord_date, customer_id, salesman_id)

```sql

SELECT c.*
FROM customer c
LEFT JOIN orders o
ON c.customer_id = o.customer_id
WHERE o.ord_date > '2012-08-17';

```

**Output:**

<img width="1333" height="748" alt="image" src="https://github.com/user-attachments/assets/f08fa239-3c66-404c-a008-4ce50a7c25d4" />

**Question 10**

Write the SQL query that accomplishes the selection of all columns from the "patients" table and the first name of doctors from the "doctors" table, with an inner join on the "doctor_id" column.

PATIENTS TABLE:
name             type
---------------  ---------------
patient_id       INT
first_name       VARCHAR(50)
last_name        VARCHAR(50)
date_of_birth    DATE
admission_date   DATE
discharge_date   DATE
doctor_id        INT

DOCTORS TABLE:

name             type
---------------  ---------------
doctor_id        INT
first_name       VARCHAR(50)
last_name        VARCHAR(50)
specialization   VARCHAR(100)

```sql

SELECT p.*,
       d.first_name AS doctor_name
FROM patients p
INNER JOIN doctors d
ON p.doctor_id = d.doctor_id;

```

**Output:**

<img width="1334" height="535" alt="image" src="https://github.com/user-attachments/assets/395ac611-572a-49e8-8e84-acedbb4588ec" />



## RESULT
Thus, the SQL queries to implement different types of joins have been executed successfully.
