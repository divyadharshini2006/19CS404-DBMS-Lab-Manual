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

**Output:**  
The program should display the employee details or an error message.

**PL/SQL CODE**
```
SET SERVEROUTPUT ON;

-- Step 1: Create the employees table
CREATE TABLE employees (
    emp_id NUMBER PRIMARY KEY,
    emp_name VARCHAR2(50),
    designation VARCHAR2(50)
);

-- Step 2: Insert sample data
INSERT INTO employees VALUES (1, 'Amit', 'Manager');
INSERT INTO employees VALUES (2, 'Divya', 'Developer');
INSERT INTO employees VALUES (3, 'Rahul', 'Analyst');
COMMIT;

-- Step 3: PL/SQL block using cursor
DECLARE
    CURSOR emp_cursor IS
        SELECT emp_name, designation FROM employees;

    v_name employees.emp_name%TYPE;
    v_designation employees.designation%TYPE;
    
    no_data EXCEPTION;
    v_count NUMBER;
BEGIN
    -- Check if the table has any records
    SELECT COUNT(*) INTO v_count FROM employees;
    IF v_count = 0 THEN
        RAISE no_data;
    END IF;

    OPEN emp_cursor;
    LOOP
        FETCH emp_cursor INTO v_name, v_designation;
        EXIT WHEN emp_cursor%NOTFOUND;
        DBMS_OUTPUT.PUT_LINE('Name: ' || v_name || ', Designation: ' || v_designation);
    END LOOP;
    CLOSE emp_cursor;

EXCEPTION
    WHEN no_data THEN
        DBMS_OUTPUT.PUT_LINE('No data found in employees table.');
    WHEN OTHERS THEN
        DBMS_OUTPUT.PUT_LINE('An unexpected error occurred: ' || SQLERRM);
END;
/
```
<img width="1174" height="604" alt="image" src="https://github.com/user-attachments/assets/5dd89c8a-4659-4ccb-b6a3-73948cb6d1f5" />

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

**Output:**  
The program should display the employee details within the specified salary range or an error message if no data is found.

**PL/SQL CODE**
```
SET SERVEROUTPUT ON;

-- Step 1: Create a fresh table (run this only once)
BEGIN
    EXECUTE IMMEDIATE 'DROP TABLE employees';
EXCEPTION
    WHEN OTHERS THEN
        NULL; -- ignore if table doesn't exist
END;
/

CREATE TABLE employees (
    emp_id NUMBER PRIMARY KEY,
    emp_name VARCHAR2(50),
    designation VARCHAR2(50),
    salary NUMBER
);

-- Step 2: Insert sample data
INSERT INTO employees VALUES (1, 'Amit', 'Manager', 80000);
INSERT INTO employees VALUES (2, 'Divya', 'Developer', 50000);
INSERT INTO employees VALUES (3, 'Rahul', 'Analyst', 60000);
COMMIT;

-- Step 3: PL/SQL block with parameterized cursor
DECLARE
    CURSOR emp_salary_cursor (min_sal NUMBER, max_sal NUMBER) IS
        SELECT emp_name, designation, salary
        FROM employees
        WHERE salary BETWEEN min_sal AND max_sal;

    v_count NUMBER := 0;
    no_data EXCEPTION;
BEGIN
    DBMS_OUTPUT.PUT_LINE('Employees with salary in the given range:');

    -- Use cursor with parameters (example: 40000 to 70000)
    FOR emp_rec IN emp_salary_cursor(40000, 70000) LOOP
        v_count := v_count + 1;
        DBMS_OUTPUT.PUT_LINE('Name: ' || emp_rec.emp_name ||
                             ', Designation: ' || emp_rec.designation ||
                             ', Salary: ' || emp_rec.salary);
    END LOOP;

    IF v_count = 0 THEN
        RAISE no_data;
    END IF;

EXCEPTION
    WHEN no_data THEN
        DBMS_OUTPUT.PUT_LINE('No employees found in the specified salary range.');
    WHEN OTHERS THEN
        DBMS_OUTPUT.PUT_LINE('An unexpected error occurred: ' || SQLERRM);
END;
/
```
<img width="1176" height="604" alt="image" src="https://github.com/user-attachments/assets/6c50016f-001f-45ba-8f3f-125737dbf158" />

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

**Output:**  
The program should display employee names with their department numbers or the appropriate error message if no data is found.

**PL/SQL CODE**
```
SET SERVEROUTPUT ON;

-- Step 1: Drop and recreate employees table (safe reset)
BEGIN
    EXECUTE IMMEDIATE 'DROP TABLE employees';
EXCEPTION
    WHEN OTHERS THEN
        NULL; -- Ignore if table doesn't exist
END;
/

-- Step 2: Create table with dept_no column
CREATE TABLE employees (
    emp_id NUMBER PRIMARY KEY,
    emp_name VARCHAR2(50),
    designation VARCHAR2(50),
    salary NUMBER,
    dept_no NUMBER
);

-- Step 3: Insert sample data
INSERT INTO employees VALUES (1, 'Amit', 'Manager', 80000, 10);
INSERT INTO employees VALUES (2, 'Divya', 'Developer', 50000, 20);
INSERT INTO employees VALUES (3, 'Rahul', 'Analyst', 60000, 30);
COMMIT;

-- Step 4: PL/SQL program using cursor FOR loop
DECLARE
    v_count NUMBER := 0;
    no_data EXCEPTION;
BEGIN
    DBMS_OUTPUT.PUT_LINE('Employee Details:');

    -- Cursor FOR loop automatically manages open/fetch/close
    FOR emp_rec IN (SELECT emp_name, dept_no FROM employees) LOOP
        v_count := v_count + 1;
        DBMS_OUTPUT.PUT_LINE('Name: ' || emp_rec.emp_name ||
                             ', Department No: ' || emp_rec.dept_no);
    END LOOP;

    -- Raise exception if no rows fetched
    IF v_count = 0 THEN
        RAISE no_data;
    END IF;

EXCEPTION
    WHEN no_data THEN
        DBMS_OUTPUT.PUT_LINE('No employees found in the database.');
    WHEN OTHERS THEN
        DBMS_OUTPUT.PUT_LINE('An unexpected error occurred: ' || SQLERRM);
END;
/
```
<img width="1180" height="634" alt="image" src="https://github.com/user-attachments/assets/b2666532-4764-4953-a110-010b352d3cd8" />

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

**Output:**  
The program should display employee records or the appropriate error message if no data is found.

**PL/SQL CODE**
```
SET SERVEROUTPUT ON;

-- Step 1: Drop and recreate the employees table (to avoid duplicate column errors)
BEGIN
    EXECUTE IMMEDIATE 'DROP TABLE employees';
EXCEPTION
    WHEN OTHERS THEN
        NULL; -- Ignore if the table doesn't exist
END;
/

-- Step 2: Create employees table
CREATE TABLE employees (
    emp_id NUMBER PRIMARY KEY,
    emp_name VARCHAR2(50),
    designation VARCHAR2(50),
    salary NUMBER
);

-- Step 3: Insert sample data
INSERT INTO employees VALUES (1, 'Amit', 'Manager', 80000);
INSERT INTO employees VALUES (2, 'Divya', 'Developer', 50000);
INSERT INTO employees VALUES (3, 'Rahul', 'Analyst', 60000);
COMMIT;

-- Step 4: PL/SQL block using cursor with %ROWTYPE
DECLARE
    CURSOR emp_cursor IS
        SELECT * FROM employees;

    emp_rec employees%ROWTYPE;
    v_count NUMBER := 0;
    no_data EXCEPTION;
BEGIN
    DBMS_OUTPUT.PUT_LINE('Employee Records:');

    OPEN emp_cursor;
    LOOP
        FETCH emp_cursor INTO emp_rec;
        EXIT WHEN emp_cursor%NOTFOUND;

        v_count := v_count + 1;
        DBMS_OUTPUT.PUT_LINE('Emp_ID: ' || emp_rec.emp_id ||
                             ', Name: ' || emp_rec.emp_name ||
                             ', Designation: ' || emp_rec.designation ||
                             ', Salary: ' || emp_rec.salary);
    END LOOP;
    CLOSE emp_cursor;

    -- Raise custom exception if no rows fetched
    IF v_count = 0 THEN
        RAISE no_data;
    END IF;

EXCEPTION
    WHEN no_data THEN
        DBMS_OUTPUT.PUT_LINE('No employees found in the database.');
    WHEN OTHERS THEN
        DBMS_OUTPUT.PUT_LINE('An unexpected error occurred: ' || SQLERRM);
END;
/
```
<img width="1174" height="606" alt="image" src="https://github.com/user-attachments/assets/52d54135-741e-481f-b125-26ce1c4b31e0" />

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

**Output:**  
The program should update employee salaries and display a message, or it should display an error message if no data is found.

**PL/SQL CODE**
```
SET SERVEROUTPUT ON;

-- Step 1: Drop and recreate the employees table (fresh start to avoid column conflicts)
BEGIN
    EXECUTE IMMEDIATE 'DROP TABLE employees';
EXCEPTION
    WHEN OTHERS THEN
        NULL; -- Ignore if table doesn't exist
END;
/

-- Step 2: Create employees table with dept_no and salary
CREATE TABLE employees (
    emp_id NUMBER PRIMARY KEY,
    emp_name VARCHAR2(50),
    designation VARCHAR2(50),
    dept_no NUMBER,
    salary NUMBER
);

-- Step 3: Insert sample data
INSERT INTO employees VALUES (1, 'Amit', 'Manager', 10, 80000);
INSERT INTO employees VALUES (2, 'Divya', 'Developer', 20, 50000);
INSERT INTO employees VALUES (3, 'Rahul', 'Analyst', 20, 60000);
INSERT INTO employees VALUES (4, 'Sneha', 'Tester', 30, 45000);
COMMIT;

-- Step 4: PL/SQL block using cursor FOR UPDATE
DECLARE
    CURSOR emp_cursor IS
        SELECT emp_id, emp_name, salary
        FROM employees
        WHERE dept_no = 20
        FOR UPDATE;

    v_emp emp_cursor%ROWTYPE;
    v_count NUMBER := 0;
    no_data EXCEPTION;
BEGIN
    DBMS_OUTPUT.PUT_LINE('Updating salaries for department 20...');

    OPEN emp_cursor;
    LOOP
        FETCH emp_cursor INTO v_emp;
        EXIT WHEN emp_cursor%NOTFOUND;

        v_count := v_count + 1;
        UPDATE employees
        SET salary = salary + 5000
        WHERE CURRENT OF emp_cursor;

        DBMS_OUTPUT.PUT_LINE('Updated Salary for ' || v_emp.emp_name || ' to ' || (v_emp.salary + 5000));
    END LOOP;
    CLOSE emp_cursor;

    IF v_count = 0 THEN
        RAISE no_data;
    END IF;

    COMMIT;
    DBMS_OUTPUT.PUT_LINE('Salary update completed successfully.');

EXCEPTION
    WHEN no_data THEN
        DBMS_OUTPUT.PUT_LINE('No employees found for the specified department.');
    WHEN OTHERS THEN
        DBMS_OUTPUT.PUT_LINE('An unexpected error occurred: ' || SQLERRM);
END;
/
```
<img width="1158" height="610" alt="image" src="https://github.com/user-attachments/assets/1c9ab972-4906-4d80-a8af-7502ae890a49" />

---

## RESULT
Thus, the program successfully executed and displayed employee details using a cursor. 

