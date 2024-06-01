A subquery is a nested query where the results of one query can be used in another query via a relational operator or aggregate function.

A subquery must be enclosed within parentheses
A subquery can have only one column in the SELECT clause if used in WHERE clause
An ORDER BY clause is not allowed in a subquery
Subqueries can be nested within other subqueries.

Subqueries are used in WHERE, HAVING, FROM and SELECT clauses.

```shell
SELECT * 
FROM t1 
WHERE column1 = (SELECT column1 FROM t2);
```


When to use subqueries vs when to use joins

Joins
Joins can include any of the columns withins the SELECT clause.
In subqueries, we are limited to querying one column within the subquery
Joins are easy to read

Subqueries
Subqueries pass aggregate values to the main query
Simplifies log and complex queries


Correlated subquery
This is a subquery that is executed once for each row.
It returns results based on the column of the main query


```shell
/*
Problem Statement:
Find all the customer's payments which are over their average payment.
*/

SELECT  payment_id, cust.first_name, cust.last_name, amount
FROM payment pt
INNER JOIN customer cust ON cust.customer_id = pt.customer_id
WHERE amount <
		(	SELECT AVG(amount)
			FROM payment pt1
			WHERE pt1.customer_id = pt.customer_id)
ORDER BY cust.customer_id;





SELECT  cust.first_name, cust.last_name, COUNT(payment_id) CountofPayment
FROM payment pt
INNER JOIN customer cust ON cust.customer_id = pt.customer_id
WHERE amount >
		(	SELECT AVG(amount)
			FROM payment pt1
			WHERE pt1.customer_id = pt.customer_id)
GROUP BY cust.first_name, cust.last_name
ORDER BY cust.customer_id;

```


```shell
mysql> SELECT t1.*
    -> FROM employee t1
    -> WHERE t1.LName NOT IN
    -> (SELECT t2.LName FROM customer t2);
+-------+---------+--------+--------+----------+
| EmpID | FName   | LName  | City   | Phone    |
+-------+---------+--------+--------+----------+
|     1 | Whitley | Ford   | Orange | 555-1001 |
|     3 | Sal     | Maglie | Nutley | 555-6905 |
+-------+---------+--------+--------+----------+

THESE TWO QUERIES OUTPUT THE SAME RESULT. THE ONE ABOVE IS A SUBQUERY WHILE THE ONE BELOW USES JOIN
THESE TWO QUESRIES RETUN ROWS FROM table1 WHERE THER IN NO OVERLAP WITH table2


mysql> SELECT t1.*
    -> FROM employee t1
    -> LEFT OUTER JOIN customer t2
    -> ON t1.LName = t2.LName
    -> WHERE t2.LName IS NULL
    -> ;
+-------+---------+--------+--------+----------+
| EmpID | FName   | LName  | City   | Phone    |
+-------+---------+--------+--------+----------+
|     1 | Whitley | Ford   | Orange | 555-1001 |
|     3 | Sal     | Maglie | Nutley | 555-6905 |
+-------+---------+--------+--------+----------+
```

