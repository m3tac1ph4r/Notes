# BETWEEN and IN Operator

## BETWEEN 
  
The SQL BETWEEN condition allows you to easily test if an expression is within a range of values (inclusive). The values can be text, date, or numbers. It can be used in a SELECT, INSERT, UPDATE, or DELETE statement. The SQL BETWEEN Condition will return the records where expression is within the range of value1 and value2.  
  
**Syntax:**  
  
```sql
SELECT column_name(s)  
FROM table_name  
WHERE column_name BETWEEN value1 AND value2;
```


  
**Examples:**  
  
Consider the following Employee Table,  
  
![](https://media.geeksforgeeks.org/wp-content/cdn-uploads/20220705225024/1266.png)  
  
**Queries**  
  
**Using BETWEEN with Numeric Values:**  
  
List all the Employee Fname, Lname who is having salary between 30000 and 45000.  
  
```sql
SELECT Fname, Lname  
FROM Employee  
WHERE Salary  
BETWEEN 30000 AND 45000;
```
  
  
Output:  
  
![](https://media.geeksforgeeks.org/wp-content/cdn-uploads/20220705225110/1342.png)  
  
  
**Using BETWEEN with Date Values:**  
  
Find all the Employee having Date of Birth Between 01-01-1985 and 12-12-1990.  
  
```sql
SELECT Fname, Lname  
FROM Employee  
where DOB  
BETWEEN '1985-01-01' AND '1990-12-30';
```
  
  
Output:  
  
![](https://media.geeksforgeeks.org/wp-content/cdn-uploads/20220705225138/1439.png)  
  
  
**Using NOT operator with BETWEEN**  
  
Find all the Employee name whose salary is not in the range of 30000 and 45000.  
  
```sql
SELECT Fname, Lname  
FROM Employee  
WHERE Salary  
NOT BETWEEN 30000 AND 45000;
```

  
  
Output:  
  
![](https://media.geeksforgeeks.org/wp-content/cdn-uploads/20220705225210/1534.png)



## IN :
  
IN operator allows you to easily test if the expression matches any value in the list of values. It is used to remove the need of multiple OR condition in SELECT, INSERT, UPDATE or DELETE. You can also use NOT IN to exclude the rows in your list. We should note that any kind of duplicate entry will be retained.  
  
**Syntax:**  

```sql
SELECT column_name(s)  
FROM table_name  
WHERE column_name IN (list_of_values);
```
  
  
**Queries**  
  
Find the Fname, Lname of the Employees who have Salary equal to 30000, 40000 or 25000.  
  
```sql
SELECT Fname, Lname  
FROM Employee  
WHERE Salary IN (30000, 40000, 25000);
```
  
  
Output:  
  
![](https://media.geeksforgeeks.org/wp-content/cdn-uploads/20220705225320/1631.png)  
  
  
Find the Fname, Lname of all the Employee who have Salary not equal to 25000 or 30000.  

```sql
SELECT Fname, Lname  
FROM Employee  
WHERE Salary NOT IN (25000, 30000);
```
  
  
Output:  
  
![](https://media.geeksforgeeks.org/wp-content/cdn-uploads/20220705225346/1728.png)  
  
  
**ALIASES**  
  
Aliases are the temporary names given to table or column for the purpose of a particular SQL query. It is used when name of column or table is used other than their original names, but the modified name is only temporary.  
  
1. Aliases are created to make table or column names more readable.  
2. The renaming is just a temporary change and table name does not change in the original database.  
3. Aliases are useful when table or column names are big or not very readable.  
4. These are preferred when there are more than one table involved in a query.  
  
**Basic Syntax:**  
  
**For column alias:**  
  
```sql
SELECT column as alias_name FROM table_name;
```

**For table alias:**  
  
```sql
SELECT column FROM table_name as alias_name;
```
