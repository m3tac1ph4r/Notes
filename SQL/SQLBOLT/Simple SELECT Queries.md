#  SQL Review: Simple SELECT Queries


**1. List all the Canadian cities and their populations**

```sql
SELECT City,Population FROM north_american_cities WHERE COUNTRY="Canada";
```

**2. Order all the cities in the United States by their latitude from north to south**

```sql
SELECT City FROM north_american_cities WHERE COUNTRY="United States"
ORDER BY LATITUDE DESC;
```

**3. List the two largest cities in Mexico (by population) **

```sql
SELECT City FROM north_american_cities WHERE Country="Mexico" 
ORDER BY Population DESC LIMIT 2;
```

**4. List the third and fourth largest cities (by population) in the United States and their population**

```sql
SELECT City FROM north_american_cities WHERE Country="United States" 4
ORDER BY Population DESC LIMIT 2 OFFSET 2;
```


### Link
https://sqlbolt.com/lesson/select_queries_review