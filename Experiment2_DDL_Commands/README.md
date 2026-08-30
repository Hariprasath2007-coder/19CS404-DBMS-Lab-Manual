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
Create a table named Invoices with the following constraints:

InvoiceID as INTEGER should be the primary key.
InvoiceDate as DATE.
DueDate as DATE should be greater than the InvoiceDate.
Amount as REAL should be greater than 0.

```sql
create TABLE Invoices(InvoiceID int primary key,InvoiceDate date,DueDate date check (DueDate>InvoiceDate),Amount real check(Amount>0));
```

**Output:**

<img width="1201" height="455" alt="image" src="https://github.com/user-attachments/assets/664c36e3-224a-4931-8c43-4c1064e8c34f" />


**Question 2**
---
Create a table named Members with the following columns:

MemberID as INTEGER
MemberName as TEXT
JoinDate as DATE

```sql
create table Members(MemberID INTEGER,MemberName TEXT,JoinDate DATE);
```

**Output:**

<img width="1238" height="579" alt="image" src="https://github.com/user-attachments/assets/a1654902-42bf-498e-8f1f-b3643b9b532e" />


**Question 3**
---
Insert the below data into the Student_details table, allowing the Subject and MARKS columns to take their default values.

RollNo      Name          Gender      
----------  ------------  ----------  
204         Samuel Black  M          

Note: The Subject and MARKS columns will use their default values.

```sql
INSERT INTO Student_details(RollNo,Name,Gender) VALUES (204,"Samuel Black","M");
```

**Output:**

<img width="1193" height="497" alt="image" src="https://github.com/user-attachments/assets/85d43be2-5ae8-45ff-93e6-bf4bf4e1e4f9" />


**Question 4**
---
Write a SQL Query  to add attribute ISBN as varchar(30) and domain_dept as varchar(30) in the table 'books'


```sql
ALTER TABLE books ADD column ISBN varchar(30);
ALTER TABLE books ADD domain_dept varchar(30);
 
```

**Output:**

<img width="1204" height="572" alt="image" src="https://github.com/user-attachments/assets/65087e07-8e82-4bf7-bdf9-b63f59307647" />


**Question 5**
---
Create a new table named contacts with the following specifications:
contact_id as INTEGER and primary key.
first_name as TEXT and not NULL.
last_name as TEXT and not NULL.
email as TEXT.
phone as TEXT and not NULL with a check constraint to ensure the length of phone is at least 10 characters.

```sql
CREATE TABLE contacts(contact_id INTEGER PRIMARY KEY,first_name TEXT NOT NULL,last_name TEXT NOT NULL,email TEXT,phone TEXT NOT NULL check(LENGTH(phone)>=10));
```

**Output:**

<img width="1225" height="517" alt="image" src="https://github.com/user-attachments/assets/1930a26d-1e05-4e12-ae2b-f3355cc863dd" />


**Question 6**
---
Write a SQL query to Add a new column State as text in the Student_details table.

Sample table: Student_details

 cid              name             type   notnull     dflt_value  pk
---------------  ---------------  -----  ----------  ----------  ----------
0                RollNo           int    0                       1
1                Name             VARCH  1                       0
2                Gender           TEXT   1                       0
3                Subject          VARCH  0                       0
4                MARKS            INT (  0                       0


```sql
ALTER TABLE Student_details ADD COLUMN State TEXT;
```

**Output:**

<img width="1266" height="537" alt="image" src="https://github.com/user-attachments/assets/77c1c8ad-4d40-4083-8e69-8a0104623877" />


**Question 7**
---
Create a table named Shipments with the following constraints:
ShipmentID as INTEGER should be the primary key.
ShipmentDate as DATE.
SupplierID as INTEGER should be a foreign key referencing Suppliers(SupplierID).
OrderID as INTEGER should be a foreign key referencing Orders(OrderID).

```sql
CREATE TABLE Shipments(ShipmentID INTEGER PRIMARY KEY,ShipmentDate DATE,SupplierID INTEGER REFERENCES Suppliers(SupplierID),OrderID INTEGER REFERENCES Orders(OrderID));
```

**Output:**

<img width="1185" height="400" alt="image" src="https://github.com/user-attachments/assets/2c6a5602-db91-4d87-8abf-2e52d7027e62" />


**Question 8**
---
Insert all books from Out_of_print_books into Books

Table attributes are ISBN, Title, Author, Publisher, YearPublished

```sql
INSERT INTO Books(ISBN, Title, Author, Publisher, YearPublished) select * from Out_of_print_books;
```

**Output:**

<img width="1177" height="436" alt="image" src="https://github.com/user-attachments/assets/71f8bc18-1709-474a-9405-d531dc7c1603" />


**Question 9**
---
Insert the following customers into the Customers table:

CustomerID  Name         Address     City        ZipCode
----------  -----------  ----------  ----------  ----------
302         Laura Croft  456 Elm St  Seattle     98101
303         Bruce Wayne  789 Oak St  Gotham      10001

```sql
INSERT INTO Customers(CustomerID,Name,Address, City, ZipCode) values (302,"Laura Croft","456 Elm St","Seattle",98101);
INSERT INTO Customers(CustomerID,Name,Address, City, ZipCode) values (303,"Bruce Wayne","789 Oak St","Gotham",10001); 
```

**Output:**

<img width="1190" height="536" alt="image" src="https://github.com/user-attachments/assets/346597bc-7bcf-4d2e-8983-8c33fe7dd809" />


**Question 10**
---
Create a table named ProjectAssignments with the following constraints:
AssignmentID as INTEGER should be the primary key.
EmployeeID as INTEGER should be a foreign key referencing Employees(EmployeeID).
ProjectID as INTEGER should be a foreign key referencing Projects(ProjectID).
AssignmentDate as DATE should be NOT NULL.

```sql
CREATE TABLE ProjectAssignments(AssignmentID INTEGER PRIMARY KEY,EmployeeID INTEGER REFERENCES Employees(EmployeeID),ProjectID INTEGER REFERENCES Projects(ProjectID),AssignmentDate DATE NOT NULL);
```

**Output:**

<img width="1167" height="444" alt="image" src="https://github.com/user-attachments/assets/ab20d3f1-72c8-4ce5-bc7e-05ab2b0e4e68" />



## RESULT
Thus, the SQL queries to implement different types of constraints and DDL commands have been executed successfully.
