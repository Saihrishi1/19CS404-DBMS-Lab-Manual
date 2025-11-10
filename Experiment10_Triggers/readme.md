# Experiment 10: PL/SQL – Triggers

## AIM
To write and execute PL/SQL trigger programs for automating actions in response to specific table events like INSERT, UPDATE, or DELETE.

---

## THEORY

A **trigger** is a stored PL/SQL block that is automatically executed or fired when a specified event occurs on a table or view. Triggers can be used for enforcing business rules, auditing changes, or automatic updates.

### Types of Triggers:
- **Before Trigger**: Executes before the operation (INSERT, UPDATE, DELETE).
- **After Trigger**: Executes after the operation.
- **Row-level Trigger**: Executes for each affected row.
- **Statement-level Trigger**: Executes once for the triggering statement.

**Basic Syntax:**
```sql
CREATE OR REPLACE TRIGGER trigger_name
BEFORE|AFTER INSERT|UPDATE|DELETE ON table_name
[FOR EACH ROW]
BEGIN
   -- trigger logic
END;
```

## 1. Write a trigger to log every insertion into a table.
**Steps:**
- Create two tables: `employees` (for storing data) and `employee_log` (for logging the inserts).
- Write an **AFTER INSERT** trigger on the `employees` table to log the new data into the `employee_log` table.

### Code :

```pl/sql

CREATE TABLE employees (
  emp_id NUMBER,
  emp_name VARCHAR2(50),
  salary NUMBER
);

CREATE TABLE employee_log (
  log_id NUMBER GENERATED ALWAYS AS IDENTITY,
  emp_id NUMBER,
  emp_name VARCHAR2(50),
  salary NUMBER,
  log_date DATE
);

CREATE OR REPLACE TRIGGER trg_employee_insert
AFTER INSERT ON employees
FOR EACH ROW
BEGIN
  INSERT INTO employee_log (emp_id, emp_name, salary, log_date)
  VALUES (:NEW.emp_id, :NEW.emp_name, :NEW.salary, SYSDATE);
END;
/
INSERT INTO employees (emp_id, emp_name, salary) VALUES (1, 'John', 5000);
/

```

**Expected Output:**
- A new entry is added to the `employee_log` table each time a new record is inserted into the `employees` table.

---

## 2. Write a trigger to prevent deletion of records from a sensitive table.
**Steps:**
- Write a **BEFORE DELETE** trigger on the `sensitive_data` table.
- Use `RAISE_APPLICATION_ERROR` to prevent deletion and issue a custom error message.

### Code :

```pl/sql

CREATE TABLE sensitive_data (
  data_id NUMBER,
  info VARCHAR2(100)
);

CREATE OR REPLACE TRIGGER trg_prevent_delete
BEFORE DELETE ON sensitive_data
FOR EACH ROW
BEGIN
  RAISE_APPLICATION_ERROR(-20001, 'Deletion not allowed on this table.');
END;
/
DELETE FROM sensitive_data WHERE data_id = 1;
/

```

**Expected Output:**
- If an attempt is made to delete a record from `sensitive_data`, an error message is raised, e.g., `ERROR: Deletion not allowed on this table.`

---

## 3. Write a trigger to automatically update a `last_modified` timestamp.
**Steps:**
- Add a `last_modified` column to the `products` table.
- Write a **BEFORE UPDATE** trigger on the `products` table to set the `last_modified` column to the current timestamp whenever an update occurs.

### Code :

```pl/sql

CREATE TABLE products (
  product_id NUMBER,
  product_name VARCHAR2(50),
  price NUMBER,
  last_modified DATE
);

CREATE OR REPLACE TRIGGER trg_update_last_modified
BEFORE UPDATE ON products
FOR EACH ROW
BEGIN
  :NEW.last_modified := SYSDATE;
END;
/
UPDATE products SET price = 200 WHERE product_id = 1;
/

```

**Expected Output:**
- The `last_modified` column in the `products` table is updated automatically to the current date and time when any record is updated.

---

## 4. Write a trigger to keep track of the number of updates made to a table.
**Steps:**
- Create an `audit_log` table with a counter column.
- Write an **AFTER UPDATE** trigger on the `customer_orders` table to increment the counter in the `audit_log` table every time a record is updated.

### Code :

```pl/sql

CREATE TABLE customer_orders (
  order_id NUMBER,
  customer_name VARCHAR2(50),
  order_total NUMBER
);

CREATE TABLE audit_log (
  id NUMBER GENERATED ALWAYS AS IDENTITY,
  update_count NUMBER
);

INSERT INTO audit_log (update_count) VALUES (0);

CREATE OR REPLACE TRIGGER trg_count_updates
AFTER UPDATE ON customer_orders
FOR EACH ROW
BEGIN
  UPDATE audit_log SET update_count = update_count + 1 WHERE id = 1;
END;
/
UPDATE customer_orders SET order_total = 500 WHERE order_id = 1;
/

```

**Expected Output:**
- The `audit_log` table will maintain a count of how many updates have been made to the `customer_orders` table.

---

## 5. Write a trigger that checks a condition before allowing insertion into a table.
**Steps:**
- Write a **BEFORE INSERT** trigger on the `employees` table to check if the inserted salary meets a specific condition (e.g., salary must be greater than 3000).
- If the condition is not met, raise an error to prevent the insert.


### Code :

```pl/sql

CREATE OR REPLACE TRIGGER trg_check_salary
BEFORE INSERT ON employees
FOR EACH ROW
BEGIN
  IF :NEW.salary < 3000 THEN
    RAISE_APPLICATION_ERROR(-20002, 'Salary below minimum threshold.');
  END IF;
END;
/
INSERT INTO employees (emp_id, emp_name, salary) VALUES (2, 'Jane', 2500);
/

```

**Expected Output:**
- If the inserted salary in the `employees` table is below the condition (e.g., salary < 3000), the insert operation is blocked, and an error message is raised, such as: `ERROR: Salary below minimum threshold.`

## RESULT
Thus, the PL/SQL trigger programs were written and executed successfully.

