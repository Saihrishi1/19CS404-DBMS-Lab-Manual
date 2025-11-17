# Experiment 8: PL/SQL Cursor Programs

## AIM
To write and execute PL/SQL programs using cursors and exception handling to manage runtime errors effectively and display appropriate messages.

## THEORY

In PL/SQL, cursors are used to handle query result sets row-by-row. 

There are two types of cursors:

- Implicit Cursors: Automatically created by PL/SQL for single-row queries.
- Explicit Cursors: Declared and controlled by the programmer for multi-row queries.

Types of Explicit Cursors:

1. Simple Cursor: Basic cursor to iterate over multiple rows.

2. Parameterized Cursor: Accepts parameters to filter the result dynamically.

3. Cursor FOR Loop: Simplifies cursor operations (open, fetch, close).

4. %ROWTYPE Cursor: Fetches entire row into a record using %ROWTYPE.

5. Cursor with FOR UPDATE: Used for row-level locking and updating the rows while looping.

**Syntax:**
```sql
DECLARE 
   <declarations section> 
BEGIN 
   <executable command(s)>
EXCEPTION 
   <exception handling> 
END;
```

### Basic Components of PL/SQL Block:

- DECLARE: Section to declare variables and constants.
- BEGIN: The execution section that contains PL/SQL statements.
- EXCEPTION: Handles errors or exceptions that occur in the program.
- END: Marks the end of the PL/SQL block.

**Exception Handling**

PL/SQL provides a robust mechanism to handle runtime errors using exception handling blocks. When an error occurs during execution, control is passed to the EXCEPTION section, where specific or general errors can be handled gracefully.

### Components of Exception Handling:
- Predefined Exceptions: Automatically raised by PL/SQL for common errors (e.g., NO_DATA_FOUND, TOO_MANY_ROWS, ZERO_DIVIDE).
- User-defined Exceptions: Declared explicitly in the declaration section using the EXCEPTION keyword.
- WHEN OTHERS: A generic handler for all exceptions not handled explicitly.

```sql
BEGIN
   -- Statements
EXCEPTION
   WHEN exception_name THEN
      -- Handling code
   WHEN OTHERS THEN
      -- Handling for unknown errors
END;
```

### **Question 1: Simple Cursor with Exception Handling**

**Write a PL/SQL program using a simple cursor to fetch employee names and designations from the `employees` table. Implement exception handling for the following cases:**

1. **NO_DATA_FOUND**: When no rows are fetched.
2. **OTHERS**: Any other unexpected errors during execution.

**Steps:**

- Create an `employees` table with fields `emp_id`, `emp_name`, and `designation`.
- Insert some sample data into the table.
- Use a simple cursor to fetch and display employee names and designations.
- Implement exception handling to catch the relevant exceptions and display appropriate messages.

## Code :

```sql

DECLARE
    CURSOR emp_cur IS
        SELECT emp_id, emp_name FROM employees;

    v_id employees.emp_id%TYPE;
    v_name employees.emp_name%TYPE;

    no_data EXCEPTION;
    v_count NUMBER := 0;
BEGIN
    OPEN emp_cur;
    LOOP
        FETCH emp_cur INTO v_id, v_name;
        EXIT WHEN emp_cur%NOTFOUND;

        v_count := v_count + 1;
        DBMS_OUTPUT.PUT_LINE('ID: ' || v_id || '  Name: ' || v_name);
    END LOOP;
    CLOSE emp_cur;

    IF v_count = 0 THEN
        RAISE no_data;
    END IF;

EXCEPTION
    WHEN no_data THEN
        DBMS_OUTPUT.PUT_LINE('No employee data found.');
    WHEN OTHERS THEN
        DBMS_OUTPUT.PUT_LINE('Error occurred: ' || SQLERRM);
END;
/


```

**Output:**  

<img width="997" height="284" alt="image" src="https://github.com/user-attachments/assets/c4d7d560-41bc-4c24-9430-b64ae34c7a58" />


---

### **Question 2: Parameterized Cursor with Exception Handling**

**Write a PL/SQL program using a parameterized cursor to retrieve and display employees with a salary in a given range. Implement exception handling for the following errors:**

1. **NO_DATA_FOUND**: When no employees meet the salary criteria.
2. **OTHERS**: For any unexpected errors during the execution.

**Steps:**

- Modify the `employees` table by adding a `salary` column.
- Insert sample salary values for the employees.
- Use a parameterized cursor to accept a salary range as input and fetch employees within that range.
- Implement exception handling to catch and display relevant error messages.


```sql

DECLARE
    CURSOR sal_cur(min_sal NUMBER, max_sal NUMBER) IS
        SELECT emp_name, salary FROM employees
        WHERE salary BETWEEN min_sal AND max_sal;
    v_name employees.emp_name%TYPE;
    v_sal employees.salary%TYPE;
    no_data EXCEPTION;
    v_count NUMBER := 0;
BEGIN
    OPEN sal_cur(20000, 50000);
    LOOP
        FETCH sal_cur INTO v_name, v_sal;
        EXIT WHEN sal_cur%NOTFOUND;
        v_count := v_count + 1;
        DBMS_OUTPUT.PUT_LINE('Name: ' || v_name || '  Salary: ' || v_sal);
    END LOOP;
    CLOSE sal_cur;

    IF v_count = 0 THEN
        RAISE no_data;
    END IF;

EXCEPTION
    WHEN no_data THEN
        DBMS_OUTPUT.PUT_LINE('No employees found in the given salary range.');
    WHEN OTHERS THEN
        DBMS_OUTPUT.PUT_LINE('Error: ' || SQLERRM);
END;
/


```

**Output:**  

<img width="1001" height="326" alt="image" src="https://github.com/user-attachments/assets/de096661-5ab7-4aab-8dcb-ceb158f390e0" />


---

### **Question 3: Cursor FOR Loop with Exception Handling**

**Write a PL/SQL program using a cursor FOR loop to retrieve and display all employee names and their department numbers from the `employees` table. Implement exception handling for the following cases:**

1. **NO_DATA_FOUND**: If no employees are found in the database.
2. **OTHERS**: For any other unexpected errors.

**Steps:**

- Modify the `employees` table by adding a `dept_no` column.
- Insert sample department numbers for employees.
- Use a cursor FOR loop to fetch and display employee names along with their department numbers.
- Implement exception handling to catch the relevant exceptions.


```sql

DECLARE
    no_data EXCEPTION;
    v_count NUMBER := 0;
BEGIN
    FOR rec IN (SELECT emp_id, emp_name FROM employees) LOOP
        v_count := v_count + 1;
        DBMS_OUTPUT.PUT_LINE('ID: ' || rec.emp_id || '  Name: ' || rec.emp_name);
    END LOOP;

    IF v_count = 0 THEN
        RAISE no_data;
    END IF;

EXCEPTION
    WHEN no_data THEN
        DBMS_OUTPUT.PUT_LINE('No employee data found.');
    WHEN OTHERS THEN
        DBMS_OUTPUT.PUT_LINE('Error: ' || SQLERRM);
END;
/

```

**Output:**  

<img width="996" height="291" alt="image" src="https://github.com/user-attachments/assets/59913916-34f5-4591-afeb-c7703f6d67f6" />


---

### **Question 4: Cursor with `%ROWTYPE` and Exception Handling**

**Write a PL/SQL program that uses a cursor with `%ROWTYPE` to fetch and display complete employee records (emp_id, emp_name, designation, salary). Implement exception handling for the following errors:**

1. **NO_DATA_FOUND**: When no employees are found in the database.
2. **OTHERS**: For any other errors that occur.

**Steps:**

- Modify the `employees` table by adding `emp_id`, `emp_name`, `designation`, and `salary` fields.
- Insert sample data into the `employees` table.
- Declare a cursor using `%ROWTYPE` to fetch complete rows from the `employees` table.
- Implement exception handling to catch the relevant exceptions and display appropriate messages.


```sql

DECLARE
    CURSOR emp_cur IS
        SELECT emp_id, emp_name FROM employees;

    emp_rec emp_cur%ROWTYPE;

    no_data EXCEPTION;
    v_count NUMBER := 0;
BEGIN
    OPEN emp_cur;
    LOOP
        FETCH emp_cur INTO emp_rec;
        EXIT WHEN emp_cur%NOTFOUND;

        v_count := v_count + 1;
        DBMS_OUTPUT.PUT_LINE(
            'ID: ' || emp_rec.emp_id ||
            '  Name: ' || emp_rec.emp_name
        );
    END LOOP;
    CLOSE emp_cur;

    IF v_count = 0 THEN
        RAISE no_data;
    END IF;

EXCEPTION
    WHEN no_data THEN
        DBMS_OUTPUT.PUT_LINE('No employee records found.');
    WHEN OTHERS THEN
        DBMS_OUTPUT.PUT_LINE('Error: ' || SQLERRM);
END;
/


```

**Output:**  

<img width="1000" height="327" alt="image" src="https://github.com/user-attachments/assets/0a7c7bbe-3226-44d6-96c1-915e2e697f81" />

---

### **Question 5: Cursor with FOR UPDATE Clause and Exception Handling**

**Write a PL/SQL program using a cursor with the `FOR UPDATE` clause to update the salary of employees in a specific department. Implement exception handling for the following cases:**

1. **NO_DATA_FOUND**: If no rows are affected by the update.
2. **OTHERS**: For any unexpected errors during execution.

**Steps:**

- Modify the `employees` table to include a `dept_no` and `salary` field.
- Insert sample data into the `employees` table with different department numbers.
- Use a cursor with the `FOR UPDATE` clause to lock the rows of employees in a specific department and update their salary.
- Implement exception handling to handle `NO_DATA_FOUND` or other errors that may occur.


```sql

DECLARE
    CURSOR emp_cur IS
        SELECT emp_id, salary
        FROM employees
        FOR UPDATE;

    v_id   employees.emp_id%TYPE;
    v_sal  employees.salary%TYPE;

    no_data EXCEPTION;
    v_count NUMBER := 0;
BEGIN
    OPEN emp_cur;
    LOOP
        FETCH emp_cur INTO v_id, v_sal;
        EXIT WHEN emp_cur%NOTFOUND;

        v_count := v_count + 1;

        UPDATE employees
        SET salary = v_sal + 2000
        WHERE CURRENT OF emp_cur;
    END LOOP;
    CLOSE emp_cur;

    IF v_count = 0 THEN
        RAISE no_data;
    END IF;

    DBMS_OUTPUT.PUT_LINE('Salary updated successfully.');

EXCEPTION
    WHEN no_data THEN
        DBMS_OUTPUT.PUT_LINE('No rows found for salary update.');
    WHEN OTHERS THEN
        DBMS_OUTPUT.PUT_LINE('Error: ' || SQLERRM);
END;
/


```

**Output:**  

<img width="999" height="282" alt="image" src="https://github.com/user-attachments/assets/81b4e829-109c-4076-a6c8-e73ee9a20b77" />

---

## RESULT
Thus, the program successfully executed and displayed employee details using a cursor. 

