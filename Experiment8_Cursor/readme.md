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
```
*Syntax:*
sql
DECLARE 
   <declarations section> 
BEGIN 
   <executable command(s)>
EXCEPTION 
   <exception handling> 
END;
```

### Basic Components of PL/SQL Block:
```
- DECLARE: Section to declare variables and constants.
- BEGIN: The execution section that contains PL/SQL statements.
- EXCEPTION: Handles errors or exceptions that occur in the program.
- END: Marks the end of the PL/SQL block.
```
*Exception Handling*

PL/SQL provides a robust mechanism to handle runtime errors using exception handling blocks. When an error occurs during execution, control is passed to the EXCEPTION section, where specific or general errors can be handled gracefully.

### Components of Exception Handling:
- Predefined Exceptions: Automatically raised by PL/SQL for common errors (e.g., NO_DATA_FOUND, TOO_MANY_ROWS, ZERO_DIVIDE).
- User-defined Exceptions: Declared explicitly in the declaration section using the EXCEPTION keyword.
- WHEN OTHERS: A generic handler for all exceptions not handled explicitly.
```
sql
BEGIN
   -- Statements
EXCEPTION
   WHEN exception_name THEN
      -- Handling code
   WHEN OTHERS THEN
      -- Handling for unknown errors
END;

```
### *Question 1: Simple Cursor with Exception Handling*

**Write a PL/SQL program using a simple cursor to fetch employee names and designations from the employees table. Implement exception handling for the following cases:**
```
1. *NO_DATA_FOUND*: When no rows are fetched.
2. *OTHERS*: Any other unexpected errors during execution.

*Steps:*

- Create an employees table with fields emp_id, emp_name, and designation.
- Insert some sample data into the table.
- Use a simple cursor to fetch and display employee names and designations.
- Implement exception handling to catch the relevant exceptions and display appropriate messages.

*Program:*
sql
SET SERVEROUTPUT ON;

DECLARE
    CURSOR emp_cursor IS
        SELECT emp_name, designation FROM employees;

    v_name employees.emp_name%TYPE;
    v_desig employees.designation%TYPE;

    no_data BOOLEAN := TRUE;
BEGIN
    OPEN emp_cursor;
    LOOP
        FETCH emp_cursor INTO v_name, v_desig;
        EXIT WHEN emp_cursor%NOTFOUND;

        DBMS_OUTPUT.PUT_LINE('Name: ' || v_name || ', Designation: ' || v_desig);
        no_data := FALSE;
    END LOOP;
    CLOSE emp_cursor;

    IF no_data THEN
        RAISE NO_DATA_FOUND;
    END IF;

EXCEPTION
    WHEN NO_DATA_FOUND THEN
        DBMS_OUTPUT.PUT_LINE('No employee records found.');
    WHEN OTHERS THEN
        DBMS_OUTPUT.PUT_LINE('Unexpected error: ' || SQLERRM);
END;
```
*Output:*  
![image](https://github.com/user-attachments/assets/48f3a61e-9ca4-439e-9818-d640fcb5484e)

---

### *Question 2: Parameterized Cursor with Exception Handling*
```
*Write a PL/SQL program using a parameterized cursor to retrieve and display employees with a salary in a given range. Implement exception handling for the following errors:*

1. *NO_DATA_FOUND*: When no employees meet the salary criteria.
2. *OTHERS*: For any unexpected errors during the execution.

*Steps:*

- Modify the employees table by adding a salary column.
- Insert sample salary values for the employees.
- Use a parameterized cursor to accept a salary range as input and fetch employees within that range.
- Implement exception handling to catch and display relevant error messages.

*Program:*
sql
SET SERVEROUTPUT ON;

DECLARE
    CURSOR emp_cursor(min_sal NUMBER, max_sal NUMBER) IS
        SELECT emp_name, salary FROM employees
        WHERE salary BETWEEN min_sal AND max_sal;

    v_name employees.emp_name%TYPE;
    v_salary employees.salary%TYPE;

    v_min NUMBER := 50000;
    v_max NUMBER := 70000;

    no_data BOOLEAN := TRUE;
BEGIN
    OPEN emp_cursor(v_min, v_max);
    LOOP
        FETCH emp_cursor INTO v_name, v_salary;
        EXIT WHEN emp_cursor%NOTFOUND;

        DBMS_OUTPUT.PUT_LINE('Name: ' || v_name || ', Salary: ' || v_salary);
        no_data := FALSE;
    END LOOP;
    CLOSE emp_cursor;

    IF no_data THEN
        RAISE NO_DATA_FOUND;
    END IF;

EXCEPTION
    WHEN NO_DATA_FOUND THEN
        DBMS_OUTPUT.PUT_LINE('No employees found in the given salary range.');
    WHEN OTHERS THEN
        DBMS_OUTPUT.PUT_LINE('Unexpected error: ' || SQLERRM);
END;
```

*Output:*  
![image](https://github.com/user-attachments/assets/ecbc9b27-679f-49ae-b57d-1228b04597cb)

---

### *Question 3: Cursor FOR Loop with Exception Handling*

**Write a PL/SQL program using a cursor FOR loop to retrieve and display all employee names and their department numbers from the employees table. Implement exception handling for the following cases:**
```
1. *NO_DATA_FOUND*: If no employees are found in the database.
2. *OTHERS*: For any other unexpected errors.

*Steps:*

- Modify the employees table by adding a dept_no column.
- Insert sample department numbers for employees.
- Use a cursor FOR loop to fetch and display employee names along with their department numbers.
- Implement exception handling to catch the relevant exceptions.
*Program:*
sql
SET SERVEROUTPUT ON;

DECLARE
    no_data BOOLEAN := TRUE;
BEGIN
    FOR emp_rec IN (SELECT emp_name, dept_no FROM employees) LOOP
        DBMS_OUTPUT.PUT_LINE('Employee: ' || emp_rec.emp_name || ', Dept No: ' || emp_rec.dept_no);
        no_data := FALSE;
    END LOOP;

    IF no_data THEN
        RAISE NO_DATA_FOUND;
    END IF;

EXCEPTION
    WHEN NO_DATA_FOUND THEN
        DBMS_OUTPUT.PUT_LINE('No employees found in the database.');
    WHEN OTHERS THEN
        DBMS_OUTPUT.PUT_LINE('Unexpected error: ' || SQLERRM);
END;
```

*Output:*  
![image](https://github.com/user-attachments/assets/d3b560be-2a7b-433e-af6b-98f81e3c81cb)

---

### **Question 4: Cursor with %ROWTYPE and Exception Handling**

**Write a PL/SQL program that uses a cursor with %ROWTYPE to fetch and display complete employee records (emp_id, emp_name, designation, salary). Implement exception handling for the following errors:**
```
1. *NO_DATA_FOUND*: When no employees are found in the database.
2. *OTHERS*: For any other errors that occur.

*Steps:*

- Modify the employees table by adding emp_id, emp_name, designation, and salary fields.
- Insert sample data into the employees table.
- Declare a cursor using %ROWTYPE to fetch complete rows from the employees table.
- Implement exception handling to catch the relevant exceptions and display appropriate messages.

 *Program:*
sql
SET SERVEROUTPUT ON;

DECLARE
    CURSOR emp_cursor IS
        SELECT emp_id, emp_name, designation, salary FROM employees;

    emp_record emp_cursor%ROWTYPE;

    no_data BOOLEAN := TRUE;
BEGIN
    OPEN emp_cursor;
    LOOP
        FETCH emp_cursor INTO emp_record;
        EXIT WHEN emp_cursor%NOTFOUND;

        DBMS_OUTPUT.PUT_LINE('ID: ' || emp_record.emp_id ||
                             ', Name: ' || emp_record.emp_name ||
                             ', Designation: ' || emp_record.designation ||
                             ', Salary: ' || emp_record.salary);

        no_data := FALSE;
    END LOOP;
    CLOSE emp_cursor;

    IF no_data THEN
        RAISE NO_DATA_FOUND;
    END IF;

EXCEPTION
    WHEN NO_DATA_FOUND THEN
        DBMS_OUTPUT.PUT_LINE('No employee records found.');
    WHEN OTHERS THEN
        DBMS_OUTPUT.PUT_LINE('Unexpected error: ' || SQLERRM);
END;
```

*Output:*  
![image](https://github.com/user-attachments/assets/66d13cfb-0bfd-4263-8bc5-b866e2912492)

---

### *Question 5: Cursor with FOR UPDATE Clause and Exception Handling*

**Write a PL/SQL program using a cursor with the FOR UPDATE clause to update the salary of employees in a specific department. Implement exception handling for the following cases:**
```
1. *NO_DATA_FOUND*: If no rows are affected by the update.
2. *OTHERS*: For any unexpected errors during execution.

*Steps:*

- Modify the employees table to include a dept_no and salary field.
- Insert sample data into the employees table with different department numbers.
- Use a cursor with the FOR UPDATE clause to lock the rows of employees in a specific department and update their salary.
- Implement exception handling to handle NO_DATA_FOUND or other errors that may occur.

*Program:*
sql
SET SERVEROUTPUT ON;

DECLARE
    CURSOR emp_cursor (p_dept_no NUMBER) IS
        SELECT emp_id, emp_name, salary
        FROM employees
        WHERE dept_no = p_dept_no
        FOR UPDATE OF salary;
        
    v_rows_updated NUMBER := 0;
BEGIN
    FOR emp_rec IN emp_cursor(10) LOOP
        UPDATE employees
        SET salary = salary * 1.10
        WHERE CURRENT OF emp_cursor;
        
        v_rows_updated := v_rows_updated + 1;
    END LOOP;
    
    IF v_rows_updated = 0 THEN
        RAISE NO_DATA_FOUND;
    ELSE
        DBMS_OUTPUT.PUT_LINE('Salaries updated for ' || v_rows_updated || ' employees in department 10.');
    END IF;
    
EXCEPTION
    WHEN NO_DATA_FOUND THEN
        DBMS_OUTPUT.PUT_LINE('No employees found in the specified department.');
    WHEN OTHERS THEN
        DBMS_OUTPUT.PUT_LINE('An unexpected error occurred: ' || SQLERRM);
END;
/
```

*Output:*  
![image](https://github.com/user-attachments/assets/4828c843-7a64-4c9f-bfa5-90674b214862)

---

## RESULT
Thus, the program successfully executed and displayed employee details using a cursor.
