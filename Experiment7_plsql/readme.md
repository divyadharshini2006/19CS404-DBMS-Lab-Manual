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

**PL/SQL CODE**
```
DECLARE
    num1 NUMBER := 45;
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
<img width="1170" height="546" alt="image" src="https://github.com/user-attachments/assets/88901b5d-30cc-4b62-910d-337102bec051" />

---

## 2. Write a PL/SQL program to Calculate Sum of First N Natural Numbers

### Steps:
- Declare a variable `n` and assign a value (e.g., 10).
- Initialize a `sum` variable to 0.
- Use a `WHILE` loop to iterate from 1 to `n`, adding each number to the sum.
- Display the result using `DBMS_OUTPUT.PUT_LINE`.

**Expected Output:**  
Sum of first 10 natural numbers is: 55

**PL/SQL CODE**
```
DECLARE
    n NUMBER := 10;
    i NUMBER := 1;
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
<img width="1184" height="602" alt="image" src="https://github.com/user-attachments/assets/9a0c0462-ebac-4e55-a96d-6f04d1b4892c" />

---

## 3. Write a PL/SQL program to generate Fibonacci series

### Steps:
- Declare the variable `n` to indicate how many terms to generate.
- Initialize the first two Fibonacci numbers (0 and 1).
- Use a loop to generate the next terms using the formula `c = a + b`.
- Print each term in the series.

**Expected Output:**  
n = 7  
Fibonacci sequence: 0, 1, 1, 2, 3, 5, 8

**PL/SQL CODE**
```
SET SERVEROUTPUT ON;
DECLARE
    n NUMBER := 7;
    a NUMBER := 0;
    b NUMBER := 1;
    c NUMBER;
    i NUMBER := 3;
BEGIN
    DBMS_OUTPUT.PUT_LINE('Fibonacci sequence:');
    DBMS_OUTPUT.PUT(a || ', ' || b);
    
    WHILE i <= n LOOP
        c := a + b;
        DBMS_OUTPUT.PUT(', ' || c);
        a := b;
        b := c;
        i := i + 1;
    END LOOP;
    
    DBMS_OUTPUT.NEW_LINE;
END;
/
```
<img width="589" height="305" alt="Screenshot 2025-11-10 at 1 36 48 PM" src="https://github.com/user-attachments/assets/4ac09d9f-ec64-4129-a1de-89f85227aefb" />

---

## 4. Write a PL/SQL Program to display the number in Reverse Order

### Steps:
- Declare a variable `n` and assign a value (e.g., 1535).
- Use a loop to extract each digit using modulo and reverse the number.
- Display the reversed number.

**Expected Output:**  
n = 1535  
Reversed number is 5351

**PL/SQL CODE**
```
SET SERVEROUTPUT ON;
DECLARE
    n NUMBER := 1535;
    rev NUMBER := 0;
    rem NUMBER;
    temp NUMBER;
BEGIN
    temp := n;
    WHILE temp > 0 LOOP
        rem := MOD(temp, 10);
        rev := (rev * 10) + rem;
        temp := FLOOR(temp / 10);
    END LOOP;
    DBMS_OUTPUT.PUT_LINE('Reversed number is ' || rev);
END;
/
```
 <img width="1184" height="628" alt="image" src="https://github.com/user-attachments/assets/6c1328ab-9e99-489e-89c7-e00ab36d6c59" />

---

## 5. Write a PL/SQL program to find the largest of three numbers

### Steps:
- Declare three numeric variables `a`, `b`, and `c`.
- Use nested `IF-ELSIF-ELSE` conditions to find the largest among the three.
- Display the largest number.

**Expected Output:**  
a = 10, b = 9, c = 15  
Largest of three number is 15

**PL/SQL CODE**
```
SET SERVEROUTPUT ON;
DECLARE
    a NUMBER := 10;
    b NUMBER := 9;
    c NUMBER := 15;
BEGIN
    IF (a > b) AND (a > c) THEN
        DBMS_OUTPUT.PUT_LINE('Largest of three numbers is ' || a);
    ELSIF (b > c) THEN
        DBMS_OUTPUT.PUT_LINE('Largest of three numbers is ' || b);
    ELSE
        DBMS_OUTPUT.PUT_LINE('Largest of three numbers is ' || c);
    END IF;
END;
/
```
<img width="1178" height="640" alt="image" src="https://github.com/user-attachments/assets/3db26688-c29f-4b1c-83c8-65c6181dabb7" />

## RESULT
Thus, the PL/SQL programs using variables, conditionals, and loops were executed successfully.

