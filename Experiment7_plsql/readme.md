# Experiment 7: PL/SQL – Variables, Control Structures and Loops

## AIM
To write and execute simple PL/SQL programs using variables, loops, and conditional statements.


## THEORY

PL/SQL, which stands for Procedural Language extensions to the Structured Query Language (SQL). It is a combination of SQL along with the procedural features of programming languages.

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

# PL/SQL Programs – Steps and Expected Output

## 1. Write a PL/SQL program to find the Greatest of Two Numbers

### Steps:
- Declare two numeric variables and initialize them.
- Use an `IF` statement to compare the values.
- Display the greater number using `DBMS_OUTPUT.PUT_LINE`.

**Expected Output:**  
Greater number is: 80

### Code:
```pl/sql

DECLARE
    num1 NUMBER := 50;
    num2 NUMBER := 80;
BEGIN
    IF num1 > num2 THEN
        DBMS_OUTPUT.PUT_LINE('Greater number is: ' || num1);
    ELSE
        DBMS_OUTPUT.PUT_LINE('Greater number is: ' || num2);
    END IF;
END;
/


```
### Output:

<img width="1014" height="296" alt="image" src="https://github.com/user-attachments/assets/19f330c8-57a2-4a73-bc85-314e6cbd5ebc" />


## 2. Write a PL/SQL program to Calculate Sum of First N Natural Numbers

### Steps:
- Declare a variable `n` and assign a value (e.g., 10).
- Initialize a `sum` variable to 0.
- Use a `WHILE` loop to iterate from 1 to `n`, adding each number to the sum.
- Display the result using `DBMS_OUTPUT.PUT_LINE`.

**Expected Output:**  
Sum of first 10 natural numbers is: 55

### Code:
```pl/sql

DECLARE
    n   NUMBER := 10;   
    i   NUMBER := 1;
    sum NUMBER := 0;
BEGIN
    WHILE i <= n LOOP
        sum := sum + i;
        i := i + 1;
    END LOOP;

    DBMS_OUTPUT.PUT_LINE('Sum of first ' || n || ' natural numbers is: ' || sum);
END;
/


```
### Output:

<img width="1014" height="329" alt="image" src="https://github.com/user-attachments/assets/6c1ef488-f3a4-480d-959c-fef6d8247ea6" />


## 3. Write a PL/SQL program to generate Fibonacci series

### Steps:
- Declare the variable `n` to indicate how many terms to generate.
- Initialize the first two Fibonacci numbers (0 and 1).
- Use a loop to generate the next terms using the formula `c = a + b`.
- Print each term in the series.

**Expected Output:**  
n = 7  
Fibonacci sequence: 0, 1, 1, 2, 3, 5, 8

### Code:
```pl/sql

DECLARE
    n   NUMBER := 7;
    a   NUMBER := 0;  
    b   NUMBER := 1;
    c   NUMBER;
    i   NUMBER := 3;

BEGIN
    DBMS_OUTPUT.PUT('Fibonacci Series : '|| a || ',' || b );
    WHILE i <= n LOOP
        c := a+b;
        DBMS_OUTPUT.PUT(', '||c);
        a := b;
        b := c;
        i := i + 1;
    END LOOP;

    DBMS_OUTPUT.NEW_LINE;
END;
/

```
### Output:

<img width="1014" height="287" alt="image" src="https://github.com/user-attachments/assets/f59ac90d-444c-44f2-8785-0062e6075be6" />


## 4. Write a PL/SQL Program to display the number in Reverse Order

### Steps:
- Declare a variable `n` and assign a value (e.g., 1535).
- Use a loop to extract each digit using modulo and reverse the number.
- Display the reversed number.

**Expected Output:**  
n = 1535  
Reversed number is 5351

### Code:
```pl/sql

DECLARE
    n        NUMBER := 1535;  ]
    rem      NUMBER;
    rev      NUMBER := 0;
    temp     NUMBER;
BEGIN
    temp := n;  
    
    WHILE n > 0 LOOP
        rem := MOD(n, 10);          
        rev := (rev * 10) + rem;    
        n := TRUNC(n / 10);         
    END LOOP;
    
    DBMS_OUTPUT.PUT_LINE('n = ' || temp);
    DBMS_OUTPUT.PUT_LINE('Reversed number is ' || rev);
END;
/

```
### Output:

<img width="1009" height="284" alt="image" src="https://github.com/user-attachments/assets/ceea0340-db90-4811-8585-f315b06868e5" />


## 5. Write a PL/SQL program to find the largest of three numbers

### Steps:
- Declare three numeric variables `a`, `b`, and `c`.
- Use nested `IF-ELSIF-ELSE` conditions to find the largest among the three.
- Display the largest number.

**Expected Output:**  
a = 10, b = 9, c = 15  
Largest of three number is 15

### Code:
```pl/sql

DECLARE
    a NUMBER := 10;
    b NUMBER := 9;
    c NUMBER := 15;
    largest NUMBER;
BEGIN
    IF (a > b) AND (a > c) THEN
        largest := a;
    ELSIF (b > a) AND (b > c) THEN
        largest := b;
    ELSE
        largest := c;
    END IF;
    
    DBMS_OUTPUT.PUT_LINE('a = ' || a || ', b = ' || b || ', c = ' || c);
    DBMS_OUTPUT.PUT_LINE('Largest of three numbers is ' || largest);
END;
/


```
### Output:

<img width="1008" height="270" alt="image" src="https://github.com/user-attachments/assets/596cb2ff-8cea-4033-8352-8eefc20ddde6" />

## RESULT
Thus, the PL/SQL programs using variables, conditionals, and loops were executed successfully.

