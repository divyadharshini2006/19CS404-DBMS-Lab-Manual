# Experiment 2: DDL Commands

## AIM
To study and implement DDL commands and different types of constraints.

## THEORY

### 1. CREATE
Used to create a new relation (table).

**Syntax:**
```sql
CREATE TABLE (
  field_1 data_type(size),
  field_2 data_type(size),
  ...
);
```
### 2. ALTER
Used to add, modify, drop, or rename fields in an existing relation.
(a) ADD
```sql
ALTER TABLE std ADD (Address CHAR(10));
```
(b) MODIFY
```sql
ALTER TABLE relation_name MODIFY (field_1 new_data_type(size));
```
(c) DROP
```sql
ALTER TABLE relation_name DROP COLUMN field_name;
```
(d) RENAME
```sql
ALTER TABLE relation_name RENAME COLUMN old_field_name TO new_field_name;
```
### 3. DROP TABLE
Used to permanently delete the structure and data of a table.
```sql
DROP TABLE relation_name;
```
### 4. RENAME
Used to rename an existing database object.
```sql
RENAME TABLE old_relation_name TO new_relation_name;
```
### CONSTRAINTS
Constraints are used to specify rules for the data in a table. If there is any violation between the constraint and the data action, the action is aborted by the constraint. It can be specified when the table is created (using CREATE TABLE) or after it is created (using ALTER TABLE).
### 1. NOT NULL
When a column is defined as NOT NULL, it becomes mandatory to enter a value in that column.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) NOT NULL
);
```
### 2. UNIQUE
Ensures that values in a column are unique.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) UNIQUE
);
```
### 3. CHECK
Specifies a condition that each row must satisfy.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) CHECK (logical_expression)
);
```
### 4. PRIMARY KEY
Used to uniquely identify each record in a table.
Properties:
Must contain unique values.
Cannot be null.
Should contain minimal fields.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) PRIMARY KEY
);
```
### 5. FOREIGN KEY
Used to reference the primary key of another table.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size),
  FOREIGN KEY (column_name) REFERENCES other_table(column)
);
```
### 6. DEFAULT
Used to insert a default value into a column if no value is specified.

Syntax:
```sql
CREATE TABLE Table_Name (
  col_name1 data_type,
  col_name2 data_type,
  col_name3 data_type DEFAULT 'default_value'
);
```

**Question 1**
--
<img width="1910" height="648" alt="image" src="https://github.com/user-attachments/assets/74d2fef8-15cb-4727-8154-f350a4f43b78" />

```sql
insert into Customers(CustomerID,Name,Address,City,ZipCode)
values(302,'Laura Croft','456 Elm St','Seattle',98101),(303,'Bruce Wayne','789 Oak St','Gotham',10001);
```

**Output:**

<img width="941" height="354" alt="Screenshot 2025-09-29 at 1 41 33 PM" src="https://github.com/user-attachments/assets/e7771924-85d9-4a16-a6a6-c452f2bf5389" />

**Question 2**
---
<img width="1898" height="738" alt="image" src="https://github.com/user-attachments/assets/2f47494c-7adb-4afc-9dd7-28803488fbb2" />

```sql
create table Products(
ProductID INTEGER,
ProductName TEXT,
Price REAL,
Stock INTEGER
);
```

**Output:**

<img width="948" height="299" alt="Screenshot 2025-09-29 at 1 44 15 PM" src="https://github.com/user-attachments/assets/633a43da-7b53-40f0-902f-68655c85676d" />

**Question 3**
---
<img width="1886" height="962" alt="image" src="https://github.com/user-attachments/assets/f46026d8-870b-4012-b665-cf2d71e06c76" />

```sql
alter table Student_details add column mobilenumb number;
```

**Output:**

<img width="1902" height="690" alt="image" src="https://github.com/user-attachments/assets/b48455bd-0379-4461-a721-d0a2e5d7454c" />


**Question 4**
---
<img width="1896" height="680" alt="image" src="https://github.com/user-attachments/assets/eae0efb2-6d36-4a9b-99ec-30084b8ce37c" />


```sql
create table contacts(
contact_id INTEGER primary key,
first_name TEXT NOT NULL,
last_name TEXT NOT NULL,
email TEXT,
phone text not null check(length(phone)>=10)
);

```

**Output:**

<img width="1916" height="630" alt="image" src="https://github.com/user-attachments/assets/96211c0e-d6f7-4d95-95a6-bc591bc1fb98" />


**Question 5**
---
<img width="1896" height="560" alt="image" src="https://github.com/user-attachments/assets/04a8fd50-c667-4179-ad95-1995a5615143" />


```sql
alter table customers add column email TEXT;
```

**Output:**

<img width="1902" height="578" alt="image" src="https://github.com/user-attachments/assets/23ae6cbb-97ef-43c1-8d48-d70f8b44a07e" />


**Question 6**
---
<img width="1900" height="564" alt="image" src="https://github.com/user-attachments/assets/6b42dbee-996d-4448-9a1a-a295c5206e24" />


```sql
create table Products(
ProductID int primary key,
ProductName not null,
Price real check(Price>0),
Stock int check(Stock>=0)
);
```

**Output:**

<img width="1908" height="568" alt="image" src="https://github.com/user-attachments/assets/ae87096b-3608-424e-bf34-8ebd47e0a507" />


**Question 7**
---
<img width="1898" height="590" alt="image" src="https://github.com/user-attachments/assets/cc451616-526b-46ca-95ca-16f44e4fade6" />


```sql
insert into Books(ISBN,Title,Author,Publisher,YearPublished)
select ISBN,Title,Author,Publisher,YearPublished 
from Out_of_print_books
```

**Output:**

<img width="1906" height="584" alt="image" src="https://github.com/user-attachments/assets/31fac14f-4472-4a09-9737-3b5361897576" />

**Question 8**
---
<img width="946" height="319" alt="Screenshot 2025-09-29 at 1 51 00 PM" src="https://github.com/user-attachments/assets/a6d99e42-f393-41a9-ae76-fe9b37fc3763" />


```sql
insert into Employee(EmployeeID,Name,Position)
values(4,'Emily White','Analyst')
```

**Output:**

<img width="1900" height="642" alt="image" src="https://github.com/user-attachments/assets/8395f004-d485-4d8f-a0c3-73bfc74c3055" />


**Question 9**
---
<img width="1900" height="552" alt="image" src="https://github.com/user-attachments/assets/6f8db62e-971d-459b-a353-31008e89248e" />


```sql
create table ProjectAssignments(
AssignmentID int primary key,
EmployeeID INT,
ProjectID INT,
AssignmentDate Date not null,
foreign key (EmployeeID) references Employees(EmployeeID)
foreign key (ProjectID) references Projects(ProjectID)
); 
```

**Output:**

<img width="957" height="283" alt="Screenshot 2025-09-29 at 1 53 09 PM" src="https://github.com/user-attachments/assets/a209319d-4959-43a3-8b7b-7d36d11af570" />


**Question 10**
---
<img width="1894" height="772" alt="image" src="https://github.com/user-attachments/assets/d4f83ba2-81f7-496a-b84d-1f50d5a848ef" />

```sql
create table item(
item_id text primary key,
item_desc text not null,
rate int not null,
icom_id text check(length(icom_id)=4),
foreign key (icom_id) references company(com_id)
on update cascade
on delete cascade
);
```

**Output:**

<img width="1906" height="684" alt="image" src="https://github.com/user-attachments/assets/5c3e0427-2d3a-4782-85db-a24a9b91b16b" />

**SEB EXAM:**

<img width="2092" height="130" alt="image" src="https://github.com/user-attachments/assets/ab70fc49-6d42-4b06-875c-87fe126eb2c6" />

## RESULT
Thus, the SQL queries to implement different types of constraints and DDL commands have been executed successfully.
