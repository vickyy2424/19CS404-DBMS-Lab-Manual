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
Create a table named Customers with the following columns:

CustomerID as INTEGER
Name as TEXT
Email as TEXT
JoinDate as DATETIME
```sql
create table Customers(
CustomerID INTEGER,
Name TEXT,
Email TEXT,
JoinDate DATETIME
);
```

**Output:**

<img width="1368" height="523" alt="Screenshot 2025-10-18 135035" src="https://github.com/user-attachments/assets/e33388b1-606c-4780-827c-921f6b346416" />


**Question 2**
---
Create a table named Bonuses with the following constraints:
BonusID as INTEGER should be the primary key.
EmployeeID as INTEGER should be a foreign key referencing Employees(EmployeeID).
BonusAmount as REAL should be greater than 0.
BonusDate as DATE.
Reason as TEXT should not be NULL.
```sql
create table Bonuses(
BonusID INTEGER  primary key,
EmployeeID INTEGER,
BonusAmount REAL check(BonusAmount>0),
BonusDate DATE,
Reason TEXT NOT NULL,
foreign key (EmployeeID) references Employees(EmployeeID)
);
```
**Output:**


<img width="1367" height="389" alt="Screenshot 2025-10-18 135059" src="https://github.com/user-attachments/assets/2efd3abd-58e1-4293-9745-edacde751ce0" />


**Question 3**
---
Write a SQL query to add birth_date attribute as timestamp (datatype) in the table customer 

Sample table: customer

 customer_id |   cust_name    |    city    | grade | salesman_id 
-------------+----------------+------------+-------+-------------
        3002 | Nick Rimando   | New York   |   100 |        5001
        3007 | Brad Davis     | New York   |   200 |        5001
        3005 | Graham Zusi    | California |   200 |        5002
```sql
alter table customer
add birth_date timestamp
```
**Output:**


<img width="1358" height="476" alt="Screenshot 2025-10-18 135122" src="https://github.com/user-attachments/assets/9c57b2c1-c106-4ab3-a79a-d059d7ce05b6" />


**Question 4**
---
Write a SQL query to add a column named Date_of_birth as Date in the Student_details table.
```sql
alter table Student_details
add column Date_of_birth Date
```

**Output:**

<img width="1345" height="474" alt="Screenshot 2025-10-18 135142" src="https://github.com/user-attachments/assets/5a843009-d912-4565-9551-8603ee22ff9a" />

**Question 5**
---
Insert the below data into the Books table, allowing the Publisher and Year columns to take their default values.

ISBN             Title                 Author
---------------  --------------------  ---------------
978-6655443321   Big Data Analytics    Karen Adams

Note: The Publisher and Year columns will use their default values.
 
 
```sql
insert into Books(ISBN,Title,Author) values('978-6655443321','Big Data Analytics','Karen Adams');
```

**Output:**


<img width="1351" height="440" alt="Screenshot 2025-10-18 135158" src="https://github.com/user-attachments/assets/2bcb2e4e-bee5-42fb-80a6-5e584a69178e" />


**Question 6**
---
Create a table named Attendance with the following constraints:
AttendanceID as INTEGER should be the primary key.
EmployeeID as INTEGER should be a foreign key referencing Employees(EmployeeID).
AttendanceDate as DATE.
Status as TEXT should be one of 'Present', 'Absent', 'Leave'.
```sql
create table Attendance(
AttendanceID INTEGER primary key,
EmployeeID INTEGER,
AttendanceDate  DATE,
Status TEXT check(status IN('Present','Absent','Leave')),
foreign key (EmployeeID) references Employees(EmployeeID));
```

**Output:**


<img width="1227" height="345" alt="image" src="https://github.com/user-attachments/assets/3f737859-e778-41de-a3e7-cd61e439cf5e" />


**Question 7**
---
Create a table named Employees with the following constraints:

EmployeeID should be the primary key.
FirstName and LastName should be NOT NULL.
Email should be unique.
Salary should be greater than 0.
DepartmentID should be a foreign key referencing the Departments table.
```sql
create table Employees(
EmployeeID integer primary key,
FirstName varchar(50) NOT NULL,
LastName varchar(50) NOT NULL,
Email text unique,
Salary check (Salary>0),
DepartmentID integer,
foreign key (DepartmentID) references Departments(DepartmentID)
);
```

**Output:**

<img width="1196" height="412" alt="image" src="https://github.com/user-attachments/assets/e0df255b-75c1-48c6-b438-42c94bc4505d" />


**Question 8**
---
Insert all employees from Former_employees into Employee

Table attributes are EmployeeID, Name, Department, Salary
 
```sql
insert into Employee(EmployeeID,Name,Department,Salary)
select EmployeeID,Name,Department,Salary from Former_employees;
```

**Output:**


<img width="1227" height="382" alt="image" src="https://github.com/user-attachments/assets/4d676538-cd61-4893-942a-113d66c8c53c" />


**Question 9**
---
Create a table named Shipments with the following constraints:
ShipmentID as INTEGER should be the primary key.
ShipmentDate as DATE.
SupplierID as INTEGER should be a foreign key referencing Suppliers(SupplierID).
OrderID as INTEGER should be a foreign key referencing Orders(OrderID).
```sql
create table Shipments(
ShipmentID INTEGER PRIMARY KEY,
ShipmentDate DATE,
SupplierID INTEGER,
OrderID INTEGER,
foreign key (SupplierID) References Suppliers(SupplierID)
foreign key (OrderID) References Orders(OrderID)
);
```

**Output:**


<img width="1361" height="360" alt="Screenshot 2025-10-18 135441" src="https://github.com/user-attachments/assets/9b923933-5344-47ab-adf0-7166a1b4ae71" />

**Question 10**
---
Insert the following students into the Student_details table:
RollNo      Name        Gender      Subject     MARKS
----------  ----------  ----------  ----------  ----------
202            Ella King         F           Chemistry   87
203            James Bond   M          Literature    78


 
```sql
insert into Student_details(RollNo,Name,Gender,Subject,MARKS) values ('202','Ella King','F','Chemistry','87'), ('203','James Bond','M','Literature','78');

```

**Output:**


<img width="1354" height="380" alt="Screenshot 2025-10-18 135456" src="https://github.com/user-attachments/assets/3697bc4a-7a8a-432a-9e99-529487789320" />


## RESULT
Thus, the SQL queries to implement different types of constraints and DDL commands have been executed successfully.
