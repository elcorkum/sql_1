Understanding Data Types

String ---char, varchar, binary, varbinary, blob, enum, set, text

*Can hold plain text and binary data


Numeric ---bit, int, float, double, decimal
Can hold integers (positive and negative), as well as fixed-point ofr floating point numbers (fractions of whole numbers)

Date and Time ---date, time, datetime, timestamp, year
Can hold date, time, combination of dates and times timestamps and years.


Designing and Creating a Database

```shell
CREATE DATABASE day_one;
#the script above creates a database called "day_one"

Query OK, 1 row affected (0.01 sec)


#To see the columns in a table:
mysql> SHOW columns FROM promotions;
+----------+-------------+------+-----+---------+-------+
| Field    | Type        | Null | Key | Default | Extra |
+----------+-------------+------+-----+---------+-------+
| id       | int         | YES  |     | NULL    |       |
| name     | varchar(50) | YES  |     | NULL    |       |
| category | varchar(15) | YES  |     | NULL    |       |
+----------+-------------+------+-----+---------+-------+
3 rows in set (0.01 sec)

mysql> DESC promotions
    -> ;
+----------+-------------+------+-----+---------+-------+
| Field    | Type        | Null | Key | Default | Extra |
+----------+-------------+------+-----+---------+-------+
| id       | int         | YES  |     | NULL    |       |
| name     | varchar(50) | YES  |     | NULL    |       |
| category | varchar(15) | YES  |     | NULL    |       |
+----------+-------------+------+-----+---------+-------+
3 rows in set (0.00 sec)



Data retrieval 
```shell
SELECT 'MyFirstValue' AS SomeValue;
#AS SomeValue provides an alias for the data that is returned by this query

SELECT 1+1 AS TWO;
#this query returns the number two with the column name TWO

SELECT NOW();
#+---------------------+
#| NOW()               |
#+---------------------+
#| 2024-05-29 21:49:19 |
#+---------------------+
#1 row in set (0.00 sec)   (RETURNS THE CURRENT DATE AND TIME)

SELECT CURDATE();
#+------------+
#| CURDATE()  |
#+------------+
#| 2024-05-29 |
#+------------+
#1 row in set (0.00 sec)   (RETURNS CURRENT DATE)
SELECT CURTIME();
#+-----------+
#| CURTIME() |
#+-----------+
#| 21:52:40  |
#+-----------+
#1 row in set (0.00 sec)  (RETURNS CURRENT TIME)

SELECT PI();
#+----------+
#| PI()     |
#+----------+
#| 3.141593 |
#+----------+
#1 row in set (0.00 sec)   (RETURNS PI)

SELECT MOD(45,7);
#+------------+
#| MOD(45, 7) |
#+------------+
#|          3 |
#+------------+
#1 row in set (0.00 sec)   (RETURNS THE REMAINDER AFTER DIVIDING 45 BY 7)


SELECT SQRT(25);
#+----------+
#| SQRT(25) |
#+----------+
#|        5 |
#+----------+
#1 row in set (0.00 sec)  (RETURNS THE SQUARE ROOT OF 25)
```

-- Retrieve all the data from table
```shell
#WHEN WE USE THE * SYMBOL WITH SELECT KEYWORD, WE ARE ESSENTIALLY RETRIEVING ALL THE DATA FROM A PARTICULAR TABLE

SELECT *
FROM sakila.actor;
# THIS SCRIPT RETURNS ALL THE DATA IN THE sakila.actor TABLE

SELECT *
FROM sakila.city;
# THIS SCRIPT RETURNS ALL THE DATA IN THE sakila.city TABLE

USE sakila;
SELECT *
FROM city;
#THE KEYWORD USE HELPS US TO ENTER THAT PARTICULAR DATABASE AND IS USEFUL WHEN WE WANT TO PERFORM SEVERAL OPERATIONS INSIDE OF THAT DATABASE

```

-- Retrieve all the data ordered by single column

```shell
SELECT *
FROM sakila.actor;
#RETURNING ALL THE DATA IN ALL THE COLUMNS

SELECT *
FROM sakila.actor
ORDER BY first_name;
#RETURNS DATA FROM THE ENTIRE TABLE BUT WITH THE FIRST NAMES ORDER ALPHABETICALLY (A - Z)

SELECT *
FROM sakila.actor
ORDER BY last_name;
#RETURNS DATA FROM THE ENTIRE TABLE BUT WITH THE LAST NAMES ORDER ALPHABETICALLY (A - Z)

SELECT *
FROM sakila.actor
ORDER BY first_name DESC;
#RETURNS DATA FROM THE ENTIRE TABLE BUT WITH THE FIRST NAMES ORDERED DESCENDING ALPHABETICALLY (Z -A)

SELECT *
FROM sakila.actor
ORDER BY last_name DESC;
#RETURNS DATA FROM THE ENTIRE TABLE BUT WITH THE LAST NAMES ORDERED DESCENDING ALPHABETICALLY (Z -A)
```



-- Retrieve selected columns from table

```shell
SELECT *
FROM sakila.actor;
#returns all the columns in the entire table

SELECT first_name, last_name
FROM sakila.actor;
#narrows down the result to return just two columns  1.first_name,   2.last_name

SELECT first_name, last_name
FROM sakila.actor
ORDER BY first_name DESC;
#narrows down the result to return just two columns  1.first_name,   2.last_name and orders the records/rows by first name descending alphabetically(Z - A)
```



-- Retrieve the data with filter condition
```shell
#filter conditions are criteria that we use to get more specific data from a database

SELECT *
FROM sakila.actor;

SELECT *
FROM sakila.actor
WHERE actor_id > 100;
#returns all the records where the actor_id field is greater than 100. This excludes 100 and returns fields whose actor_id starts from 101

SELECT *
FROM sakila.actor
WHERE actor_id < 100;
#returns records whose actor_id field is less than 100. Excludes 100 and returns everything up to 99.

SELECT actor_id, first_name, last_name
FROM sakila.actor
WHERE first_name = 'Nick';
#returns data from the three columns 1.actor_id,  2.first_name,  3.last_name
#filters out the data within these three columns to return only records whose first name is equal to 'Nick'



```

-- Retrieve the data with filter condition and ordered by columns
```shell
SELECT *
FROM sakila.actor
WHERE first_name = 'Nick';
#returns all the records whose first_name fields equals 'Nick'
#+----------+------------+-----------+---------------------+
#| actor_id | first_name | last_name | last_update         |
#+----------+------------+-----------+---------------------+
#|        2 | NICK       | WAHLBERG  | 2006-02-15 04:34:33 |
#|       44 | NICK       | STALLONE  | 2006-02-15 04:34:33 |
#|      166 | NICK       | DEGENERES | 2006-02-15 04:34:33 |
#+----------+------------+-----------+---------------------+
#3 rows in set (0.00 sec)


SELECT actor_id, first_name, last_name
FROM sakila.actor
WHERE first_name = 'Nick'
ORDER BY actor_id DESC;
#returns data within the specified three columns whose first names equal 'Nick' and then orders the records by actor_id DESCENDING
#+----------+------------+-----------+
#| actor_id | first_name | last_name |
#+----------+------------+-----------+
#|      166 | NICK       | DEGENERES |
#|       44 | NICK       | STALLONE  |
#|        2 | NICK       | WAHLBERG  |
#+----------+------------+-----------+
#3 rows in set (0.00 sec)


SELECT actor_id, first_name, last_name
FROM sakila.actor
WHERE actor_id > 100
ORDER BY first_name, last_name DESC;
#returns data ih the specified three columns
#keeps only the records whose actor_id is greater than 100
#orders these records by first name alphabetically and then orders similar first names by their last names in descending order(Z - A)

```
