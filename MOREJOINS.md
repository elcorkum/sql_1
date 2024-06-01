CROSS JOIN

A cross join returns all possible combinations of rows of two tables (also called a Cartesian product).
Every row from table1 is aligned with every row in table 2.
If table1 has 5 rows and table2 has 8 we end up with (4*8) 32 rows
```shell
mysql> SELECT employee.EmpID, employee.FName, customer.CustomerID, customer.FName
    -> FROM employee
    -> CROSS JOIN customer;
+-------+---------+------------+--------+
| EmpID | FName   | CustomerID | FName  |
+-------+---------+------------+--------+
|     4 | Bob     |          1 | Mike   |
|     3 | Sal     |          1 | Mike   |
|     2 | Don     |          1 | Mike   |
|     1 | Whitley |          1 | Mike   |
|     4 | Bob     |          2 | Bob    |
|     3 | Sal     |          2 | Bob    |
|     2 | Don     |          2 | Bob    |
|     1 | Whitley |          2 | Bob    |
|     4 | Bob     |          3 | Sophia |
|     3 | Sal     |          3 | Sophia |
|     2 | Don     |          3 | Sophia |
|     1 | Whitley |          3 | Sophia |
|     4 | Bob     |          4 | Rachel |
|     3 | Sal     |          4 | Rachel |
|     2 | Don     |          4 | Rachel |
|     1 | Whitley |          4 | Rachel |
|     4 | Bob     |          5 | Don    |
|     3 | Sal     |          5 | Don    |
|     2 | Don     |          5 | Don    |
|     1 | Whitley |          5 | Don    |
+-------+---------+------------+--------+
```

EQUI JOIN

EQUI JOIN creates a JOIN for equality or matching column(s) values of the relative tables. 
EQUI JOIN also create JOIN by using JOIN with ON and then providing the names of the columns with their relative tables to check equality using equal sign (=).
```shell
mysql> SELECT *
    -> FROM employee, customer
    -> WHERE employee.EmpID = customer.CustomerID
    -> ;
+-------+---------+--------+---------+----------+------------+--------+--------+--------+
| EmpID | FName   | LName  | City    | Phone    | CustomerID | FName  | LName  | Rating |
+-------+---------+--------+---------+----------+------------+--------+--------+--------+
|     1 | Whitley | Ford   | Orange  | 555-1001 |          1 | Mike   | Larson |    3.8 |
|     2 | Don     | Larson | Newark  | 555-3221 |          2 | Bob    | Sydney |    4.8 |
|     3 | Sal     | Maglie | Nutley  | 555-6905 |          3 | Sophia | Ridley |    4.6 |
|     4 | Bob     | Turley | Passaic | 555-8908 |          4 | Rachel | Turley |    1.8 |
+-------+---------+--------+---------+----------+------------+--------+--------+--------+

SELECT employee.*, customer.*
FROM employee
RIGHT OUTER JOIN customer
ON employee.LName = customer.LName
;
```

NON EQUI-JOIN performs a JOIN using comparison operator other than equal(=) sign like >, <, >=, <= with conditions.


SELF JOIN
A self join is a regular join, but the table is joined with itself.
This join would be useful in the case of a table
containing hierarchical data such as employees and managers.
```shell
mysql> SELECT c1.FName, c2.LName
    -> FROM customer AS c1
    -> LEFT OUTER JOIN customer as c2
    -> ON c1.CustomerID = c2.CustomerID
    -> ;
+--------+--------+
| FName  | LName  |
+--------+--------+
| Mike   | Larson |
| Bob    | Sydney |
| Sophia | Ridley |
| Rachel | Turley |
| Don    | Larson |
+--------+--------+
```


NATURAL JOIN
Matches identical columns from both tables(similar names)
```shell
mysql> SELECT employee.*, customer.*
    -> FROM employee
    -> NATURAL LEFT JOIN customer
    -> ;
+-------+---------+--------+---------+----------+------------+-------+--------+--------+
| EmpID | FName   | LName  | City    | Phone    | CustomerID | FName | LName  | Rating |
+-------+---------+--------+---------+----------+------------+-------+--------+--------+
|     1 | Whitley | Ford   | Orange  | 555-1001 |       NULL | NULL  | NULL   |   NULL |
|     2 | Don     | Larson | Newark  | 555-3221 |          5 | Don   | Larson |    2.7 |
|     3 | Sal     | Maglie | Nutley  | 555-6905 |       NULL | NULL  | NULL   |   NULL |
|     4 | Bob     | Turley | Passaic | 555-8908 |       NULL | NULL  | NULL   |   NULL |
+-------+---------+--------+---------+----------+------------+-------+--------+--------+

mysql> SELECT employee.EmpID, employee.FName, customer.CustomerID, customer.FName
    -> FROM employee
    -> NATURAL JOIN customer;
+-------+-------+------------+-------+
| EmpID | FName | CustomerID | FName |
+-------+-------+------------+-------+
|     2 | Don   |          5 | Don   |
+-------+-------+------------+-------+
```

JOIN with USING keyword
```shell
mysql> SELECT c1.FName, c2.LName
    -> FROM customer AS c1
    -> LEFT OUTER JOIN customer as c2
    -> USING(LName)
    -> ;
+--------+--------+
| FName  | LName  |
+--------+--------+
| Mike   | Larson |
| Mike   | Larson |
| Bob    | Sydney |
| Sophia | Ridley |
| Rachel | Turley |
| Don    | Larson |
| Don    | Larson |
+--------+--------+

mysql> SELECT c1.FName, c1.LName, c2.FName, c2.LName
    -> FROM employee AS c1
    -> INNER JOIN customer as c2
    -> USING(LName)
    -> ;
+-------+--------+--------+--------+
| FName | LName  | FName  | LName  |
+-------+--------+--------+--------+
| Don   | Larson | Mike   | Larson |
| Bob   | Turley | Rachel | Turley |
| Don   | Larson | Don    | Larson |
+-------+--------+--------+--------+
```
