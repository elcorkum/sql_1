-- WHERE clause Comparison Operators

-- AND
```shell
SELECT *
FROM sakila.actor
WHERE first_name = 'KENNETH';

SELECT *
FROM sakila.actor
WHERE first_name = 'KENNETH' AND actor_id < 100;
#records returned must fulfill the above criteria

SELECT *
FROM sakila.actor
WHERE first_name = 'KENNETH' AND actor_id < 100 AND last_name = 'TORN';
```


-- OR
```shell
SELECT *
FROM sakila.actor
WHERE first_name = 'KENNETH';

SELECT *
FROM sakila.actor
WHERE first_name = 'KENNETH' OR actor_id < 100;

SELECT *
FROM sakila.actor
WHERE first_name = 'KENNETH' OR actor_id < 100 OR last_name = 'TEMPLE';
#records returned fulfill either one of the above criteria
```


-- NOT
```shell
SELECT actor_id, first_name, last_name
FROM sakila.actor
WHERE NOT actor_id = 5;
#excludes the records whose actor_id equals 5

SELECT actor_id, first_name, last_name
FROM sakila.actor
WHERE actor_id <> 5;
```


-- All together
AND expressions are evaluated first, then OR and then NOT

```shell
SELECT *
FROM sakila.actor
WHERE first_name = 'KENNETH' AND actor_id < 100 OR last_name = 'TEMPLE';

SELECT *
FROM sakila.actor
WHERE first_name = 'KENNETH' OR last_name = 'TEMPLE' AND actor_id < 100;

SELECT *
FROM sakila.actor
WHERE (first_name = 'KENNETH' AND actor_id < 100) OR last_name = 'TEMPLE';

SELECT *
FROM sakila.actor
WHERE first_name = 'KENNETH' AND (actor_id < 100 OR last_name = 'TEMPLE');
#+----------+------------+-----------+---------------------+
#| actor_id | first_name | last_name | last_update         |
#+----------+------------+-----------+---------------------+
#|       69 | KENNETH    | PALTROW   | 2006-02-15 04:34:33 |
#|       88 | KENNETH    | PESCI     | 2006-02-15 04:34:33 |
#|       94 | KENNETH    | TORN      | 2006-02-15 04:34:33 |
#+----------+------------+-----------+---------------------+

SELECT *
FROM sakila.actor
WHERE (first_name = 'KENNETH' OR last_name = 'TEMPLE') AND actor_id < 100;
#+----------+------------+-----------+---------------------+
#| actor_id | first_name | last_name | last_update         |
#+----------+------------+-----------+---------------------+
#|       53 | MENA       | TEMPLE    | 2006-02-15 04:34:33 |
#|       69 | KENNETH    | PALTROW   | 2006-02-15 04:34:33 |
#|       88 | KENNETH    | PESCI     | 2006-02-15 04:34:33 |
#|       94 | KENNETH    | TORN      | 2006-02-15 04:34:33 |
#+----------+------------+-----------+---------------------+

SELECT *
FROM sakila.actor
WHERE first_name = 'KENNETH' OR (last_name = 'TEMPLE' AND actor_id < 100);
#+----------+------------+-----------+---------------------+
#| actor_id | first_name | last_name | last_update         |
#+----------+------------+-----------+---------------------+
#|       53 | MENA       | TEMPLE    | 2006-02-15 04:34:33 |
#|       69 | KENNETH    | PALTROW   | 2006-02-15 04:34:33 |
#|       88 | KENNETH    | PESCI     | 2006-02-15 04:34:33 |
#|       94 | KENNETH    | TORN      | 2006-02-15 04:34:33 |
#|      169 | KENNETH    | HOFFMAN   | 2006-02-15 04:34:33 |
#+----------+------------+-----------+---------------------+

SELECT *
FROM sakila.actor
WHERE NOT (first_name = 'KENNETH' OR (last_name = 'TEMPLE' AND actor_id < 100));
#retruns all the records that do not fit the criteria within the parenthesis

SELECT *
FROM sakila.actor
WHERE first_name = 'KENNETH' OR NOT(last_name = 'TEMPLE' AND actor_id < 100);
#returns any records with the first name Kenneth
#returns any record whose last name is not temple and whose actor_id is not less than 100
#one record is excluded from this result because their last name is Temple and their actor_id is 53 which is less than 100

```