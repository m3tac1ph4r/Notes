# Exists Clause

The EXISTS condition in SQL is used to check whether the result of a correlated nested query is empty (contains no tuples) or not. The result of EXISTS is a boolean value True or False. It can be used in a SELECT, UPDATE, INSERT or DELETE statement.

**Syntax:**  

```sql
SELECT column_name(s)  
FROM table_name  
WHERE EXISTS  
(SELECT column_name(s)  
FROM table_name  
WHERE condition);
```


## Examples  
  
Consider the following two relation “Customers” and “Orders”.  
  
![](https://media.geeksforgeeks.org/wp-content/cdn-uploads/20220706105811/2027.png)  
  
![](https://media.geeksforgeeks.org/wp-content/cdn-uploads/20220706105826/2149.png)  
  
**Queries**  
  
**1. Using EXISTS condition with SELECT statement**  
  
To fetch the first and last name of the customers who placed atleast one order.  
  
```sql
SELECT fname, lname  
FROM Customers  
WHERE EXISTS (SELECT *  
FROM Orders  
WHERE Customers.customer_id = Orders.c_id);
```
  
  
Output:  
  
![](https://media.geeksforgeeks.org/wp-content/cdn-uploads/20220706105919/2252.png)  
  
  
**2. Using NOT with EXISTS**  
  
Fetch last and first name of the customers who has not placed any order.  
  
```sql
SELECT lname, fname  
FROM Customer  
WHERE NOT EXISTS (SELECT *  
FROM Orders  
WHERE Customers.customer_id = Orders.c_id);
```
  
  
Output:  
  
![](https://media.geeksforgeeks.org/wp-content/cdn-uploads/20220706105951/2327.png)  
  
  
**3. Using EXISTS condition with DELETE statement**  
  
Delete the record of all the customer from Order Table whose last name is ‘Mehra’.  
  
```sql
DELETE  
FROM Orders  
WHERE EXISTS (SELECT *  
FROM customers  
WHERE Customers.customer_id = Orders.cid  
AND Customers.lname = 'Mehra');  
SELECT * FROM Orders;
```
  
  
Output:  
  
![](https://media.geeksforgeeks.org/wp-content/cdn-uploads/20220706110043/2424.png)  
  
  
**4. Using EXISTS condition with UPDATE statement**  
  
Update the lname as ‘Kumari’ of customer in Customer Table whose customer_id is 401.  
  
```sql
UPDATE Customers  
SET lname = 'Kumari'  
WHERE EXISTS (SELECT *  
FROM Customers  
WHERE customer_id = 401);  
SELECT * FROM Customers;
```
  
  
Output:  
  
![](https://media.geeksforgeeks.org/wp-content/cdn-uploads/20220706110117/2526.png)