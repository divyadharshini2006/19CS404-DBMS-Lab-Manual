# Experiment 5: Subqueries and Views

## AIM
To study and implement subqueries and views.

## THEORY

### Subqueries
A subquery is a query inside another SQL query and is embedded in:
- WHERE clause
- HAVING clause
- FROM clause

**Types:**
- **Single-row subquery**:
  Sub queries can also return more than one value. Such results should be made use along with the operators in and any.
- **Multiple-row subquery**:
  Here more than one subquery is used. These multiple sub queries are combined by means of ‘and’ & ‘or’ keywords.
- **Correlated subquery**:
  A subquery is evaluated once for the entire parent statement whereas a correlated Sub query is evaluated once per row processed by the parent statement.

**Example:**
```sql
SELECT * FROM employees
WHERE salary > (SELECT AVG(salary) FROM employees);
```
### Views
A view is a virtual table based on the result of an SQL SELECT query.
**Create View:**
```sql
CREATE VIEW view_name AS
SELECT column1, column2 FROM table_name WHERE condition;
```
**Drop View:**
```sql
DROP VIEW view_name;
```

**Question 1**
--
<img width="990" height="544" alt="Screenshot 2025-10-27 at 1 14 51 PM" src="https://github.com/user-attachments/assets/eb600047-0b68-4964-9127-a367ed42ee93" />

```sql
select * from CUSTOMERS 
where SALARY<2500
```

**Output:**

<img width="1988" height="862" alt="image" src="https://github.com/user-attachments/assets/d8d1aaa3-0d4c-4d60-9daf-5cf2b57f4d4a" />

**Question 2**
---
<img width="1978" height="828" alt="image" src="https://github.com/user-attachments/assets/2386f048-621c-4de7-82b1-38e3e6baf39e" />

```sql
select * from Medications 
where dosage=(select min(dosage) from Medications);
```

**Output:**

<img width="1974" height="784" alt="image" src="https://github.com/user-attachments/assets/2350a5ec-cfe2-4424-b1a3-9e2730584590" />

**Question 3**
---
<img width="1972" height="946" alt="image" src="https://github.com/user-attachments/assets/693edca9-3891-41ac-af30-08df49767b3c" />

```sql
select * from orders 
where salesman_id in(select salesman_id from orders
WHERE customer_id=3007);
```

**Output:**

<img width="991" height="412" alt="Screenshot 2025-10-27 at 1 18 25 PM" src="https://github.com/user-attachments/assets/df1c0295-10c6-4fb0-87f6-723e3fa0272d" />


**Question 4**
---
<img width="1984" height="1310" alt="image" src="https://github.com/user-attachments/assets/14d0506e-123b-4dc2-b98e-704a92610fa6" />


```sql
select ord_no,purch_amt,ord_date,salesman_id  from orders
where salesman_id = (select salesman_id from salesman
where commission = (select max(commission) from salesman));
```

**Output:**

<img width="1986" height="880" alt="image" src="https://github.com/user-attachments/assets/65a7bdde-0870-4598-ad7d-329651c70640" />


**Question 5**
---
<img width="1970" height="1078" alt="image" src="https://github.com/user-attachments/assets/c5e86eb0-7c82-4f59-ab80-4a772ece1dab" />

```sql
select student_name,grade from GRADES g
where grade=(select min(grade) from GRADES 
where subject=g.subject)
```

**Output:**

<img width="1996" height="820" alt="image" src="https://github.com/user-attachments/assets/cae6b180-eab5-4ebd-9012-9cc503b3dfe5" />


**Question 6**
---
<img width="1982" height="994" alt="image" src="https://github.com/user-attachments/assets/3df0af5c-07c6-47a4-a615-a91abfd3f3de" />


```sql
select * from CUSTOMERS 
where SALARY=1500;
```

**Output:**

<img width="1966" height="656" alt="image" src="https://github.com/user-attachments/assets/8b69af90-5846-4d68-9ae4-b03bc64052cf" />


**Question 7**
---
<img width="1988" height="1126" alt="image" src="https://github.com/user-attachments/assets/eeb856e4-caf6-459f-a94d-41e554e745d5" />

```sql
select commission from salesman 
where salesman_id in (select salesman_id from customer 
where city = 'Paris');
```

**Output:**

<img width="1974" height="676" alt="image" src="https://github.com/user-attachments/assets/e8602af7-3004-4706-8e2b-5842353b5294" />


**Question 8**
---
<img width="1980" height="1088" alt="image" src="https://github.com/user-attachments/assets/997f72b0-89e5-4cbf-869c-67469cba0baf" />


```sql
select * from CUSTOMERS 
where SALARY>4500;
```

**Output:**

<img width="1986" height="822" alt="image" src="https://github.com/user-attachments/assets/d3cf7d74-8e89-4417-9339-e34218ef62db" />


**Question 9**
---
<img width="1994" height="1022" alt="image" src="https://github.com/user-attachments/assets/29d6ee86-0cd9-475c-8544-993df404f903" />


```sql
select * from CUSTOMERS 
where ADDRESS ='Delhi'
```

**Output:**

<img width="1994" height="676" alt="image" src="https://github.com/user-attachments/assets/ec71a90c-0218-4af5-8ed0-b77ccf842c44" />


**Question 10**
---
<img width="1986" height="1282" alt="image" src="https://github.com/user-attachments/assets/3d533c6c-532b-4eb0-b6b8-2a9581b4fd58" />


```sql
select  ord_no, purch_amt, ord_date, customer_id ,salesman_id from ORDERS 
where salesman_id in (select salesman_id froM SALESMAN
WHERE city ='New York')
```

**Output:**

<img width="1986" height="894" alt="image" src="https://github.com/user-attachments/assets/69e51a83-098c-4852-8158-334b8ee7365b" />

**SEB EXAM:**
<img width="2110" height="128" alt="image" src="https://github.com/user-attachments/assets/3d857f8c-04da-4381-bec1-6b555d04d9ec" />

## RESULT
Thus, the SQL queries to implement subqueries and views have been executed successfully.
