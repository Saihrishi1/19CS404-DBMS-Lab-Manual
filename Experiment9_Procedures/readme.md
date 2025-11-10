# Experiment 9: PL/SQL – Procedures and Functions

## AIM
To understand and implement procedures and functions in PL/SQL for performing various operations such as calculations, decision-making, and looping.

---

## THEORY

PL/SQL (Procedural Language/SQL) extends SQL by adding procedural constructs like variables, conditions, loops, procedures, and functions. Procedures and functions are subprograms that help modularize the code and improve reusability.

### **Procedure**
A PL/SQL **procedure** is a subprogram that performs a specific action. It does not return a value directly but can return values using `OUT` parameters.

**Syntax:**
```sql
CREATE OR REPLACE PROCEDURE procedure_name (parameters)
IS
BEGIN
   -- statements
END;
```

To call the procedure

```sql
EXEC procedure_name(arguments);
```

### **Function**
A PL/SQL **function** is a subprogram that returns a single value using the RETURN keyword.

```sql
CREATE OR REPLACE FUNCTION function_name (parameters)
RETURN datatype
IS
BEGIN
   -- statements
   RETURN value;
END;
```

To call the function:

```sql
SELECT function_name(arguments) FROM DUAL;
```

Key Differences:

-A procedure does not return a value, whereas a function must return a value.
-Functions can be called from SQL queries, procedures cannot (in most cases).

## 1. Write a PL/SQL Procedure to Find the Square of a Number

### Steps:
- Create a procedure named `find_square`.
- Declare a parameter to accept a number.
- Inside the procedure, compute the square of the input number.
- Use `DBMS_OUTPUT.PUT_LINE` to display the result.
- Call the procedure with a number as input.

**Expected Output:**  
Square of 6 is 36

### Code :

```pl/sql

CREATE OR REPLACE PROCEDURE find_square(n IN NUMBER) IS
sq NUMBER;
BEGIN
  sq := n * n;
  DBMS_OUTPUT.PUT_LINE('Square of ' || n || ' is ' || sq);
END;
/
BEGIN
  find_square(6);
END;
/

```

### Output :

<img width="1003" height="322" alt="image" src="https://github.com/user-attachments/assets/e6ca581c-d41c-4840-a9da-9ec376d23c4c" />


---

## 2. Write a PL/SQL Function to Return the Factorial of a Number

### Steps:
- Create a function named `get_factorial`.
- Declare a parameter to accept a number.
- Use a loop to calculate the factorial.
- Return the result using the `RETURN` statement.
- Call the function using a `SELECT` statement or in an anonymous block.

**Expected Output:**  
Factorial of 5 is 120

### Code :

```pl/sql

CREATE OR REPLACE FUNCTION get_factorial(n IN NUMBER) RETURN NUMBER IS
fact NUMBER := 1;
i NUMBER;
BEGIN
  FOR i IN 1..n LOOP
    fact := fact * i;
  END LOOP;
  RETURN fact;
END;
/
DECLARE
  res NUMBER;
BEGIN
  res := get_factorial(5);
  DBMS_OUTPUT.PUT_LINE('Factorial of 5 is ' || res);
END;
/

```

### Output :

<img width="999" height="291" alt="image" src="https://github.com/user-attachments/assets/b0e25081-c7d9-42a3-a543-b567e7f3e017" />

---

## 3. Write a PL/SQL Procedure to Check Whether a Number is Even or Odd

### Steps:
- Create a procedure named `check_even_odd`.
- Accept an input parameter.
- Use the `MOD` function to check if the number is divisible by 2.
- Display whether it is Even or Odd using `DBMS_OUTPUT.PUT_LINE`.

**Expected Output:**  
12 is Even

### Code :

```pl/sql

CREATE OR REPLACE PROCEDURE check_even_odd(n IN NUMBER) IS
BEGIN
  IF MOD(n, 2) = 0 THEN
    DBMS_OUTPUT.PUT_LINE(n || ' is Even');
  ELSE
    DBMS_OUTPUT.PUT_LINE(n || ' is Odd');
  END IF;
END;
/
BEGIN
  check_even_odd(12);
END;
/

```

### Output :

<img width="997" height="310" alt="image" src="https://github.com/user-attachments/assets/9cd7cc68-de35-40e8-9df0-001145a5b3b9" />

---

## 4. Write a PL/SQL Function to Return the Reverse of a Number

### Steps:
- Create a function named `reverse_number`.
- Accept an input number as parameter.
- Use a loop to reverse the digits of the number.
- Return the reversed number.
- Call the function and display the output.

**Expected Output:**  
Reversed number of 1234 is 4321

### Code :

```pl/sql

CREATE OR REPLACE FUNCTION reverse_number(n IN NUMBER) RETURN NUMBER IS
rev NUMBER := 0;
num NUMBER := n;
digit NUMBER;
BEGIN
  WHILE num > 0 LOOP
    digit := MOD(num, 10);
    rev := rev * 10 + digit;
    num := TRUNC(num / 10);
  END LOOP;
  RETURN rev;
END;
/
DECLARE
  res NUMBER;
BEGIN
  res := reverse_number(1234);
  DBMS_OUTPUT.PUT_LINE('Reversed number of 1234 is ' || res);
END

```

### Output :

<img width="998" height="282" alt="image" src="https://github.com/user-attachments/assets/775c0020-74db-4c4f-84ec-7b1662ea8364" />

---

## 5. Write a PL/SQL Procedure to Display the Multiplication Table of a Number

### Steps:
- Create a procedure named `print_table`.
- Accept an input number.
- Use a loop from 1 to 10 to multiply the input number.
- Display the multiplication results using `DBMS_OUTPUT.PUT_LINE`.

**Expected Output:**  
Multiplication table of 5:  
5 x 1 = 5  
5 x 2 = 10  
5 x 3 = 15  
...  
5 x 10 = 50

### Code :

```pl/sql

CREATE OR REPLACE PROCEDURE print_table(n IN NUMBER) IS
i NUMBER;
BEGIN
  DBMS_OUTPUT.PUT_LINE('Multiplication table of ' || n || ':');
  FOR i IN 1..10 LOOP
    DBMS_OUTPUT.PUT_LINE(n || ' x ' || i || ' = ' || (n * i));
  END LOOP;
END;
/
BEGIN
  print_table(5);
END;
/

```

### Output :

<img width="1004" height="436" alt="image" src="https://github.com/user-attachments/assets/6a363249-d6c8-42bd-8f41-44b438618890" />

## RESULT
Thus, the PL/SQL programs using procedures and functions were written, compiled, and executed successfully.
