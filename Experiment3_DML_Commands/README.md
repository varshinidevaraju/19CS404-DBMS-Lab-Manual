# Experiment 3: DML Commands

## AIM
To study and implement DML (Data Manipulation Language) commands.

## THEORY

### 1. INSERT INTO
Used to add records into a relation.
These are three type of INSERT INTO queries which are as
A)Inserting a single record
*Syntax (Single Row):*
sql
INSERT INTO table_name (field_1, field_2, ...) VALUES (value_1, value_2, ...);

*Syntax (Multiple Rows):*
sql
INSERT INTO table_name (field_1, field_2, ...) VALUES
(value_1, value_2, ...),
(value_3, value_4, ...);

*Syntax (Insert from another table):*
sql
INSERT INTO table_name SELECT * FROM other_table WHERE condition;

### 2. UPDATE
Used to modify records in a relation.
Syntax:
sql
UPDATE table_name SET column1 = value1, column2 = value2 WHERE condition;

### 3. DELETE
Used to delete records from a relation.
*Syntax (All rows):*
sql
DELETE FROM table_name;

*Syntax (Specific condition):*
sql
DELETE FROM table_name WHERE condition;

### 4. SELECT
Used to retrieve records from a table.
*Syntax:*
sql
SELECT column1, column2 FROM table_name WHERE condition;

*Question 1*
--
![image](https://github.com/user-attachments/assets/ace60931-cc4c-4219-badc-f469a811d10f)


sql
UPDATE products
SET product_name = 'Grapefruit'
WHERE product_id = 4
;



*Output:*

![image](https://github.com/user-attachments/assets/d79a0863-c9ea-4eba-81f4-afa8b116ce0b)

*Question 2*
---
![image](https://github.com/user-attachments/assets/f9b28267-cade-4f0b-b49b-c795710f57e6)


sql
UPDATE suppliers
SET supplier_name = 'A1 Suppliers'
WHERE supplier_id = 8;


*Output:*

![image](https://github.com/user-attachments/assets/8f49b7c2-a663-4c68-9b15-a9415f5fd14d)


*Question 3*
---
![image](https://github.com/user-attachments/assets/b8564586-0dd9-4987-abd3-f14e529921ed)


sql
UPDATE Customer
SET grade = 5
WHERE city = 'Chennai'
;


*Output:*

![image](https://github.com/user-attachments/assets/686c12b7-f8f0-43ec-a6f4-53eff762ae54)


*Question 4*
---
![image](https://github.com/user-attachments/assets/78922170-86f8-46c8-b5a2-46661d7f92d6)


sql
UPDATE SALES
SET total_sell_price = quantity * sell_price  
WHERE product_id = 10
;


*Output:*

![image](https://github.com/user-attachments/assets/07c5cf07-4f9a-4ce2-9cf1-8406b9f0a0cd)


*Question 5*
---
![image](https://github.com/user-attachments/assets/fe511130-b174-4c72-9295-d39de8174cc2)


sql
DELETE FROM Customer
WHERE GRADE = 2
;



*Output:*

![image](https://github.com/user-attachments/assets/0d18a809-2f94-42b9-a136-8ff13a98b5ec)


*Question 6*
---
![image](https://github.com/user-attachments/assets/fe3338a3-a594-4624-b916-3b12c588499d)


sql
DELETE FROM Customer
WHERE CUST_COUNTRY = 'UK'
    AND WORKING_AREA = 'London'
    AND GRADE < 3;


*Output:*

![image](https://github.com/user-attachments/assets/1edf7284-3b74-4f08-a2b7-7cc4e6fd9b96)

*Question 7*
---
![image](https://github.com/user-attachments/assets/382e0a83-6157-4fe8-bf69-21151a895702)


sql
DELETE FROM customer
WHERE cust_city LIKE 'L%';


*Output:*

![image](https://github.com/user-attachments/assets/7da4455f-3d9b-4b7a-9e49-ba6248674d63)


*Question 8*
---
![image](https://github.com/user-attachments/assets/03b10915-c3d7-419c-8ef5-7ce7160b12cd)


sql
DELETE FROM customer
WHERE agent_code IN ('A003', 'A008');


*Output:*
![image](https://github.com/user-attachments/assets/1f7494a9-ab0a-454c-bb50-c2e4f6db992c)


*Question 9*
---
![image](https://github.com/user-attachments/assets/f56a205e-3ca8-4601-87cc-0fa26eb86688)


sql
DELETE FROM customer
WHERE CUST_COUNTRY NOT IN ('India', 'USA');


*Output:*
![image](https://github.com/user-attachments/assets/1fce7246-d44f-4b12-a102-1e6d5c80e683)


*Question 10*
---
![image](https://github.com/user-attachments/assets/fd64442e-8c31-4fd6-af07-ff3f7521ecf5)



sql
SELECT *
FROM salesman
WHERE commission BETWEEN 0.12 AND 0.14;


*Output:*

![image](https://github.com/user-attachments/assets/10aa3731-bc8c-4fbf-8480-c3473a0ca4cc)

## RESULT
Thus, the SQL queries to implement DML commands have been executed successfully.
