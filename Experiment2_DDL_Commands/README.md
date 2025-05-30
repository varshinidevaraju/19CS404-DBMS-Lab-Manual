# Experiment 2: DDL Commands

## AIM
To study and implement DDL commands and different types of constraints.
```
NAME:VARSHINI D
REG NO:212223230234

```
## THEORY
```
### 1. CREATE
Used to create a new relation (table).

*Syntax:*
sql
CREATE TABLE (
  field_1 data_type(size),
  field_2 data_type(size),
  ...
);

### 2. ALTER
Used to add, modify, drop, or rename fields in an existing relation.
(a) ADD
sql
ALTER TABLE std ADD (Address CHAR(10));

(b) MODIFY
sql
ALTER TABLE relation_name MODIFY (field_1 new_data_type(size));

(c) DROP
sql
ALTER TABLE relation_name DROP COLUMN field_name;

(d) RENAME
sql
ALTER TABLE relation_name RENAME COLUMN old_field_name TO new_field_name;

### 3. DROP TABLE
Used to permanently delete the structure and data of a table.
sql
DROP TABLE relation_name;

### 4. RENAME
Used to rename an existing database object.
sql
RENAME TABLE old_relation_name TO new_relation_name;

### CONSTRAINTS
Constraints are used to specify rules for the data in a table. If there is any violation between the constraint and the data action, the action is aborted by the constraint. It can be specified when the table is created (using CREATE TABLE) or after it is created (using ALTER TABLE).
### 1. NOT NULL
When a column is defined as NOT NULL, it becomes mandatory to enter a value in that column.
Syntax:
sql
CREATE TABLE Table_Name (
  column_name data_type(size) NOT NULL
);

### 2. UNIQUE
Ensures that values in a column are unique.
Syntax:
sql
CREATE TABLE Table_Name (
  column_name data_type(size) UNIQUE
);

### 3. CHECK
Specifies a condition that each row must satisfy.
Syntax:
sql
CREATE TABLE Table_Name (
  column_name data_type(size) CHECK (logical_expression)
);

### 4. PRIMARY KEY
Used to uniquely identify each record in a table.
Properties:
Must contain unique values.
Cannot be null.
Should contain minimal fields.
Syntax:
sql
CREATE TABLE Table_Name (
  column_name data_type(size) PRIMARY KEY
);

### 5. FOREIGN KEY
Used to reference the primary key of another table.
Syntax:
sql
CREATE TABLE Table_Name (
  column_name data_type(size),
  FOREIGN KEY (column_name) REFERENCES other_table(column)
);

### 6. DEFAULT
Used to insert a default value into a column if no value is specified.

Syntax:
sql
CREATE TABLE Table_Name (
  col_name1 data_type,
  col_name2 data_type,
  col_name3 data_type DEFAULT 'default_value'
);
```
*Question 1*
--
![image](https://github.com/user-attachments/assets/66163850-1dfd-490e-ab70-714d31038dab)

```
sql
CREATE TABLE products(
product_id INTEGER PRIMARY KEY,
product_name TEXT NOT NULL,
list_price DECIMAL(10,2) NOT NULL check(list_price>=discount and list_price>=0),
discount DECIMAL(10,2) default 0 NOT NULL check(discount>=0)
);
```

*Output:*

![image](https://github.com/user-attachments/assets/c843e10b-ef45-417e-83fb-58be29f4da55)


*Question 2*
---
![image](https://github.com/user-attachments/assets/be02b6d8-a4c8-4e2f-a5b8-fbab9132c04d)

```
sql
INSERT INTO Products(ProductID,Name,CategorY,Price,Stock)
VALUES(101,"Laptop","Electronics",1500,50);
```

*Output:*

![image](https://github.com/user-attachments/assets/30acff29-1563-42f2-982e-e90aa291eddf)


*Question 3*
---
![image](https://github.com/user-attachments/assets/425b3d39-d66e-4618-9c22-9773dd4b6e72)

```
sql
select * from Archived_students
UNION ALL
select * from Student_details 
```

*Output:*

![image](https://github.com/user-attachments/assets/601e5e3e-7f03-4d74-86f8-a1e011ff6d12)


*Question 4*
---
![image](https://github.com/user-attachments/assets/747e11fe-7cb1-4b3f-b9cd-28be76802894)

```
sql
ALTER TABLE Student_details 
ADD COLUMN "MobileNumber" NUMBER;

ALTER TABLE Student_details 
ADD COLUMN "Address" VARCHAR(100);
```

*Output:*

![image](https://github.com/user-attachments/assets/b6f271e4-c343-487c-bcb5-6271ec3adcbf)


*Question 5*
---
![image](https://github.com/user-attachments/assets/c766706c-1512-4302-a6f7-7af9ba34b2ca)

```
sql
ALTER TABLE customer
ADD COLUMN "discount" DECIMAL(5,2);
```

*Output:*

![image](https://github.com/user-attachments/assets/7b6f2041-2f44-466b-97c9-b616362085ea)


*Question 6*
---
![image](https://github.com/user-attachments/assets/e55da1b2-0761-4941-8928-885f2f77c46e)

```
sql
CREATE TABLE item(
item_id TEXT PRIMARY KEY,
item_desc TEXT NOT NULL,
rate  INTEGER NOT NULL,
icom_id TEXT(4),
FOREIGN KEY (icom_id) references company(com_id)
ON UPDATE CASCADE
ON DELETE CASCADE


);
```

*Output:*

![image](https://github.com/user-attachments/assets/fbd203fd-772b-4575-9749-79563558d14c)


*Question 7*
---
![image](https://github.com/user-attachments/assets/e070a37e-e77b-4aa6-aa35-a06f4e5a3240)

```
sql
CREATE TABLE Shipments(
ShipmentID INTEGER PRIMARY KEY,
ShipmentDate DATE,
SupplierID INTEGER,
OrderID INTEGER,
foreign key(SupplierID) references Suppliers(SupplierID),
foreign key(OrderID) references Orders(OrderID)

);
```

*Output:*

![image](https://github.com/user-attachments/assets/12f1be83-964a-4323-8a6e-8dad3dbb65b8)


*Question 8*
---
![image](https://github.com/user-attachments/assets/b817bd9e-b967-45bc-ab20-8a65bf2efa3f)
```

sql
CREATE TABLE jobs(
job_id INTEGER PRIMARY KEY,
job_title TEXT DEFAULT '',
min_salary INTEGER DEFAULT 8000,
max_salary INTEGER DEFAULT NULL


);

```
*Output:*

![image](https://github.com/user-attachments/assets/497282ed-b6ef-4570-b93d-01d6297d2419)


*Question 9*
---
![image](https://github.com/user-attachments/assets/e15ff118-f046-4fe5-8f01-6a92613e24e6)

```
sql
CREATE TABLE Events(
EventID INTEGER,
EventName TEXT,
EventDate DATE


); 
```

*Output:*

![image](https://github.com/user-attachments/assets/680c6ec5-f2a3-4a07-996f-7073370a0d48)


*Question 10*
---
![image](https://github.com/user-attachments/assets/2a734cc4-f361-460d-8efb-31d4ac5a8a82)

```
sql
INSERT INTO Customers(ID,NAME,AGE,ADDRESS,SALARY)
VALUES(1,"Ramesh",32,"Ahmedabad",2000),
(2,"Khilan",25,"Delhi",1500),
(3,"Kaushik",23,"Kota",2000);

```
*Output:*

![image](https://github.com/user-attachments/assets/6c2cdcb8-6c4a-43da-b6a8-e8bcc4d6f925)

## RESULT
Thus, the SQL queries to implement different types of constraints and DDL commands have been executed successfully.
