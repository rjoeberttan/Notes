# SQL: Statements Fundamentals

`SELECT`  


**Select `column1` and `column2`**
``` 
SELECT first_name, last_name
FROM actor;
```
| "first_name" | "last_name"    |
|--------------|----------------|
| "Penelope"   | "Guiness"      |
| "Nick"       | "Wahlberg"     |
| "Ed"         | "Chase"        |
| "Jennifer"   | "Davis"        |
| "Johnny"     | "Lollobrigida" |
<br>

**Select all columns**
```
SELECT * 
FROM actor;
```
| "actor_id" | "first_name" | "last_name"    | "last_update"            |
|------------|--------------|----------------|--------------------------|
| 1          | "Penelope"   | "Guiness"      | "2013-05-26 14:47:57.62" |
| 2          | "Nick"       | "Wahlberg"     | "2013-05-26 14:47:57.62" |
| 3          | "Ed"         | "Chase"        | "2013-05-26 14:47:57.62" |
| 4          | "Jennifer"   | "Davis"        | "2013-05-26 14:47:57.62" |
| 5          | "Johnny"     | "Lollobrigida" | "2013-05-26 14:47:57.62" |
<br>

**Select firstname, lastname, and email of customers**
```
SELECT first_name, last_name, email
FROM customer
```
| "first_name" | "last_name" | "email"                               |
|--------------|-------------|---------------------------------------|
| "Jared"      | "Ely"       | "jared.ely@sakilacustomer.org"        |
| "Mary"       | "Smith"     | "mary.smith@sakilacustomer.org"       |
| "Patricia"   | "Johnson"   | "patricia.johnson@sakilacustomer.org" |
| "Linda"      | "Williams"  | "linda.williams@sakilacustomer.org"   |
| "Barbara"    | "Jones"     | "barbara.jones@sakilacustomer.org"    |
<br>

**Select Distinct or Unique** returns all unique values of a column. Can be said get all possible values from a column. How many unique years we have on film table?
```
SELECT DISITNCT release_year FROM film;
```
| "release_year" |
|----------------|
| 2006           |

How many unique rentals rates we have?
```
SELECT DISITNCT(rental_rate) FROM film;
```
| "rental_rate" |
|---------------|
| 2.99          |
| 4.99          |
| 0.99          |
```
SELECT DISITNCT(rating) FROM film;
```
| "rating" |
|----------|
| "R"      |
| "NC-17"  |
| "G"      |
| "PG"     |
| "PG-13"  |
<br>

**COUNT** returns the number of input rows that match a specific condition of a query
```
SELECT COUNT(*) FROM payment;
or
SELECT COUNT(amount) FROM payment;
```
| "count" |
|---------|
| 14596    |
```
SELECT COUNT(DISTINCT amount) FROM payment;
```
| "count" |
|---------|
| 19      |
<br>

**SELECT WHERE** specify conditions on columns for the rows to be returned. When usiung AND or OR. Operator AND is applied first and OR is applied second. Unless we use parentheses
```
SELECT * FROM customer 
WHERE first_name = 'Jared';

SELECT * FROM film
WHERE rental_rate > 4 AND replacement_cost >= 19.99 
AND rating='R';

SELECT COUNT(*) FROM film
WHERE rental_rate > 4 AND replacement_cost >= 19.99 
AND rating='R' ;

SELECT COUNT(*) FROM film
WHERE rating='R' OR rating='PG-13';

SELECT * FROM film
WHERE rating != 'R';

SELECT description FROM film
WHERE title = 'Outlaw Hanky'

SELECT * FROM employees
WHERE last_name = 'Denis AND (gender = 'M' or gender = 'F')

SELECT phone FROM address WHERE address = '259 Ipoh Drive'
```
<br>

**ORDER BY** sort rows based on a column value depending on ascening or descending. Ascending by default. Can also be used on multiple columns
```
SELECT col1, col2
FROM table
ORDER BY col1 ASC/DESC

SELECT company, name, sales FROM table
ORDER BY company, sales    -- Sort by company first, then sales

SELECT * FROM customer
ORDER BY store_id, first_name ASC

SELECT store_id, first_name, last_name FROM customer
ORDER BY store_id DESC, first_name ASC
```
| "store_id" | "first_name" | "last_name" |
|------------|--------------|-------------|
| 2          | "Aaron"      | "Selby"     |
| 2          | "Adrian"     | "Clary"     |
| 2          | "Agnes"      | "Bishop"    |
| 2          | "Alexander"  | "Fennell"   |
| 1          | "Andrea"     | "Henderson" |
| 1          | "Angel"      | "Barclay"   |
| 1          | "Chad"       | "Carbone"   |
| 1          | "Charles"    | "Kowalski"  |
| 1          | "Charlotte"  | "Hunter"    |
<br>

**LIMIT** at the end of the query. Top 10 most recent payments with actual amount
```
SELECT payment_id, customer_id, amount, payment_date FROM payments
WHERE amount > 0
ORDER BY payment_date DESC
LIMIT 10
```
| "payment_id" | "customer_id" | "amount" | "payment_date"               |
|--------------|---------------|----------|------------------------------|
| 31928        | 296           | 2.99     | "2007-05-14 13:44:29.996577" |
| 31926        | 287           | 0.99     | "2007-05-14 13:44:29.996577" |
| 31924        | 284           | 5.98     | "2007-05-14 13:44:29.996577" |
| 31927        | 295           | 0.99     | "2007-05-14 13:44:29.996577" |
| 31923        | 282           | 0.99     | "2007-05-14 13:44:29.996577" |
| 31917        | 267           | 7.98     | "2007-05-14 13:44:29.996577" |
| 31922        | 279           | 4.99     | "2007-05-14 13:44:29.996577" |
| 31919        | 269           | 3.98     | "2007-05-14 13:44:29.996577" |
| 31921        | 274           | 0.99     | "2007-05-14 13:44:29.996577" |
| 31929        | 300           | 4.99     | "2007-05-14 13:44:29.996577" |

Get top 5 movies with shortest lengths
```
SELECT title, length FROM film
ORDER BY length ASC
LIMIT 5
```
| "title"               |
|-----------------------|
| "Labyrinth League"    |
| "Alien Center"        |
| "Iron Moon"           |
| "Kwai Homeward"       |
| "Ridgemont Submarine" |
<br>

**BETWEEN** value >= low AND value <= high (inclusive). Can also be used as `NOT BETWEEN` (exclusive). When using on dates it should be ISO 8601: YYYY-MM-DD
```
SELECT * FROM payment
WHERE amount BETWEEN 8 AND 9;

SELECT * FROM payment
WHERE amount NOT BETWEEN 8 AND 9;

SELECT payment_id, customer_id, amount, payment_date FROM payment
WHERE payment_date BETWEEN '2007-02-01' AND '2007-02-15'
-- for dates it always is considered as YYYY-MM-DD 00:00
```
| "payment_id" | "customer_id" | "amount" | "payment_date"               |
|--------------|---------------|----------|------------------------------|
| 17610        | 368           | 0.99     | "2007-02-14 23:25:11.996577" |
| 17617        | 370           | 6.99     | "2007-02-14 23:33:58.996577" |
| 17743        | 402           | 4.99     | "2007-02-14 23:53:34.996577" |
| 17793        | 416           | 2.99     | "2007-02-14 21:21:59.996577" |
| 17854        | 432           | 5.99     | "2007-02-14 23:07:27.996577" |
| 18051        | 481           | 2.99     | "2007-02-14 22:03:35.996577" |
<br>

**IN** Multiple values conditions
```
SELECT color FROM table
WHERE color IN ('red', 'blue')

SELECT color FROM table
WHERE color NOT IN ('red', 'blue')

SELECT payment_id, customer_id, amount, payment_date FROM payment
WHERE amount IN (0.99, 1.98, 1.99)
ORDER BY amount 

SELECT payment_id, customer_id, amount, payment_date FROM payment
WHERE amount NOT IN (0.99, 1.98, 1.99)
ORDER BY amount 

SELECT customer_id, first_name, last_name
FROM customer
WHERE first_name in ('John', 'Jake', 'Julie')
```
| "customer_id" | "first_name" | "last_name"  |
|---------------|--------------|--------------|
| 52            | "Julie"      | "Sanchez"    |
| 300           | "John"       | "Farnsworth" |
<br>

**LIKE and ILIKE** matches a general pattern. **%** matches any sequence of character while **_** only matches a single character. `LIKE` is case sensitive while `ILIKE` is not case sensitive.
```
-- First name starts with J and Last name starts with S
SELECT * FROM customer 
WHERE first_name LIKE 'J%' AND last_name ILIKE 's%'

SELECT * FROM customer 
WHERE first_name LIKE '%her%'

SELECT * FROM customer 
WHERE first_name LIKE '_her%

SELECT * FROM customer 
WHERE first_name NOT LIKE '_her%'

SELECT customer_id, first_name, last_name FROM customer
WHERE first_name LIKE 'A%' AND last_name NOT LIKE 'B%'
ORDER BY last_name
LIMIT 5
```
| "customer_id" | "first_name" | "last_name" |
|---------------|--------------|-------------|
| 196           | "Alma"       | "Austin"    |
| 40            | "Amanda"     | "Carter"    |
| 423           | "Alfred"     | "Casillas"  |
| 599           | "Austin"     | "Cintron"   |
| 525           | "Adrian"     | "Clary"     |
<br>

**IS NOT NULL / IS NULL** shows values is null or not null
```
SELECT * FROM customer
WHERE first_name IS NOT NULL

SELECT * FROM customer
WHERE first_name IS NULL
```
<br>