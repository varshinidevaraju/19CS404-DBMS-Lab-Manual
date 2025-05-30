# Experiment 4: Aggregate Functions, Group By and Having Clause

## AIM
To study and implement aggregate functions, GROUP BY, and HAVING clause with suitable examples.
```
NAME:VARSHINI D
REG NO:212223230234
```
## THEORY

### Aggregate Functions
These perform calculations on a set of values and return a single value.

- **MIN()** – Smallest value  
- **MAX()** – Largest value  
- **COUNT()** – Number of rows  
- **SUM()** – Total of values  
- **AVG()** – Average of values

**Syntax:**
```sql
SELECT AGG_FUNC(column_name) FROM table_name WHERE condition;
```
### GROUP BY
Groups records with the same values in specified columns.
**Syntax:**
```sql
SELECT column_name, AGG_FUNC(column_name)
FROM table_name
GROUP BY column_name;
```
### HAVING
Filters the grouped records based on aggregate conditions.
**Syntax:**
```sql
SELECT column_name, AGG_FUNC(column_name)
FROM table_name
GROUP BY column_name
HAVING condition;
```

**Question 1**
--
![image](https://github.com/user-attachments/assets/dae06e32-6d28-4a98-9338-756428d42376)

```sql
SELECT DoctorID, COUNT(RecordID) AS TotalRecords FROM MedicalRecords GROUP BY DoctorID;
```

**Output:**

![image](https://github.com/user-attachments/assets/0be031fb-2cdf-4c4e-85fb-1615b27caddc)

**Question 2**
---
![image](https://github.com/user-attachments/assets/4a936c72-b258-455c-99cd-e37e8f94e261)

```sql
SELECT InsuranceCompany, SUM(DATE('now')>SUBSTR(ValidityPeriod,15)) AS TotalExpiredPatients 
FROM Insurance GROUP BY InsuranceCompany;
```

**Output:**

![image](https://github.com/user-attachments/assets/685364b5-e4a8-4226-8902-357f04e15f65)

**Question 3**
---
![image](https://github.com/user-attachments/assets/de4489d2-7618-494b-9fdb-2fb0ca1a0188)

```sql
SELECT Frequency, COUNT(PrescriptionID) AS TotalPrescriptions FROM Prescriptions GROUP BY Frequency;
```

**Output:**

![image](https://github.com/user-attachments/assets/12f741e0-1801-42ec-98dd-38c44b06e304)

**Question 4**
---
![image](https://github.com/user-attachments/assets/0df295b1-ce51-4e6d-b1a5-bb09502860a1)

```sql
SELECT sum(purch_amt) AS TOTAL FROM orders;
```

**Output:**

![image](https://github.com/user-attachments/assets/015a1c3d-a2ce-44ab-a985-6916f9c726aa)

**Question 5**
---
![image](https://github.com/user-attachments/assets/d19924fd-1386-4a59-8d63-80009bf5aeac)

```sql
SELECT COUNT(distinct salesman_id) AS COUNT FROM orders;
```

**Output:**

![image](https://github.com/user-attachments/assets/12a2eb37-01dd-430f-b59b-8a256b61e05f)

**Question 6**
---
![image](https://github.com/user-attachments/assets/bdc23562-9cad-43f9-88b6-8b0ca18dd909)

```sql
SELECT COUNT(city) AS COUNT FROM customer GROUP BY city HAVING city='Noida'; 
```

**Output:**

![image](https://github.com/user-attachments/assets/5c71ead4-95a3-4cd2-b2e9-25af3e8733e8)

**Question 7**
---
![image](https://github.com/user-attachments/assets/44ec804d-b98c-4c1d-a88d-c22fc6353f50)

```sql
SELECT COUNT(distinct city) AS unique_cities FROM customer;
```

**Output:**

![image](https://github.com/user-attachments/assets/19bd13d0-0c70-4123-9e2e-4f0a96f00944)

**Question 8**
---
![image](https://github.com/user-attachments/assets/23e931de-10bf-490a-9ab2-e620be58bb70)

```sql
SELECT (age/5)*5 AS age_group, sum(salary) AS 'SUM(salary)' FROM customer1 GROUP BY age_group HAVING sum(salary)>5000;
```

**Output:**

![image](https://github.com/user-attachments/assets/cc762380-4493-446b-b5ae-2c0163ff8a93)

**Question 9**
---
![image](https://github.com/user-attachments/assets/607c8b39-de02-4dc4-881b-3fba1867fc04)

```sql
SELECT occupation, min(workhour) AS 'MIN(workhour)' FROM employee1 GROUP BY occupation HAVING MIN(workhour)>=8;
```

**Output:**

![image](https://github.com/user-attachments/assets/0ab32ddf-a462-477a-9ea3-15d28d6ae26a)

**Question 10**
---
![image](https://github.com/user-attachments/assets/96c9300c-fffa-4055-b552-38b220dd4888)

```sql
SELECT category_id, COUNT(product_name) AS 'count(product_name)' FROM products GROUP BY category_id HAVING min(category_id)<3;
```

**Output:**

![image](https://github.com/user-attachments/assets/4fbdd60e-5207-4bed-b62b-017161e6470d)

## RESULT
Thus, the SQL queries to implement aggregate functions, GROUP BY, and HAVING clause have been executed successfully.
