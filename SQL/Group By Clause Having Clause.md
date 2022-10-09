# Group By Clause

The GROUP BY Statement in SQL is used to arrange identical data into groups with the help of some functions. i.e if a particular column has same values in different rows then it will arrange these rows in a group.  
  
**Important Points:**  
  
1. GROUP BY clause is used with the SELECT statement.  
2. In the query, GROUP BY clause is placed after the WHERE clause.  
3. In the query, GROUP BY clause is placed before ORDER BY clause if used any.  
  
**Syntax:**  
  
```sql
SELECT column1, function_name(column2)  
FROM table_name  
WHERE condition  
GROUP BY column1, column2  
ORDER BY column1, column2;
```



**Group By single column :** Group By single column means, to place all the rows with same value of only that particular column in one group. Consider the query as shown below:  

**Employee**  
  
![](https://media.geeksforgeeks.org/wp-content/cdn-uploads/20220706103621/1535.png)  
  
  
**Student**  
  
![](https://media.geeksforgeeks.org/wp-content/cdn-uploads/20220706103642/1632.png)

```sql
SELECT NAME, SUM(SALARY) FROM Employee  
GROUP BY NAME;
```


The above query will produce the below output:  
  
![](https://media.geeksforgeeks.org/wp-content/cdn-uploads/20220706103817/1729.png)


**Group By multiple columns:** Group by multiple column is say for example, GROUP BY column1, column2. This means to place all the rows with same values of both the columns column1 and column2 in one group. Consider the below query:  
  
```sql
SELECT SUBJECT, YEAR, Count(*)  
FROM Student  
GROUP BY SUBJECT, YEAR;
```

Output:  

![](https://media.geeksforgeeks.org/wp-content/cdn-uploads/20220706103908/1827.png)


**Student**  
  
![](https://media.geeksforgeeks.org/wp-content/cdn-uploads/20220706103642/1632.png)

As you can see in the above output the students with both same SUBJECT and YEAR are placed in same group. And those whose only SUBJECT is same but not YEAR belongs to different groups. So here we have grouped the table according to two columns or more than one column.



# Having Clause

**HAVING Clause**  
  
We know that WHERE clause is used to place conditions on columns but what if we want to place conditions on groups?  
  
This is where HAVING clause comes into use. We can use HAVING clause to place conditions to decide which group will be the part of final result-set. Also we can not use the aggregate functions like SUM(), COUNT() etc. with WHERE clause. So we have to use HAVING clause if we want to use any of these functions in the conditions.  
  
**Syntax:**  
  
```sql
SELECT column1, function_name(column2)  
FROM table_name  
WHERE condition  
GROUP BY column1, column2  
HAVING condition  
ORDER BY column1, column2;
```


**Example:**

```sql
SELECT NAME, SUM(SALARY) FROM Employee  
GROUP BY NAME  
HAVING SUM(SALARY)>3000;
```

**Employee**  
  
![](https://media.geeksforgeeks.org/wp-content/cdn-uploads/20220706103621/1535.png) 

Output:  
  
![](https://media.geeksforgeeks.org/wp-content/cdn-uploads/20220706104032/1927.png)

