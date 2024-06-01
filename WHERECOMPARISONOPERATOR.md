-- WHERE clause Comparison Operators
Astement performs an operation only WHERE a stated condition is True.

Comparison Predicates
* BETWEEN
* IN / NOT IN
* LIKE / NOT LIKE
* NULL
* ALL, SOME, ANY
* EXISTS
* UNIQUE
* OVERLAPS
* MATCH
* SIMILAR
* DISTINCT


-- IN
```shell
SELECT *
FROM sakila.actor
WHERE first_name IN ('NICK','JOHNNY','JOE','VIVIEN');
#returns the values in the first_name column that contain the names specified in the range
#this predicate is more compact than having multiple OR conditions

SELECT *
FROM sakila.actor
WHERE actor_id IN (1,2,3,4,5,6,7,8);
#rreturns all the records whose actor_id s are contained in the provided range

SELECT *
FROM sakila.actor
WHERE (actor_id = 1 OR
actor_id = 2 OR
actor_id = 3 OR
actor_id = 4 OR
actor_id = 5 OR
actor_id = 6 OR
actor_id = 7 OR
actor_id = 8);
#this is how we would write the scrip above if using OR
```

-- NOT IN
SELECT *
FROM sakila.actor
WHERE actor_id NOT IN (1,2,3,4,5,6,7);
#negates the condition and returns all the values except the ones whose actor_id falls within the specified ragle of values

-- In Subquery
```shell
SELECT *
FROM sakila.actor
WHERE first_name IN ('NICK','JOHNNY','JOE','VIVIEN')
-- 		OR actor_id IN (41, 107, 166)
AND actor_id IN
(SELECT actor_id
FROM sakila.actor
WHERE last_name = 'DEGENERES');
#this is a subquery within a query
```

-- BETWEEN
```shell
SELECT *
FROM sakila.actor
WHERE actor_id >= 10 AND actor_id <= 20;
#returns records whose actor_id is 10 and above but 20 and below

SELECT *
FROM sakila.actor
WHERE actor_id BETWEEN 10 AND 20;
#this returns the same result as the above but is cleaner

SELECT *
FROM sakila.actor
WHERE actor_id BETWEEN 11 AND 19;
#BETWEEN returns the values within the range including the beginning and end of range

SELECT *
FROM sakila.actor
WHERE actor_id NOT BETWEEN 11 AND 19;
#excludes all the records that have an actor_id of 11 to 20;
```


-- LIKE
LIKE is a predicate used to compare two character strings for a partial match
Two wildcard characters are used  to in identifying partial matches   
* %    stands for any string of characters that have zero or more characters
* _    stands for any single character
```shell

SELECT *
FROM sakila.actor
WHERE first_name LIKE 'A%';
#this will find all the records where first_name starts with 'A'

SELECT *
FROM sakila.actor
WHERE first_name LIKE 'AL%';

SELECT *
FROM sakila.actor
WHERE first_name LIKE 'A__E';
#here the pattern being searched for is first_name that begins with 'A' followed by two characters and then 'E' as the fourth character

SELECT *
FROM sakila.actor
WHERE first_name LIKE 'A__E%';
#this is a little similar but only cares about the first four characters following the pattern while the rest of the string can be anything.

SELECT *
FROM sakila.actor
WHERE first_name LIKE 'A%E%';

SELECT *
FROM sakila.actor
WHERE NOT (first_name LIKE 'A%E%' AND first_name LIKE 'A%');
```

-- -----------------------------------------------------
-- NULL
-- -----------------------------------------------------
```shell
SELECT *
FROM sakila.address;

SELECT *
FROM sakila.address
WHERE address2 IS NULL;
#returns only records where the address field is NULL

SELECT *
FROM sakila.address
WHERE address2 IS NOT NULL;
#returns all the records where the address field have a value that is NOT NULL
```



-- ORDER BY clause
Used to display the output table of a query in either ascending or descending order
ORDER BY sorts individual rows
Null values always appear first where a sequence is declared

```shell


SELECT *
FROM sakila.address
ORDER BY district;

SELECT *
FROM sakila.address
ORDER BY district DESC;

SELECT *
FROM sakila.address
ORDER BY district, postal_code DESC;
#displays output in order or district alphabetically and then orders records with the same value in the district field by postal code in descending order

SELECT actor_id, CONCAT(first_name, ' ', last_name) AS FullName
FROM sakila.actor
ORDER BY CONCAT(first_name, ' ', last_name);
#displays the output with the rows ordered according to the alphabetical order of the full name

SELECT actor_id, CONCAT(first_name, ' ', last_name) AS FullName
FROM sakila.actor
ORDER BY FullName;
#displays the output with the rows ordered according to the alphabetical order of the full name

SELECT actor_id, CONCAT(first_name, ' ', last_name) AS FullName
FROM sakila.actor
ORDER BY 1;
#this specifies that we are ordering the display by the values in the first column which is actor_id for this query
#however, this can be a little ambiguous and it is recommended to use a complete expression(ORDER BY CONCAT(first_name, ' ', last_name);) or the alias(ORDER BY FullName;)
```



-- Limit Keyword
```shell

SELECT *
FROM sakila.actor
ORDER BY actor_id;

SELECT *
FROM sakila.actor
ORDER BY actor_id
LIMIT 12;
#gets only the first twelve records that fit the criteria

SELECT *
FROM sakila.actor
ORDER BY actor_id
LIMIT 25, 5;
#limits output to records starting at the next actor_id from 25 and gets just the five records excluding (26, 27, 28, 29, 30)
```
