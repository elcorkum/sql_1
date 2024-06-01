
-- Retrieve column names using aliases
```shell


SELECT rental_date, inventory_id, return_date
FROM sakila.rental;
#returns the three columns specified

SELECT 	rental_date AS RentalDate, 
		inventory_id AS FilmListID, 
		return_date AS ReturnDate
FROM sakila.rental;

#when we use AS   the data that is return will have the names we specify as the column names
```
-- Retrieve values based on arithmetic expressions

```shell
SELECT 	replacement_cost-rental_rate,
		film_id AS FilmID,
		length/60 
FROM sakila.film;
#returns three columns
#1.replacement_cost-rental_rate
#2.film_id AS FilmID  (film_id column will be named FilmID in the resulting data)
#3.length/60 which computes the length divided by 60


SELECT 	replacement_cost-rental_rate AS CostDiff,
		film_id AS FilmID,
		length/60 AS TimeinHour 
FROM sakila.film;
#returns three columns that will all be named using the aliases provided with the third column

SELECT 	rental_rate AS RentalRate,
		rental_rate + 3 * 4 - 1 AS Result1,
		(rental_rate + 3) * 4 -1 AS Result2,
		(rental_rate + 3) * (4 -1) AS Result3,
		rental_rate + (3 * 4) -1 AS Result4
FROM sakila.film;
#returns 5 columns
#1.rental_rate named RentalRate
#2.computation on the rental rate and this column is aliased Result1
#3.computation on rental rate and this column is aliased Result2
#4.computation on rental rate and this column is aliased Result3
#5.computation on rental rate and this column is aliased Result4


SELECT 	replacement_cost AS ReplacementCost,
		replacement_cost / 5 AS DecimalRentalRate,
		replacement_cost DIV 5 AS IntegerRentalRate,
		replacement_cost % 5 AS RemainderRentalRate
FROM sakila.film;
#returns 4 columns
#1.replacement_cost aliased as ReplacementCost
#2.computation on replacement cost aliased as DecimalRentalRate
#3.computation on replacement cost aliased as IntegerRentalRate
#4.computation on replacement cost aliased as RemainderRentalRate


```
-- Retrieve results based on function

```shell
SELECT *
FROM sakila.actor;

SELECT *
FROM sakila.payment;

-- ------------------------------------
-- Integer Operations
-- ------------------------------------

SELECT 	amount,
ROUND(amount) Amnt, ROUND(amount,1) Amnt1,
FLOOR(amount) FloorAmnt, CEILING(amount) CeilingAmnt
FROM sakila.payment;
#there are several integer functions used within SQL
#ROUND(amount)   rounds off to the nearest whole number
#ROUND(amount, 1)  rounds off to one decimal place
#FLOOR(amount)  rounds down decimal number to its integer value, ignoring the decimal value   3.897 would be 3
#CEILING(amount)  round up to the nest whole number 3.213 would be 4


SELECT ROUND(4.44,1);
#rounds off to one decimal place
#+---------------+
#| ROUND(4.44,1) |
#+---------------+
#|           4.4 |
#+---------------+
#1 row in set (0.00 sec)
```

-- ------------------------------------
-- String Operations
-- ------------------------------------
```shell
-- Concat
SELECT CONCAT(first_name, ' ', last_name) AS FullName
FROM sakila.actor;
#CONCAT   combines strings to make one string;

-- LEFT function
SELECT 	CONCAT(first_name, ' ', last_name) AS FullName,
CONCAT(LEFT(first_name,2),  LEFT(last_name,2)) AS FirstInitial
FROM sakila.actor;
#LEFT()  gets the first character from the left of a string.   LEFT('Antelope')   returns 'A'
#LEFT(name, 2) returns two characters starting from the leftmost

-- LENGTH function
SELECT 	CONCAT(first_name, ' ', last_name) AS FullName,
LENGTH(CONCAT(first_name, ' ', last_name)) AS Length,
CONCAT(LEFT(first_name,1), ' ', LEFT(last_name,1)) AS FirstInitial
FROM sakila.actor;

#LENGTH()  returns the number of characters in a string

-- Various function
SELECT 	CONCAT(first_name, ' ', last_name) AS FullName,
REVERSE(CONCAT(first_name, ' ', last_name)) AS ReverseFullName,
REPLACE(CONCAT(first_name, ' ', last_name),'S','$') AS ReplaceExample
FROM sakila.actor;

#REVERSE()  reverses the characters in a string    'maize' would be 'eziam'
#REPLACE() replaces occurrences of a specified character in a string with the given character
```


-- ------------------------------------
-- Date Operations
-- ------------------------------------
```shell
-- DATE_FORMAT function
SELECT 	CONCAT(first_name, ' ', last_name) AS FullName,
DATE_FORMAT(last_update, '%m/%d/%y') AS LastUpdated1,
DATE_FORMAT(last_update, '%d-%m-%Y') AS LastUpdated2,
DATE_FORMAT(last_update, '%d %b %Y %T:%f') AS LastUpdated3
FROM sakila.actor;

-- DATE_FORMAT with GET_FORMAT function
SELECT 	CONCAT(first_name, ' ', last_name) AS FullName,
DATE_FORMAT(last_update, GET_FORMAT(DATE,'EUR')) AS LastUpdated1,
DATE_FORMAT(last_update, GET_FORMAT(DATE,'ISO')) AS LastUpdated2,
DATE_FORMAT(last_update, GET_FORMAT(DATE,'USA')) AS LastUpdated3
FROM sakila.actor;


-- Other function
SELECT 	rental_date,
DAYOFWEEK(rental_date) AS DayOfWeek,
QUARTER(rental_date) AS Quarter,
WEEK(rental_date) AS Week,
MONTHNAME(rental_date) AS MonthName		
FROM sakila.rental;
```



-- ------------------------------------
-- DISTINCT Operations
when the DISTINCT keyword is used it returns only unique values(no duplicates or similar values)
-- ------------------------------------
```shell
SELECT first_name
FROM sakila.actor;

SELECT DISTINCT first_name
FROM sakila.actor;
#returns the first name column but only with unique names(any duplicates are left out)

SELECT last_name
FROM sakila.actor;

SELECT DISTINCT last_name
FROM sakila.actor;
#returns the last name column but only with unique names(any duplicates are left out)
```
