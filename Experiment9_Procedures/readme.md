# Experiment 9: PL/SQL – Procedures and Functions

## AIM
To understand and implement procedures and functions in PL/SQL for performing various operations such as calculations, decision-making, and looping.

## THEORY

PL/SQL (Procedural Language/SQL) extends SQL by adding procedural constructs like variables, conditions, loops, procedures, and functions. Procedures and functions are subprograms that help modularize the code and improve reusability.

### *Procedure*
A PL/SQL *procedure* is a subprogram that performs a specific action. It does not return a value directly but can return values using OUT parameters.

```
*Syntax:*
sql
CREATE OR REPLACE PROCEDURE procedure_name (parameters)
IS
BEGIN
   -- statements
END;
```

To call the procedure

sql
EXEC procedure_name(arguments);


### *Function*
A PL/SQL *function* is a subprogram that returns a single value using the RETURN keyword.
```
sql
CREATE OR REPLACE FUNCTION function_name (parameters)
RETURN datatype
IS
BEGIN
   -- statements
   RETURN value;
END;
```

To call the function:

sql
SELECT function_name(arguments) FROM DUAL;


Key Differences:

-A procedure does not return a value, whereas a function must return a value.
-Functions can be called from SQL queries, procedures cannot (in most cases).

## 1. Write a PL/SQL Procedure to Find the Square of a Number

### Steps:
- Create a procedure named find_square.
- Declare a parameter to accept a number.
- Inside the procedure, compute the square of the input number.
- Use DBMS_OUTPUT.PUT_LINE to display the result.
- Call the procedure with a number as input.
```
*Program:*
sql
SET SERVEROUTPUT ON;

CREATE OR REPLACE PROCEDURE find_square (num IN NUMBER) IS
    sq NUMBER;
BEGIN
    sq := num * num;
    DBMS_OUTPUT.PUT_LINE('Square of ' || num || ' is ' || sq);
END;
/

BEGIN
    find_square(6);
END;
/
```


*Output:*
![image](https://github.com/user-attachments/assets/b3cf8c94-fe63-47db-b227-c0b8db64d7ea)

*Expected Output:*  
Square of 6 is 36


## 2. Write a PL/SQL Function to Return the Factorial of a Number

### Steps:
- Create a function named get_factorial.
- Declare a parameter to accept a number.
- Use a loop to calculate the factorial.
- Return the result using the RETURN statement.
- Call the function using a SELECT statement or in an anonymous block.
  
```
*Program:*
sql
SET SERVEROUTPUT ON;

CREATE OR REPLACE FUNCTION get_factorial (num IN NUMBER) RETURN NUMBER IS
    fact NUMBER := 1;
BEGIN
    FOR i IN 1..num LOOP
        fact := fact * i;
    END LOOP;
    RETURN fact;
END;
/

DECLARE
    result NUMBER;
BEGIN
    result := get_factorial(5);
    DBMS_OUTPUT.PUT_LINE('Factorial of 5 is ' || result);
END;
/
```


*Output:*

  ![image](https://github.com/user-attachments/assets/a0db2454-65ff-4270-946d-e0826e5c3d06)

*Expected Output:*  
Factorial of 5 is 120

---

## 3. Write a PL/SQL Procedure to Check Whether a Number is Even or Odd

### Steps:
- Create a procedure named check_even_odd.
- Accept an input parameter.
- Use the MOD function to check if the number is divisible by 2.
- Display whether it is Even or Odd using DBMS_OUTPUT.PUT_LINE.
```
*Program:*
sql
SET SERVEROUTPUT ON;

CREATE OR REPLACE PROCEDURE check_even_odd (num IN NUMBER) IS
BEGIN
    IF MOD(num, 2) = 0 THEN
        DBMS_OUTPUT.PUT_LINE(num || ' is Even');
    ELSE
        DBMS_OUTPUT.PUT_LINE(num || ' is Odd');
    END IF;
END;
/

-- Calling the procedure
BEGIN
    check_even_odd(12);
END;
/
```


*Output:*

![image](https://github.com/user-attachments/assets/eb0b9436-1e78-4625-9320-9f125cc0aede)

*Expected Output:*  
12 is Even

---

## 4. Write a PL/SQL Function to Return the Reverse of a Number

### Steps:
- Create a function named reverse_number.
- Accept an input number as parameter.
- Use a loop to reverse the digits of the number.
- Return the reversed number.
- Call the function and display the output.
```
*Program:*
sql
SET SERVEROUTPUT ON;

CREATE OR REPLACE FUNCTION reverse_number (num IN NUMBER) RETURN NUMBER IS
    rev_num NUMBER := 0;
    temp_num NUMBER := num;
BEGIN
    WHILE temp_num > 0 LOOP
        rev_num := rev_num * 10 + MOD(temp_num, 10);
        temp_num := FLOOR(temp_num / 10);
    END LOOP;
    RETURN rev_num;
END;
/
```
-- Calling the function and displaying output
DECLARE
    rev_result NUMBER;
BEGIN
    rev_result := reverse_number(1234);
    DBMS_OUTPUT.PUT_LINE('Reversed number of 1234 is ' || rev_result);
END;
/



*Output:*

![image](https://github.com/user-attachments/assets/89d0ded7-a2f9-467c-b0ef-f20971a33d79)

*Expected Output:*  
Reversed number of 1234 is 4321

```
---

## 5. Write a PL/SQL Procedure to Display the Multiplication Table of a Number

### Steps:
- Create a procedure named print_table.
- Accept an input number.
- Use a loop from 1 to 10 to multiply the input number.
- Display the multiplication results using DBMS_OUTPUT.PUT_LINE.
```
*Program:*
sql
SET SERVEROUTPUT ON;

CREATE OR REPLACE PROCEDURE print_table (num IN NUMBER) IS
BEGIN
    DBMS_OUTPUT.PUT_LINE('Multiplication table of ' || num || ':');
    FOR i IN 1..10 LOOP
        DBMS_OUTPUT.PUT_LINE(num || ' x ' || i || ' = ' || (num * i));
    END LOOP;
END;
/

-- Calling the procedure
BEGIN
    print_table(5);
END;
/



*Output:*

![image](https://github.com/user-attachments/assets/12625873-6b80-4936-8276-50f607cf3f82)

```
*Expected Output:*  
Multiplication table of 5:  
5 x 1 = 5  
5 x 2 = 10  
5 x 3 = 15  
...  
5 x 10 = 50

```
## RESULT
Thus, the PL/SQL programs using procedures and functions were written, compiled, and executed successfully.
