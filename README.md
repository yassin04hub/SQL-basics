# Section 1. Querying data
## Select From
 This statement allows you to select one or multiple columns from a certain table.
```sql
SELECT column_name
FROM table;

SELECT 
    lastname
FROM 
    employees;

+-----------+
| lastName  |
+-----------+
| Murphy    |
| Patterson |
| Firrelli  |
| Patterson |
| Bondur    |
| Bow       |
| Jennings  |
...

SELECT 
    lastName, 
    firstName, 
    jobTitle
FROM
    employees;


+-----------+-----------+----------------------+
| lastname  | firstname | jobtitle             |
+-----------+-----------+----------------------+
| Murphy    | Diane     | President            |
| Patterson | Mary      | VP Sales             |
| Firrelli  | Jeff      | VP Marketing         |
| Patterson | William   | Sales Manager (APAC) |
| Bondur    | Gerard    | Sale Manager (EMEA)  |
...

SELECT * 
FROM employees;
Returns all the columns of the table
```
## SQL Insert
```sql
INSERT INTO table(c1,c2,...)
VALUES (v1,v2,...);
```
However it's also possible to use this command without specifying the names of the columns
```sql
INSERT INTO table
VALUES (v1,v2,...);
```
#### - MySQL INSERT – Inserting multiple rows example
```sql
INSERT INTO table
VALUES 
    (v1,v2,...),
    (v1,v2,...),
    (v1,v2,...);
```
## MySQL INSERT INTO SELECT
This statement is very useful when wanting to fill a column by using existent data.
```sql
INSERT INTO table_name(column_list)
SELECT 
   select_list 
FROM 
   another_table
WHERE
   condition;
```
## UPDATE
This statement allows you to commit changes to the existent data of a table.
```sql
UPDATE table_name 
SET 
    column_name1 = expr1,
    column_name2 = expr2,
    ...
[WHERE
    condition];
```
WHERE modifier is optional as shown by the brackets [] but without it the changes are going to be applied to all the rows of the table while if you use WHERE you can specify a filter to select a certain row.
```sql
SELECT 
    firstname, 
    lastname, 
    email
FROM
    employees
WHERE
    employeeNumber = 1056;
```
## MySQL CREATE USER
### How To Create User Accounts Using MySQL CREATE USER Statement
```sql
CREATE USER account_name
IDENTIFIED BY 'password';
```
```sql
account_name=> username@hostname
```
## MySQL GRANT
When you create a user using the CREATE USER statement this user has no privileges and so he cannot do anything like accessing or editing data.
```sql
GRANT privilege [,privilege],.. 
ON privilege level 
TO account_name;
```
```sql
GRANT SELECT 
ON database_name
TO user@localhost;
```
**MYSQL Privileges**
```sql
*.*  
```
**Database Privileges**
```sql
databasename.* 
```
**Table Priviliges**
```sql
database_name.table_name 
```
**Column privileges**
```sql
GRANT 
   SELECT (column_name, ...), 
ON database_name
TO user@localhost;
```
**ALL** used to grant all privileges
```sql
ALL [PRIVILEGES]
```
## MYSQL ROLES
### Creating Roles
```mysql
CREATE ROLE 
    crm_dev, 
    crm_read, 
    crm_write;
```
If you omit the host part it defeaults to any host.
```mysql
role_name@host_name
```
### Granting privileges to roles
```mysql
GRANT SELECT 
ON crm.* 
TO crm_read;
```
### Assigning roles to user accounts
```mysql
GRANT crm_read 
TO crm_read1@localhost;
```
To show the assigned role we use the `SHOW GRANTS` statement
```mysql
SHOW GRANTS FOR crm_dev1@localhost;
```
To see the actual privileges acquired thanks to the role by using the `USING` modifier.
```mysql
SHOW GRANTS 
FOR crm_write1@localhost 
USING crm_write;
```
## MySQL ALTER TABLE- Create Tables
1) Add a column to a table  use the `ALTER TABLE ADD `statement
```mysql
ALTER TABLE table_name
ADD
    new_column_name column_definition
    [FIRST | AFTER column_name]
```
`FIRST AFTER` allows you to specify the position of the column.

2) Add multiple columns to a table
```mysql
ALTER TABLE table_name
    ADD new_column_name column_definition
    [FIRST | AFTER column_name],
    ADD new_column_name column_definition
    [FIRST | AFTER column_name],
    ...;
```
## MySQL ALTER TABLE – Modify columns
### 1) Modify a column
```mysql
ALTER TABLE table_name
MODIFY column_name column_definition
[ FIRST | AFTER column_name];    

```
