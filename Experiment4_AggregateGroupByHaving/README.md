# Experiment 4: Aggregate Functions, Group By and Having Clause

## AIM
To study and implement aggregate functions, GROUP BY, and HAVING clause with suitable examples.

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
How many patients have insurance coverage valid in each year?

Sample table:Insurance Table

name               type
-----------------  ----------
InsuranceID        INTEGER
PatientID          INTEGER
InsuranceCompany   TEXT
PolicyNumber       TEXT
PolicyHolder       TEXT
ValidityPeriod     TEXT
For example:

Result
ValidityYear  TotalPatients
------------  -------------
2024          3
2025          1
2027          4
2031          2


```sql
SELECT 
    CAST(substr(ValidityPeriod, 1, 4) AS INTEGER) AS ValidityYear,
    COUNT(DISTINCT PatientID) AS TotalPatients
FROM Insurance
GROUP BY ValidityYear
ORDER BY ValidityYear;
```

**Output:**
<img width="738" height="377" alt="image" src="https://github.com/user-attachments/assets/baf3d97b-35dc-4137-a578-2126a8a6ffd4" />


**Question 2**
---
Write the SQL query that accomplishes the selection of average price for each category from the "products" table and includes only those products where the average price falls between 10 and 15.

Sample table: products



For example:

Result
category_id  AVG(Price)
-----------  ----------
1            12.375


```sql
SELECT category_id,
       AVG(Price)
FROM products
GROUP BY category_id
HAVING AVG(price) BETWEEN 10 AND 15;
```

**Output:**
<img width="614" height="322" alt="image" src="https://github.com/user-attachments/assets/4818cb8c-e3d4-4c54-a890-87c9ca3d2109" />


**Question 3**
---
Write the SQL query that achieves the selection of category and calculates the sum of the product of price and category ID as Revenue for each category from the "products" table, and includes only those products where the total revenue is greater than 25.

Sample table: products



For example:

Result
category_id  Revenue
-----------  ----------
1            49.5
2            126
3            79.44


```sql
SELECT category_id,
       SUM(price * category_id) AS Revenue
FROM products
GROUP BY category_id
HAVING SUM(price * category_id) > 25;
```

**Output:**
<img width="576" height="418" alt="image" src="https://github.com/user-attachments/assets/73de2624-4250-4e0b-95a8-a76486b81cda" />


**Question 4**
---
Write a SQL query to find the average length of email addresses (in characters):

Table: customer

name        type
----------  ----------
id          INTEGER
name        TEXT
city        TEXT
email       TEXT
phone       INTEGER
For example:

Result
avg_email_length
----------------
15.0

```sql
SELECT AVG(LENGTH(email)) AS avg_email_length
FROM customer;
```

**Output:**

<img width="535" height="294" alt="image" src="https://github.com/user-attachments/assets/eaf763ae-98ab-400d-9083-826aaaee03ac" />


**Question 5**
---
Write a SQL query to find the Fruit with the lowest available quantity.

Note: Inventory attribute contains amount of fruits

Table: fruits

name        type
----------  ----------
id          INTEGER
name        TEXT
unit        TEXT
inventory   INTEGER
price       REAL
 

For example:

Result
fruit_name  lowest_quantity
----------  ---------------
Watermelon  15


```sql
SELECT 
    name AS fruit_name,
    MIN(inventory) AS lowest_quantity
FROM fruits;
```

**Output:**

<img width="657" height="296" alt="image" src="https://github.com/user-attachments/assets/5aa7e80b-fc68-4cbb-bf6f-c91cc191e5d8" />


**Question 6**
---
Write a SQL query to calculate total purchase amount of all orders. Return total purchase amount.

Sample table: orders

ord_no      purch_amt   ord_date    customer_id  salesman_id

----------  ----------  ----------  -----------  -----------

70001       150.5       2012-10-05  3005         5002

70009       270.65      2012-09-10  3001         5005

70002       65.26       2012-10-05  3002         5001

For example:

Result
TOTAL
----------
17541.18


```sql
SELECT SUM(purch_amt) AS TOTAL
FROM orders;
```

**Output:**
<img width="403" height="276" alt="image" src="https://github.com/user-attachments/assets/7bc20cf1-43da-4f02-8acb-f65960f7414d" />


**Question 7**
---
Write a SQL query to  find the average salary of all employees?

Table: employee

name        type
----------  ----------
id          INTEGER
name        TEXT
age         INTEGER
city        TEXT
income      INTEGER
 

For example:

Result
Average_Salary
--------------
1568750.0


```sql
SELECT AVG(income) AS Average_Salary
FROM employee;
```

**Output:**

<img width="483" height="299" alt="image" src="https://github.com/user-attachments/assets/e076bacd-df29-4f9f-87c4-f205ea5bbf73" />


**Question 8**
---
Write the SQL query that achieves the selection of category and calculates the sum of the product of price and category ID as Revenue for each category from the "products" table, and includes only those products where the total revenue is greater than 25.

Sample table: products



For example:

Result
category_id  Revenue
-----------  ----------
1            49.5
2            126
3            79.44


```sql
SELECT category_id,
       SUM(price * category_id) AS Revenue
FROM products
GROUP BY category_id
HAVING SUM(price * category_id) > 25;
```

**Output:**
<img width="620" height="408" alt="image" src="https://github.com/user-attachments/assets/8816d1c9-17ab-4498-b0f3-f7820019b92e" />


**Question 9**
---
Write the SQL query that accomplishes the grouping of data by addresses, calculates the sum of salaries for each address, and excludes addresses where the total salary sum is not greater than 2000.

Sample table: customer1



For example:

Result
address     SUM(salary)
----------  -----------
Bhopal      8500
Hyderabad   4500
Indore      10000
Mumbai      6500


```sql
SELECT address,
       SUM(salary)
FROM customer1
GROUP BY address
HAVING SUM(salary) > 2000;
```

**Output:**

<img width="658" height="467" alt="image" src="https://github.com/user-attachments/assets/ff292b1a-7a5e-4083-a4d0-4b03f7efb805" />


**Question 10**
---
Write the SQL query that accomplishes the selection of average price for each category from the "products" table and includes only those products where the average price falls between 10 and 15.

Sample table: products



For example:

Result
category_id  AVG(Price)
-----------  ----------
1            12.375


```sql
SELECT category_id,
       AVG(Price)
FROM products
GROUP BY category_id
HAVING AVG(price) BETWEEN 10 AND 15;
```

**Output:**

<img width="614" height="322" alt="image" src="https://github.com/user-attachments/assets/f6c53976-69fb-4216-8fe0-aef941579182" />



## RESULT
Thus, the SQL queries to implement aggregate functions, GROUP BY, and HAVING clause have been executed successfully.
