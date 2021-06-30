# SQL: Joins

**JOINS** allow us to combine information from multiple tables.

**AS** allows us to create an alias for a column or result. Executed at the end of the query. Cannot be used at the `WHERE` or `HAVING` operator
```
SELECT column as new_name FROM table

SELECT amount AS rental_price
FROM payment

SELECT SUM(amount) AS net_revenue 
FROM payment

SELECT customer_idd, SUM(amount) AS total_spent
FROM payment
GROUP BY customer_id
HAVING SUM(amoount) > 100
```

**INNER JOIN** will result the sset of records that match in both tables. Will return entries that are in both Table A and Table B. Intersection. Symmetrical-- meaning no affect if tables are reordered in the statement.

```
SELECT * FROM TableA
INNER JOIN TableB 
ON TableA.col_match = TableB.col_match

SELECT reg_id, Logins.name, log_id FROM Registration
INNER JOIN Logins
ON Registrations
INNER JOIN Logins
ON Registration.name = Logins.name


SELECT payment_id, payment.customer_id, first_name
FROM payment
INNER JOIN customer
ON payment.customer_id = customer.customer_id
```
| "payment_id" | "customer_id" | "first_name" |
|--------------|---------------|--------------|
| 17503        | 341           | "Peter"      |
| 17504        | 341           | "Peter"      |
| 17505        | 341           | "Peter"      |
| 17506        | 341           | "Peter"      |
| 17507        | 341           | "Peter"      |


**FULL OUTER JOIN** deal with values on present in one of the tables being joined. It will get everything in Table A and the matches on table B. If no match in each other, it will be replaced with a null

**Registration**
| reg_id | name     |
|--------|----------|
| 1      | Andrew   |
| 2      | Bob      |
| 3      | Charlie  |
| 4      | David    |

**Logins**
| log_id | name    |
|--------|---------|
| 1      | Xavier  |
| 2      | Andrew  |
| 3      | Yolanda |
| 4      | Bob     |

```
SELECT * FROM TableA
FULL OUTER JOIN TableB
ON TableA.col_match = TableB.col_match

SELECT * FROM Registrations FULL OUTER JOIN Logins
ON Registration.name = Logins.name
```
| reg_id | name    | log_id | name    |
|--------|---------|--------|---------|
| 1      | Andrew  | 2      | Andrew  |
| 2      | Bob     | 4      | Bob     |
| 3      | Charlie | null   | null    |
| 4      | David   | null   | null    |
| null   | null    | 1      | Xavier  |
| null   | null    | 3      | Yolanda |


**FULL OUTER JOIN WITH WHERE** Get rows unique to either table. Exact opposite of inner join
```
SELECT * FROM TableA
FULL OUTER JOIN TableB
ON TableA.col_match = TableB.col_match
WHERE TableA.id IS null OR 
TableB.id IS null

SELECT * FROM Registrations FULL OUTER JOIN Logins
ON Registrations.name = Logins.name
WHERE Registrations.reg_id IS null OR 
Logins.log_id IS NULL
```
| reg_id | name    | log_id | name    |
|--------|---------|--------|---------|
| 3      | Charlie | null   | null    |
| 4      | David   | null   | null    |
| null   | null    | 1      | Xavier  |
| null   | null    | 3      | Yolanda |

```
-- We dont have any payment info that dont have a customer or
-- no customer with no payments
SELECT * FROM customer
FULL OUTER JOIN payment
ON customer.customer_id = payment.customer_id
WHERE customer.customer_id IS NULL
OR payment.payment_id IS NULL

-- Result is empty
```

**LEFT OUTER JOIN** fetches all records on the left table. If no entries match on the right table, the results are null. Table order matters on this case.
```
SELECT * FROM TableA 
LEFT OUTER JOIN TableB
ON TableA.col_match = TableB.col_match

SELECT * FROM TableA 
LEFT JOIN TableB
ON TableA.col_match = TableB.col_match

SELECT * FROM Registrations
LEFT OUTER JOIN Logins
ON Registrations.name = Logins.name
```
| reg_id | name    | log_id | name   |
|--------|---------|--------|--------|
| 1      | Andrew  | 2      | Andrew |
| 2      | Bob     | 4      | Bob    |
| 3      | Charlie | null   | null   |
| 4      | David   | null   | null   |

Unique to the Left Table not found in right table
```
SELECT * FROM TableA
LEFT OUTER JOIN TableB
ON TableA.col_match = TableB.col_match
WHERE TableB.id is null

SELECT * FROM Registrations
LEFT OUTER JOIN Logins
ON Registrations.name = Logins.name
WHERE Logins.log_id is null
```
| reg_id | name    | log_id | name   |
|--------|---------|--------|--------|
| 3      | Charlie | null   | null   |
| 4      | David   | null   | null   |

```
-- Get all films that are in inventory
SELECT film.film_id, film.title, inventory_id
FROM film
LEFT JOIN inventory ON
inventory.film_id = film.film_id

--same as
SELECT inventory_id, (select title from film where film_id=inventory.film_id) FROM inventory
```

**RIGHT JOIN** is same as the LEFT JOIN but order is switched
```
SELECT * FROM TableA
RIGHT OUTER JOIN TableB
ON TableA.col_match = TableB.col_match

-- exclusively on TableB
SELECT * FROM TableA
RIGHT OUTER JOIN TableB
ON TableA.col_match = TableB.col_match
WHERE TableA.id IS NULL
```

**UNION** combine the results of two SELECT Statement
```
SELECT col1, col2 FROM Table1
UNION
SELECT col3, col4 FROM Table2
```

**Assessment**
```
-- Get all emails from customers living in California
SELECT email, district FROM address
INNER JOIN customer
ON address.address_id = customer.address_id
WHERE district = 'California'

-- Get all films played in by Nick Wahlberg
select title from film
inner join film_actor
on film.film_id = film_actor.film_id
inner join actor
on film_actor.actor_id = actor.actor_id
where first_name = 'Nick' and last_name = 'Wahlberg'
```