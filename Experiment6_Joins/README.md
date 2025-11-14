# Experiment 6: Joins

## AIM
To study and implement different types of joins.

## THEORY

SQL Joins are used to combine records from two or more tables based on a related column.

### 1. INNER JOIN
Returns records with matching values in both tables.

**Syntax:**
```sql
SELECT columns
FROM table1
INNER JOIN table2
ON table1.column = table2.column;
```

### 2. LEFT JOIN
Returns all records from the left table, and matched records from the right.

**Syntax:**

```sql
SELECT columns
FROM table1
LEFT JOIN table2
ON table1.column = table2.column;
```
### 3. RIGHT JOIN
Returns all records from the right table, and matched records from the left.

**Syntax:**

```sql
SELECT columns
FROM table1
RIGHT JOIN table2
ON table1.column = table2.column;
```
### 4. FULL OUTER JOIN
Returns all records when there is a match in either left or right table.

**Syntax:**

```sql
SELECT columns
FROM table1
FULL OUTER JOIN table2
ON table1.column = table2.column;
```

**Question 1**
--
From the following tables write a SQL query to display the customer name, customer city, grade, salesman, salesman city. The results should be sorted by ascending customer_id.  

```sql
SELECT 
    c.cust_name AS "cust_name",
    c.city AS "city",
    c.grade AS "grade",
    s.name AS "Salesman",
    s.city AS "city"
FROM 
    customer c
JOIN 
    salesman s 
ON 
    c.salesman_id = s.salesman_id
ORDER BY 
    c.customer_id ASC;

```

**Output:**

<img width="1244" height="716" alt="image" src="https://github.com/user-attachments/assets/507cb58f-56d2-444d-86f3-f0e3dd336c37" />


**Question 2**
---
From the following tables write a SQL query to find those orders where the order amount exists between 500 and 2000. Return ord_no, purch_amt, cust_name, city.

```sql
SELECT 
    o.ord_no AS "ord_no",
    o.purch_amt AS "purch_amt",
    c.cust_name AS "cust_name",
    c.city AS "city"
FROM 
    orders o
JOIN 
    customer c 
ON 
    o.customer_id = c.customer_id
WHERE 
    o.purch_amt BETWEEN 500 AND 2000
ORDER BY 
    o.ord_no;

```

**Output:**
<img width="1215" height="409" alt="image" src="https://github.com/user-attachments/assets/d0976350-3988-4a64-9948-95771398c6aa" />


**Question 3**
---
Write the SQL query that achieves the selection of the first name from the "patients" table (aliased as "patient_name") and the first name from the "doctors" table (aliased as "doctor_name"), with an inner join on the "doctor_id" column and a condition filtering for patients with a null discharge date.

```sql
SELECT 
    p.first_name AS patient_name,
    d.first_name AS doctor_name
FROM 
    patients p
INNER JOIN 
    doctors d 
ON 
    p.doctor_id = d.doctor_id
WHERE 
    p.discharge_date IS NULL;

```

**Output:**

<img width="683" height="412" alt="image" src="https://github.com/user-attachments/assets/6657905a-6016-49db-8388-bb5c0b934f7c" />


**Question 4**
---
Write the SQL query that achieves the selection of the "name" column from the "salesman" table (aliased as "salesman_name") and the "cust_name" column from the "customer" table (aliased as "customer_name"), with a left join on the "salesman_id" column.

Customer Table: (customer_id, cust_name, city, grade, salesman_id)

Salesman Table: (salesman_id, name, city, commission)

```sql
SELECT
    s.name AS "salesman_name",
    c.cust_name AS "customer_name"
FROM
    salesman s
LEFT JOIN
    customer c ON s.salesman_id = c.salesman_id;


```

**Output:**

<img width="682" height="815" alt="image" src="https://github.com/user-attachments/assets/9edae1cc-c468-42db-a7b3-560502d5b32f" />


**Question 5**
---
From the following tables write a SQL query to find the details of an order. Return ord_no, ord_date, purch_amt, Customer Name, grade, Salesman, commission. 

```sql
SELECT
    o.ord_no,
    o.ord_date,
    o.purch_amt,
    c.cust_name AS "Customer Name",
    c.grade,
    s.name AS "Salesman",
    s.commission
FROM
    orders o
JOIN
    customer c ON o.customer_id = c.customer_id
JOIN
    salesman s ON o.salesman_id = s.salesman_id;

```

**Output:**
<img width="1325" height="801" alt="image" src="https://github.com/user-attachments/assets/0ee930c5-e876-49ee-9434-fd90ee16aed5" />


**Question 6**
---
write a SQL query to find the salesperson and customer who reside in the same city. Return Salesman, cust_name and city.

```sql
SELECT
    s.name AS "Salesman",
    c.cust_name,
    c.city
FROM
    salesman s
JOIN
    customer c ON s.city = c.city;

```

**Output:**

<img width="1024" height="663" alt="image" src="https://github.com/user-attachments/assets/bb4e214b-7c9c-4353-87e3-8c953a1d8c7f" />


**Question 7**
---
Write the SQL query that achieves the selection of all columns from the "patients" table (aliased as "p"), with an inner join on the "patient_id" column and conditions filtering for test results with the test names 'Blood Test' or 'Blood Pressure' and results not containing the substring 'Normal'.

```sql
CREATE TABLE test_result (
    result_id INTEGER PRIMARY KEY,
    patient_id INTEGER,
    test_name TEXT,
    result TEXT,
    test_date DATE
);
INSERT INTO test_result (result_id, patient_id, test_name, result, test_date) VALUES
(1, 1, 'Blood Test', 'High Cholesterol', '2024-01-12'),
(2, 1, 'Blood Pressure', 'Above Normal', '2024-01-13'),
(3, 2, 'Blood Test', 'Normal', '2024-02-10'),
(4, 3, 'Urine Test', 'Normal', '2024-03-01');
SELECT 
    p.*
FROM 
    patients p
INNER JOIN 
    test_result t 
ON 
    p.patient_id = t.patient_id
WHERE 
    t.test_name IN ('Blood Test', 'Blood Pressure')
    AND t.result NOT LIKE '%Normal%';

```

**Output:**

<img width="1509" height="268" alt="image" src="https://github.com/user-attachments/assets/8ebdfdbe-5de6-4564-b402-7452b4a9d383" />


**Question 8**
---
Write an SQL query to retrieve all columns from the 'customer' table (aliased as 'c') using a LEFT JOIN with the 'orders' table on the 'customer_id' column, and filter the results to include only those orders placed between '2012-07-01' and '2012-07-30'.

```sql
SELECT 
    c.*
FROM 
    customer c
LEFT JOIN 
    orders o 
ON 
    c.customer_id = o.customer_id
WHERE 
    o.ord_date BETWEEN '2012-07-01' AND '2012-07-30';

```

**Output:**

<img width="1270" height="300" alt="image" src="https://github.com/user-attachments/assets/75cb742b-e70c-4f2c-a59e-c35121131077" />


**Question 9**
---
Write a SQL statement to make a report with customer name, city, order number, order date, and order amount in ascending order according to the order date to determine whether any of the existing customers have placed an order or not.

```sql
SELECT 
    c.cust_name AS "cust_name",
    c.city AS "city",
    o.ord_no AS "ord_no",
    o.ord_date AS "ord_date",
    o.purch_amt AS "Order Amount"
FROM 
    customer c
LEFT JOIN 
    orders o 
ON 
    c.customer_id = o.customer_id
ORDER BY 
    o.ord_date ASC;

```

**Output:**
<img width="1050" height="791" alt="image" src="https://github.com/user-attachments/assets/d74de3aa-31cb-40a2-8208-c43ebb8369e5" />


**Question 10**
---
Write the SQL query that achieves the selection of all columns from the "patients" table (aliased as "p"), with an inner join on the "patient_id" column and a condition filtering for test results with a test date between '2024-03-01' and '2024-03-31'.

```sql
CREATE TABLE test_result (
    result_id INTEGER PRIMARY KEY,
    patient_id INTEGER,
    test_name TEXT,
    result TEXT,
    test_date DATE
);
INSERT INTO test_result (result_id, patient_id, test_name, result, test_date) VALUES
(1, 1, 'Blood Test', 'High Cholesterol', '2024-02-28'),
(2, 2, 'Blood Pressure', 'Above Normal', '2024-03-01'),
(3, 3, 'Urine Test', 'Normal', '2024-03-15'),
(4, 2, 'Blood Test', 'Normal', '2024-03-20');
SELECT DISTINCT p.*
FROM patients p
INNER JOIN test_result tr ON p.patient_id = tr.patient_id
WHERE tr.test_date BETWEEN '2024-03-01' AND '2024-03-31'
AND p.first_name <> 'Charlie';





```

**Output:**

<img width="1721" height="313" alt="image" src="https://github.com/user-attachments/assets/ea4bf918-6c39-4b78-8556-b0f1a155865d" />



## RESULT
Thus, the SQL queries to implement different types of joins have been executed successfully.
