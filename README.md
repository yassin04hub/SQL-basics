# Section 1. Querying data
## Select From
 This statement allows you to select one or multiple columns from a certain table.
```sql
SELECT column_name
FROM table;
```
#Section 2. Sorting data
## ORDER BY
This command is used together with the `SELECT` command to select and more importantly sort data in a determined order by default is ascending.
```sql
SELECT * FROM table_name
ORDER BY 
    column_name [ASC|DESC];
```
### ORDER BY clause to sort a result set by an expression example
```sql
SELECT 
	orderNumber
	productCode
	priceEeach*quantityOrdered as total
FROM 
	orderdetails
ORDER BY 
	priceEeach*quantityOrdered DESC;
```
# Section 3. Filtering data
## MySQL WHERE
```sql
SELECT 
	column_name
FROM 
	table_name
WHERE
	search_condition;
```
[![as](https://www.mysqltutorial.org/wp-content/uploads/2021/07/MySQL-Where.svg "as")](https://www.mysqltutorial.org/wp-content/uploads/2021/07/MySQL-Where.svg "as")
```sql
SELECT lastName,firstName,email
FROM
    employees
WHERE
    email like 'a%'
```
```sql
SELECT lastName,firstName,email
FROM
    employees
WHERE
    firstName like 'a%' AND
	lastName like 'b%';
```
```sql
SELECT employeeNumber,lastName,firstName,email
FROM
    employees
WHERE
    employeeNumber between 1000 and 1060
ORDER BY
	employeeNumber,
	lastName,
    firstName;
```
# Section 9. Modifying data in MySQL

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
# Section 12. Working with tables
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
## MySQL ALTER TABLE – Rename a column in a table
```mysql
ALTER TABLE table_name
CHANGE COLUMN column_name column_definition
[ FIRST | AFTER column_name];    
```
##MySQL ALTER TABLE – Drop a column
```mysql
ALTER TABLE table_name
DROP COLUMN column_name;
```
## MySQL ALTER TABLE – Rename table
```mysql
ALTER TABLE table_name
RENAME TO new_name;
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
