# Example of Subqueries

### Database :

![[database_used.png]]

### Questions

**1. Find highest salary among**

```sql
select e_name,salary from emp where salary=(select max(salary) from emp);
```


**2. Find Second highest Salary**

```sql
select max(salary) from emp where salary!=(select max(salary) from emp);
```

![[second_highest_salary.png]]

In subquery we find the highest then exclude that using *NOT EQUAL* then in main query find the maximum salary among all others using *MAX(salary)*

**3. Find Second highest Salary with name**

```sql
select e_name,salary from emp where salary=
(select max(salary) from emp where salary!=(select max(salary) from emp));
```
![[second_highest_salary_with_name.png]]