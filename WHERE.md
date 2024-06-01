-- WHERE clause Comparison Operators
Where clauses can be used with filtering conditions to narrow down the resulting data from our queries.

-- Equal (=)
```shell
SELECT actor_id, first_name, last_name
FROM sakila.actor
WHERE actor_id = 100;
#queries the sakila.actor table to obtain the three specified columns for the record whose actor_id equals 100
#+----------+------------+-----------+
#| actor_id | first_name | last_name |
#+----------+------------+-----------+
#|      100 | SPENCER    | DEPP      |
#+----------+------------+-----------+
#1 row in set (0.00 sec)

SELECT actor_id, first_name, last_name
FROM sakila.actor
WHERE first_name = 'Nick';
#+----------+------------+-----------+
#| actor_id | first_name | last_name |
#+----------+------------+-----------+
#|        2 | NICK       | WAHLBERG  |
#|       44 | NICK       | STALLONE  |
#|      166 | NICK       | DEGENERES |
#+----------+------------+-----------+
#3 rows in set (0.00 sec)

```
-- Less than (<)
```shell
SELECT actor_id, first_name, last_name
FROM sakila.actor
WHERE actor_id < 100;
#excludes 100 and goes up to 99

SELECT actor_id, first_name, last_name
FROM sakila.actor
WHERE first_name < 'Nick';
#returns the records whose first name is before 'Nick' in the alphabet excluding 'Nick'
```

-- Greater than (>)
```shell
SELECT actor_id, first_name, last_name
FROM sakila.actor
WHERE actor_id > 100;
#excludes 100 and starts at 99

SELECT actor_id, first_name, last_name
FROM sakila.actor
WHERE first_name > 'Nick';
#returns records whose name are after 'Nick' in natural alphabetical ordering excluding 'Nick'
```

-- Less than or Equal to (<=)
```shell
SELECT actor_id, first_name, last_name
FROM sakila.actor
WHERE actor_id <= 100;
#includes 100 and all the actor_id below 100

SELECT actor_id, first_name, last_name
FROM sakila.actor
WHERE first_name <= 'Nick';
#includes 'Nick'

```
-- Greater than or Equal to (>=)
```shell
SELECT actor_id, first_name, last_name
FROM sakila.actor
WHERE actor_id >= 100;
#includes 100 and higher

SELECT actor_id, first_name, last_name
FROM sakila.actor
WHERE first_name >= 'Nick';
#includes first_name "Nick"
```

-- Not equal (<> or !=)
```shell
SELECT actor_id, first_name, last_name
FROM sakila.actor
WHERE actor_id <> 100;
#returns al records whose actor_id is not 100

SELECT actor_id, first_name, last_name
FROM sakila.actor
WHERE first_name != 'Nick';
#returns records whose first_name is anything but 'Nick'
```