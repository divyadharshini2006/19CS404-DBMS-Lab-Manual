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
---
<img width="1916" height="924" alt="image" src="https://github.com/user-attachments/assets/8cb50501-30f2-455f-b121-a0b83d87f5ac" />

```sql
select Specialty,Gender, COUNT(*) AS "TotalDoctors"
from Doctors 
group by Specialty, Gender;
```

**Output:**

<img width="1896" height="1164" alt="image" src="https://github.com/user-attachments/assets/0407fbe2-ad6a-4347-9112-314790931431" />


**Question 2**
---
<img width="1900" height="1022" alt="image" src="https://github.com/user-attachments/assets/82f40f99-9ec8-4b59-8ea3-cec6c412c212" />

```sql
select DoctorID ,COUNT(*) as 'TotalPrescriptions'
from Prescriptions
group by DoctorID;
```

**Output:**

<img width="1524" height="1326" alt="image" src="https://github.com/user-attachments/assets/fb7b8517-b4d1-4a1e-9ccd-281aa50de57d" />


**Question 3**
---
<img width="1902" height="1052" alt="image" src="https://github.com/user-attachments/assets/9d2cde00-01ed-4bac-9c7a-969169ea2532" />


```sql
SELECT InsuranceCompany,count(*) as TotalPatients
from Insurance
group by InsuranceCompany;
```

**Output:**

<img width="952" height="606" alt="Screenshot 2025-10-15 at 10 53 04 AM" src="https://github.com/user-attachments/assets/4068f2dc-9103-4097-8ace-74902e73da55" />


**Question 4**
---
<img width="1904" height="780" alt="image" src="https://github.com/user-attachments/assets/be326299-73ba-42e3-9b16-405f3372217f" />

```sql
select COUNT(DISTINCT city) as unique_cities
from customer 

```

**Output:**

<img width="1914" height="638" alt="image" src="https://github.com/user-attachments/assets/c02fba74-2498-4961-92c7-2c85840e8bcb" />


**Question 5**
---
<img width="1912" height="756" alt="image" src="https://github.com/user-attachments/assets/d1d1590a-d48c-4ef7-a177-226fe5063830" />


```sql
select sum(purch_amt) as TOTAL
from orders 
```

**Output:**

<img width="1918" height="638" alt="image" src="https://github.com/user-attachments/assets/fcea1038-7c3a-46f6-a4f1-0c308e52fdcc" />



**Question 6**
---
<img width="1898" height="756" alt="image" src="https://github.com/user-attachments/assets/5b88c97c-aadb-4d8b-8193-ed5540cf87f2" />


```sql
select avg(income) as avg_income
from employee
where name like "A%"
```

**Output:**

<img width="1912" height="630" alt="image" src="https://github.com/user-attachments/assets/201ff936-68fe-411c-b29e-5f12ce374bc2" />


**Question 7**
---
<img width="1902" height="786" alt="image" src="https://github.com/user-attachments/assets/bd63a7b9-784d-4503-b2d5-b74dcfc46cb7" />

```sql
select count(city) as COUNT
from customer 
where city <> 'Noida';
```

**Output:**

<img width="1896" height="632" alt="image" src="https://github.com/user-attachments/assets/15793697-4351-45de-8874-871aedf04eee" />


**Question 8**
---
<img width="1902" height="866" alt="image" src="https://github.com/user-attachments/assets/95968f73-3271-400f-9c1e-044c15c8c989" />


```sql
select jdate,MIN(workhour) as 'MIN(workhour)'
from  employee1
group by jdate 
having MIN(workhour) < 10;
```

**Output:**

<img width="1890" height="818" alt="image" src="https://github.com/user-attachments/assets/97eff6ab-3f91-4627-9fbf-034cf1f810b6" />


**Question 9**
---
<img width="1892" height="858" alt="image" src="https://github.com/user-attachments/assets/f4e3274c-2761-4915-b218-2a17a81fb3f9" />


```sql
select PatientID ,count(*) as TotalRecords
from MedicalRecords
group by PatientID 
having TotalRecords > 3;
```

**Output:**

<img width="1908" height="668" alt="image" src="https://github.com/user-attachments/assets/4f5dea9b-a3dd-4b72-b5cb-220b2c8f0992" />


**Question 10**
---
<img width="1912" height="826" alt="image" src="https://github.com/user-attachments/assets/0d3f8bef-e194-4b88-aff5-9bebecee3a74" />


```sql
select category_id , AVG(Price) as 'AVG(Price)'
from products 
group by category_id
having AVG(Price) between 10 and 15 ;
```

**Output:**

<img width="1904" height="680" alt="image" src="https://github.com/user-attachments/assets/5d16dcf0-2665-4799-b62f-fa3c480e9870" />

**SEB:**
<img width="2102" height="170" alt="image" src="https://github.com/user-attachments/assets/d5b8db12-9be1-4928-bf38-490af6876733" />


## RESULT
Thus, the SQL queries to implement aggregate functions, GROUP BY, and HAVING clause have been executed successfully.
