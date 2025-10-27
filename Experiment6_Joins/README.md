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
<img width="1982" height="1290" alt="image" src="https://github.com/user-attachments/assets/8dd12a44-7c8a-40ac-8bcd-81f2d06edeb0" />

```sql
select p.first_name as "patient_name", d.first_name as "doctor_name"
from PATIENTS p
join doctors d on p.doctor_id=d.doctor_id
where p.discharge_date is not null;
```

**Output:**

<img width="1982" height="778" alt="image" src="https://github.com/user-attachments/assets/07170bf8-5a24-4c3a-b4ad-d1fff6840351" />


**Question 2**
---
<img width="992" height="354" alt="Screenshot 2025-10-27 at 1 38 14 PM" src="https://github.com/user-attachments/assets/e3a050f6-416c-4cbe-a499-b98a19dd6d18" />


```sql
select s.name , c.cust_name,c.city,c.grade,s.salesman_id 
from Customer c
left join Salesman s on c.salesman_id=s.salesman_id
where c.grade<=100
```

**Output:**

<img width="1994" height="1018" alt="image" src="https://github.com/user-attachments/assets/5de9a567-bd0b-4041-b2de-f7cd8e9501ee" />


**Question 3**
---
<img width="1992" height="1560" alt="image" src="https://github.com/user-attachments/assets/0466a0a4-345e-4c34-bf2f-57b4a2037269" />


```sql
select c.cust_name, c.city,c.grade,s.name as "Salesman",s.city
from customer c
join salesman s on c.salesman_id=s.salesman_id 
order by c.customer_id asc
```

**Output:**

<img width="1986" height="1498" alt="image" src="https://github.com/user-attachments/assets/4de113df-d893-4ae6-8c77-659239697363" />


**Question 4**
---
<img width="1988" height="1282" alt="image" src="https://github.com/user-attachments/assets/8c8c043b-b4ba-4e5a-bc58-3630b0185b7a" />

```sql
select p.first_name from PATIENTS p
join SURGERIES s on p.patient_id=s.patient_id
where s.surgery_date='2024-01-15';
```

**Output:**

<img width="1974" height="764" alt="image" src="https://github.com/user-attachments/assets/83bec534-9c02-496f-ae74-419ebfab20a7" />


**Question 5**
---
<img width="1990" height="1564" alt="image" src="https://github.com/user-attachments/assets/70e17645-1485-4291-aa62-81f9caa5f0a2" />


```sql
select o.ord_no,o.purch_amt,o.ord_date,c.cust_name,c.city as "customer_city",c.grade,s.name as"salesman_name",s.city as"salesman_city",s.commission
from orders o
join customer c on o.customer_id=c.customer_id
join salesman s on o.salesman_id=s.salesman_id
```

**Output:**

<img width="1992" height="1212" alt="image" src="https://github.com/user-attachments/assets/1dfcdb7a-15c7-407b-9120-0298d187a626" />


**Question 6**
---
<img width="1974" height="1110" alt="image" src="https://github.com/user-attachments/assets/a077a889-3f68-4d8e-a49d-96c89842a212" />


```sql
select c.cust_name,o.ord_no,o.ord_date,o.purch_amt
from customer c
left join orders o on c.customer_id=o.customer_id
```

**Output:**

<img width="1986" height="1466" alt="image" src="https://github.com/user-attachments/assets/ede2262a-a76a-4c97-b3af-3503a3984ea8" />


**Question 7**
---
<img width="1974" height="1568" alt="image" src="https://github.com/user-attachments/assets/5863a3f3-fb8a-4ee5-99e2-28160e2a507d" />


```sql
select o.ord_no,o.ord_date,o.purch_amt,c.cust_name as"Customer Name",c.grade,s.name as"Salesman",s.commission
from orders o
join customer c on o.customer_id=c.customer_id
join salesman s on o.salesman_id=s.salesman_id
```

**Output:**

<img width="1984" height="1426" alt="image" src="https://github.com/user-attachments/assets/3cb96604-ff9c-4dcb-b060-34653b860a16" />

**Question 8**
---
<img width="1974" height="1278" alt="image" src="https://github.com/user-attachments/assets/ce8a3c11-5344-4ea4-9d1b-913645431317" />


```sql
select p.first_name, p.last_name 
from PATIENTS p
join SURGERIES s on p.patient_id=s.patient_id
where s.surgery_date between '2024-01-01' and '2024-01-31';
```

**Output:**

<img width="1956" height="774" alt="image" src="https://github.com/user-attachments/assets/58930bda-3fc3-4cf8-a261-0874494e26cc" />


**Question 9**
---
<img width="1978" height="1432" alt="image" src="https://github.com/user-attachments/assets/7a4f76ba-564e-4a73-adfa-a84f1c888f78" />


```sql
select s.name as "Salesman",c.cust_name,c.city 
from salesman s
join customer c on s.city=c.city
```

**Output:**

<img width="1974" height="1240" alt="image" src="https://github.com/user-attachments/assets/f08cc36b-6635-430a-918f-fd2445f28892" />


**Question 10**
---
<img width="1988" height="1520" alt="image" src="https://github.com/user-attachments/assets/df50cc25-9d70-445b-a24d-21ad0dfc5d46" />

```sql
select c.cust_name,c.city,c.grade,s.name as"Salesman",s.city 
from customer c
join salesman s on c.salesman_id=s.salesman_id 
where c.grade<300 
order by c.customer_id asc
```

**Output:**

<img width="1990" height="1342" alt="image" src="https://github.com/user-attachments/assets/e5adacdf-8d6f-4bc7-b32d-df2b6f9f85a2" />

**SEB EXAM**
<img width="2114" height="134" alt="image" src="https://github.com/user-attachments/assets/38ab76b8-772d-405d-8378-765888ec89a8" />


## RESULT
Thus, the SQL queries to implement different types of joins have been executed successfully.
