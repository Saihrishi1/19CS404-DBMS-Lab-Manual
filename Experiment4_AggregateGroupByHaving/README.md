# Experiment 4: Aggregate Functions, Group By and Having Clause

## AIM
To study and implement aggregate functions, GROUP BY, and HAVING clause with suitable examples.

## THEORY

### Aggregate Functions
These perform calculations on a set of values and return a single value.

- **MIN()** – Smallest value  
- **MAX()** – Largest value  
- **COUNT()** – Number of rows  
- **SUM()** – Total of values  
- **AVG()** – Average of values

**Syntax:**
```sql
SELECT AGG_FUNC(column_name) FROM table_name WHERE condition;
```
### GROUP BY
Groups records with the same values in specified columns.
**Syntax:**
```sql
SELECT column_name, AGG_FUNC(column_name)
FROM table_name
GROUP BY column_name;
```
### HAVING
Filters the grouped records based on aggregate conditions.
**Syntax:**
```sql
SELECT column_name, AGG_FUNC(column_name)
FROM table_name
GROUP BY column_name
HAVING condition;
```

**Question 1**

How many patients have expired insurance coverage for each insurance company?

Sample table:Insurance Table

```sql

SELECT 
    InsuranceCompany,
    count(*) as TotalExpiredPatients
from Insurance
group by InsuranceCompany;

```

**Output:**

<img width="1238" height="833" alt="image" src="https://github.com/user-attachments/assets/5768e3d4-9bbd-488b-8e99-732e4573b0a8" />

**Question 2**

How many medical records are there for each patient?

Sample table:MedicalRecords Table

```sql

SELECT PatientID, COUNT(*) AS TotalRecords
FROM MedicalRecords
GROUP BY PatientID;

```

**Output:**

<img width="1230" height="748" alt="image" src="https://github.com/user-attachments/assets/f1ccf664-244f-4392-8f20-338e02619cce" />

**Question 3**

How many appointments are scheduled for each patient?

Sample table: Appointments Table

name                  type
--------------------  ----------
AppointmentID         INTEGER
PatientID             INTEGER
DoctorID              INTEGER
AppointmentDateTime   DATETIME
Purpose               TEXT
Status                TEXT

```sql

SELECT PatientID, COUNT(*) AS TotalAppointments
FROM Appointments
GROUP BY PatientID;

```

**Output:**

<img width="1227" height="720" alt="image" src="https://github.com/user-attachments/assets/e33edd58-3d95-4588-8164-ef9c2d47b577" />

**Question 4**

Write a SQL query to calculate the total number of working hours of all employees

Sample table: employee1

```sql

SELECT SUM(workhour) AS "Total working hours"
FROM employee1;

```

**Output:**

<img width="1235" height="397" alt="image" src="https://github.com/user-attachments/assets/402c8fa4-9d16-47e4-830e-479246d205bc" />

**Question 5**

Write a SQL query to calculate total purchase amount of all orders. Return total purchase amount.

Sample table: orders

ord_no      purch_amt   ord_date    customer_id  salesman_id

----------  ----------  ----------  -----------  -----------

70001       150.5       2012-10-05  3005         5002

70009       270.65      2012-09-10  3001         5005

70002       65.26       2012-10-05  3002         5001

```sql

SELECT SUM(purch_amt) AS TOTAL
FROM orders;

```

**Output:**

<img width="1236" height="395" alt="image" src="https://github.com/user-attachments/assets/912bcb04-35fd-4b4d-b2dc-ec569ca63726" />

**Question 6**

Write a SQL query to find What is the age difference between the youngest and oldest employee in the company.

Table: employee

name        type
----------  ----------
id          INTEGER
name        TEXT
age         INTEGER
city        TEXT
income      INTEGER

```sql

SELECT (MAX(age) - MIN(age)) AS age_difference
FROM employee;

```

**Output:**

<img width="1227" height="395" alt="image" src="https://github.com/user-attachments/assets/5b35c41d-d852-49b9-abd7-78eb9019f148" />

**Question 7**

Write a SQL query to return the total number of rows in the 'customer' table where the city is not Noida.

Sample table: customer

```sql

SELECT COUNT(*) AS COUNT
FROM customer
WHERE city != 'Noida';

```

**Output:**

<img width="1237" height="396" alt="image" src="https://github.com/user-attachments/assets/4c025752-1d73-4492-b0f0-9dc01d757353" />

**Question 8**

Write the SQL query that accomplishes the selection of total number of products for each category from the "products" table, and includes only those products where the minimum category ID is less than 3.

Sample table: products

```sql

SELECT category_id, COUNT(*) AS "count(product_name)"
FROM products
GROUP BY category_id
HAVING category_id < 3;

```

**Output:**

<img width="1230" height="444" alt="image" src="https://github.com/user-attachments/assets/7fe73aa9-9d89-43ed-b28d-cc2dc6277922" />

**Question 9**

Write the SQL query that achieves the grouping of data by age, calculates the minimum income for each age group, and includes only those age groups where the minimum income is less than 400,000.

Sample table: employee

```sql

SELECT age, MIN(income)
FROM employee
GROUP BY age
HAVING MIN(income) < 400000;

```

**Output:**

<img width="1229" height="468" alt="image" src="https://github.com/user-attachments/assets/6409fee4-b90f-4208-9911-f97afb88801c" />

**Question 10**

Write an SQL query that groups the customer data into 5-year age intervals, calculates the minimum salary for each group, and excludes groups where the minimum salary is not less than 2000.

Table: customer1

```sql

SELECT (age/5) * 5 AS age_group, MIN(salary)
FROM customer1
GROUP BY age_group
HAVING MIN(SALARY) < 2000;

```

**Output:**

<img width="1233" height="422" alt="image" src="https://github.com/user-attachments/assets/78922429-1e01-4a0a-9333-41f775a3638f" />

## RESULT
Thus, the SQL queries to implement aggregate functions, GROUP BY, and HAVING clause have been executed successfully.
