# SQL: Aggregations

**Aggregate Functions** take multiple inputs and return a single output. Happen only in the select clause
1. **AVG** returns floating point value. We can use **ROUND()** on top of AVG  
2. **COUNT**
3. **MAX AND MIN**
4. **SUM**
5. **DATE** removes time gets only the YYYY-MM-DD

```
SELECT  MIN(replacement_cost), MAX(replacement_cost), 
ROUND(AVG(replacement_cost), 2), SUM(replacement_cost),
COUNT(replacement_cost)
FROM film;
```
| "min" | "max" | "round" | "sum"    | "count" |
|-------|-------|---------|----------|---------|
| 9.99  | 29.99 | 19.98   | 19984.00 | 1000    |

**GROUP BY** allow us aggreagate columns per some category. Categorical columns are non-continuous (considered as). Coilumns must eitheer have an aggregate function or be in the GROUP BY call
```
SELECT category_col, AGG(data_col)
FROM table
WHERE ...
GROUP BY category_col
-- WHERE statements does not refer to the aggregation result


--Example of note statement
SELECT company, division, SUM(sales)
FROM finance_table
GROUP BY company, division
-- this will work because company and division are on Group by while sales is in aggrgate function.

SELECT company, division, SUM(sales)
FROM finance_table
GROUP BY company
-- will not work because division is not on GROUP BY or does not have an aggregate function
```

```
SELECT customer_id, staff_id, SUM(amount) FROM payment
GROUP BY staff_id, customer_id
ORDER BY customer_id

SELECT DATE(payment_date), SUM(amount) FROM payment
GROUP BY DATE(payment_date)
ORDER BY SUM(amount) DESC

SELECT DATE(payment_date), SUM(amount) FROM payment
GROUP BY DATE(payment_date)
ORDER BY SUM(amount) DESC

SELECT customer_id, staff_id, SUM(amount) FROM payment
GROUP BY staff_id, customer_id
ORDER BY customer_id

SELECT staff_id, count(amount)
FROM payment
GROUP BY staff_id
ORDER BY count(amount) DESC

SELECT rating, AVG(replacement_cost) from film
group by rating

SELECT customer_id, SUM(amount) from payment
group by customer_id
order by SUM(amount) DESC
```
<br>

**HAVING** allows us to filter after an aggregation
```
SELECT company, SUM(sales)
FROM finance_table
WHERE company != 'Google'
GROUP BY company
HAVING SUM(sales) > 1000

SELECT customer_id, SUM(amount) FROM payment
GROUP BY customer_id
HAVING SUM(amount) > 100

SELECT store_id, COUNT(customer_id) FROM customer
GROUP BY store_id
HAVING COUNT(customer_id) > 300

SELECT customer_id, count(*) FROM payment
group by customer_id
having count(*) >= 40

SELECT customer_id, SUM(amount) FROM payment
where staff_id = 2
group by customer_id
HAVING sum(amount) > 100
```
<br>

**ASSESSMENT** 
```
select customer_id, sum(amount) from payment
where staff_id = 2
group by customer_id
having sum(amount) >= 110

select * from film where title like 'J%'

select * from customer 
where first_name like 'E%' and address_id < 500 
order by customer_id desc
```

