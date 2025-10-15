# Experiment 3: DML Commands

## AIM
To study and implement DML (Data Manipulation Language) commands.

## THEORY

### 1. INSERT INTO
Used to add records into a relation.
These are three type of INSERT INTO queries which are as
A)Inserting a single record
**Syntax (Single Row):**
```sql
INSERT INTO table_name (field_1, field_2, ...) VALUES (value_1, value_2, ...);
```
**Syntax (Multiple Rows):**
```sql
INSERT INTO table_name (field_1, field_2, ...) VALUES
(value_1, value_2, ...),
(value_3, value_4, ...);
```
**Syntax (Insert from another table):**
```sql
INSERT INTO table_name SELECT * FROM other_table WHERE condition;
```
### 2. UPDATE
Used to modify records in a relation.
Syntax:
```sql
UPDATE table_name SET column1 = value1, column2 = value2 WHERE condition;
```
### 3. DELETE
Used to delete records from a relation.
**Syntax (All rows):**
```sql
DELETE FROM table_name;
```
**Syntax (Specific condition):**
```sql
DELETE FROM table_name WHERE condition;
```
### 4. SELECT
Used to retrieve records from a table.
**Syntax:**
```sql
SELECT column1, column2 FROM table_name WHERE condition;
```
**Question 1**
--
<img width="953" height="399" alt="Screenshot 2025-10-15 at 10 17 15 AM" src="https://github.com/user-attachments/assets/6c9ea4fb-f734-4be9-9d30-32ebd3b28eae" />

```sql
update products
set reorder_lvl= 20
where quantity <10 and category='Snacks';

```
**Output:**

<img width="1906" height="1022" alt="image" src="https://github.com/user-attachments/assets/3fa37df3-4ecd-4eb3-934a-c4260aa98325" />

**Question 2**
---
<img width="1898" height="810" alt="image" src="https://github.com/user-attachments/assets/1392fd65-b7a1-42ea-9475-c97ed53a781a" />


```sql
update Suppliers
set address ='58 Lakeview, Magnolia'
where supplier_id=5
```

**Output:**

<img width="1910" height="756" alt="image" src="https://github.com/user-attachments/assets/7a564c28-549d-413c-968b-0d309d611d7c" />


**Question 3**
---
<img width="1894" height="906" alt="image" src="https://github.com/user-attachments/assets/f23fc91c-485b-4fbb-b850-3e5f3fac81f5" />


```sql
update PRODUCTS
set sell_price=round(sell_price *1.1,2)
where supplier_id=6;
```

**Output:**

<img width="1898" height="972" alt="image" src="https://github.com/user-attachments/assets/a7691f5a-55b9-4107-82ba-cee362c5eaf1" />


**Question 4**
---
<img width="954" height="441" alt="Screenshot 2025-10-15 at 10 22 07 AM" src="https://github.com/user-attachments/assets/73241099-95e4-4f4e-85b4-1766609c33c7" />


```sql
update Products 
set category='Household'
where product_name like '%Detergent%';
```

**Output:**

<img width="1880" height="908" alt="image" src="https://github.com/user-attachments/assets/93c2f2cc-4a6c-4f09-8c83-55e23c0359de" />


**Question 5**
---
<img width="1896" height="984" alt="image" src="https://github.com/user-attachments/assets/bb29c1d6-14f4-4073-84ae-679211659efb" />

```sql
update PRODUCTS
set reorder_lvl=reorder_lvl * 0.7
where product_name like '%cream%' and quantity>reorder_lvl;
```

**Output:**

<img width="1904" height="898" alt="image" src="https://github.com/user-attachments/assets/3a0be7d9-8acf-4bc0-835b-363eea98abee" />


**Question 6**
---
<img width="1908" height="894" alt="image" src="https://github.com/user-attachments/assets/9873da33-fb84-4816-8828-6777788af106" />


```sql
delete from Doctors
where specialization is null
```

**Output:**

<img width="1898" height="1566" alt="image" src="https://github.com/user-attachments/assets/4942f78d-2ba5-4a41-b802-7b133b0df0d7" />


**Question 7**
---
<img width="1900" height="1078" alt="image" src="https://github.com/user-attachments/assets/d3645d62-785b-4d5e-ae9c-f38f9e41b895" />


```sql
delete from Customer 
where cust_city like 'L%'
```

**Output:**

<img width="1916" height="1564" alt="image" src="https://github.com/user-attachments/assets/0ec5381a-7d6f-4918-8b22-6063d7566ce9" />


**Question 8**
---
<img width="1900" height="1074" alt="image" src="https://github.com/user-attachments/assets/4c2fdb48-11d8-4064-b45d-9cbe75be0e23" />


```sql
delete from Surgeries
where surgery_id=3 or surgeon_id=4
```

**Output:**

<img width="1906" height="1526" alt="image" src="https://github.com/user-attachments/assets/82b01af0-8c55-4ce7-9d2a-ea479a8d7879" />


**Question 9**
---
<img width="1896" height="1060" alt="image" src="https://github.com/user-attachments/assets/1afe7c76-964f-4e1b-a721-06e84a064a33" />


```sql
delete from Customer 
where CUST_NAME like '______';
```

**Output:**

<img width="1892" height="1274" alt="image" src="https://github.com/user-attachments/assets/6547b5ae-edab-4a3b-a00a-beea877b8822" />


**Question 10**
---
<img width="1900" height="1072" alt="image" src="https://github.com/user-attachments/assets/9c925f0b-ded4-4d8c-9d66-ad9433c9c652" />


```sql
delete from Customer
where GRADE >=2;
```

**Output:**

<img width="1910" height="986" alt="image" src="https://github.com/user-attachments/assets/ff301049-fe4f-4706-975b-9e934b102ceb" />

**SEB:**
<img width="2110" height="132" alt="image" src="https://github.com/user-attachments/assets/8942955e-0da9-40a6-b42a-c9c239451b1a" />

## RESULT
Thus, the SQL queries to implement DML commands have been executed successfully.
