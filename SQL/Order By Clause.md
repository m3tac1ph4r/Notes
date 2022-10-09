# Order By Clause


The ORDER BY statement in SQL is used to sort the fetched data in either ascending or descending according to one or more columns.  
  
By default ORDER BY sorts the data in ascending order.  
We can use the keyword DESC to sort the data in descending order and the keyword ASC to sort in ascending order.  
  
**Sort according to one column:**  
  
To sort in ascending or descending order we can use the keywords ASC or DESC respectively.  
  
**Syntax:**  

```sql
SELECT * FROM table_name ORDER BY column_name ASC|DESC
```


**Sort according to multiple columns:**  
  
To sort in ascending or descending order we can use the keywords ASC or DESC respectively. To sort according to multiple columns, separate the names of columns by the (,) operator.  
  
**Syntax:**  

```sql
SELECT * FROM table_name ORDER BY column1 ASC|DESC , column2 ASC|DESC
```



