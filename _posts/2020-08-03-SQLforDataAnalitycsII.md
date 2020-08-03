---
title: "SQL for Data Analytics II"
date: 2020-08-03
tags: [SQL]
excerpt: "SQL for Data Analytics II"
mathjax: "True"
---

## Notes on Postgresql for Data Analysis -- II

- [1. Aggregation](#1)
- [2. Date Functions](#2)
- [3. CASE Statements](#3)

<a name='1'></a>

# Aggregation

SQL allows us to transform and aggregate our data hence making queries more efficient and results more meaningful. Aggregations work down column and not across rows. Below are some of the aggregation functions that we can use in SQL:
*   `COUNT` -- counts how many rows are in a particular column
*   `SUM` -- adds up all the values in a particular column
*   `MIN`  -- returns the minimun value in a particular column
*   `MAX`  -- returns the maximun value in a particular column
*   `AVERAGE` -- calculates the average in a particular column

### Examples:

1. To count the number of rows in the *accounts* table:

```
SELECT COUNT(*)
FROM accounts;
```

2. Return the total amount of `poster_qty` paper ordered:

```
SELECT SUM(poster_qty)
FROM orders;
```

3. Return the total amount of `standard_qty` paper orderd:

```
SELECT SUM(standard_qty)
FROM orders;
```

4. Return the `total_amt_usd` of sales:

```
SELECT SUM(total_amt_usd)
FROM orders;
```

5. Return the ratio between the totals of `standard_amt_usd` & `standard_qty`

```
SELECT SUM(standard_amt_usd) / SUM(standard_qty)
FROM orders;
```

6. Return the earliest order ever placed:

```
SELCT MIN(occurred_at)
FROM orders;
```

7. Return the latests order placed

```
SELECT MAX(occurred_at)
FROM orders;
```

8. Return the average for each paper typer as well as its amount spent per order

```
SELECT AVG(standard_qty) AS avg_standard,
       AVG(standard_amt_usd) AS avg_standard_amt,
       AVG(gloss_qty) AS avg_gloss,
       AVG(gloss_amt_usd) AS avg_gloss_amt,
       AVG(poster_qty) AS avg_poster,
       AVG(poster_amt_usd) AS avg_poster_amt
FROM orders;
```
## GROUP BY
Using a `GROUP BY` clause allows us to create segments that will aggregate independent from each other. For instance, and using the queries above, we could sum up all of the sales of each paper type for each account. The `GROUP BY` clause always goes between the `WHERE` and `ORDER BY` clause. 

### Examples

1. Return which account placed the earliest orders:
```
SELECT accounts.name AS account_name,
       MIN(orders.occurred_at) AS date_ordered
FROM accounts
JOIN orders
ON accounts.id = orders.account_id
GROUP BY accounts.name;
```

2. Return the total sales for each account:
```
SELECT accounts.name AS account_name,
       SUM(orders.total_amt_usd) AS total
FROM accounts
JOIN orders
ON accounts.id = orders.account_id
GROUP BY accounts.name;
```

3. Return the smallest order in $ value for each account:
```
SELECT accounts.name, MIN(orders.total_amt_usd) AS smallest_order
FROM accounts
JOIN orders
ON accounts.id = orders.account_id
GROUP BY accounts.name
ORDER BY smallest_order;
```

4. Return the number of sales rep for each region:
```
SELECT region.name, COUNT(*) AS num_reps
FROM region
JOIN sales_reps
ON region.id = sales_reps.region_id
GROUP BY region.name
ORDER BY num_reps
```
4. Return the average amount of each type of paper purchased for each account. 
```
SELECT accounts.name, 
       AVG(standard_qty) AS avg_standard,
       AVG(gloss_qty) AS avg_gloss,
       AVG(poster_qty) AS avg_poster
FROM accounts
JOIN orders
ON accounts.id = orders.account_id
GROUP BY accounts.name;
```

5. Return the average amount spent on each type of paper for each account. Sort A-Z.
```
SELECT accounts.name, 
       AVG(standard_amt_usd) AS avg_standard_usd,
       AVG(gloss_amt_usd) AS avg_gloss_usd,
       AVG(poster_amt_usd) AS avg_poster_usd
FROM accounts
JOIN orders
ON accounts.id = orders.account_id
GROUP BY accounts.name
ORDER BY accounts.name;
```

6. Return the number of times a particular channel was used in a web event for each region.
```
SELECT region.name, 
       web_events.channel, 
       COUNT(*) num_events
FROM accounts
JOIN web_events
ON accounts.id = web_events.account_id
JOIN sales_reps 
ON sales_reps.id = accounts.sales_rep_id
```

## DISTINCT

The `DISTINCT` clause is always used with the `SELECT` clause to return the unique rows for all columns written in the `SELECT` statement. Its syntax is as follows:
```
SELECT DISTINCT column1, column2, column3
FROM table1;
```

### Example:

1. Use DISTINCT to check if there are any accounts associated with more than one region. 
```
SELECT DISTINCT id, name
FROM accounts;
```

## HAVING
The `HAVING` clause is used to filtered data based on a particular criteria. `HAVING` is similar to `WHERE` in concept with the difference that `HAVING` is used when the data has been aggregated. 

<a name='2'></a>

## DATE FUNCTIONS

Working with dates is somewhat cumbersome as each timestamp is treated as unique and it is not possible to aggregate. Databases use a different date format. They represent dates from the least to the most granular part of the date: `YYYY:MM:DD`. This format is very useful and practical as the dates are sorted alphabetically and also in chronological order so when we want to retrieve the newests or oldest date-- it is correct and a lot easier to sort by `YYYY` rather than any other format. Another benefit is the date can be easily **truncated** so they can be group for analysis. 
Let's say we need to retrieve data for a particular day:
`2020-07-10- 11:50:01` since each data point has a unique timestamp we would not be able to group it and it will only return one data point. To group by day, we would need to adjust all the times for July 10th to read `2020-07-10 00:00:00`. By doing this we would retrieve every event that occured for all hours. minutes and secods of July 10th. They will al bee group together into a single grouping. To achieve this we use `DATE_TRUNC`.

`DATE_TRUNC` allows us to truncate our date to a particular part of our datetime column. We can truncate by `day, month, year`. In the example below, we're showing how to get the total number of orders placed daily. We use `DATE_TRUNC` in the `SELECT` clause. The first argument is the truncation method, which is daily in this case, and the second argument is the column that contains the order's dates. In the second line, we sum all the orders to get the total of daily orders. It is important to group by and order the query by the same statement used in the `SELECT` clause to ensure consistent results. 
```
SELECT DATE_TRUNC('day',  order_date) AS day
       SUM(orders) AS orders_sum
FROM orders
GROUP BY DATE_TRUNC('day',  order_date)
ORDER BY DATE_TRUNC('day',  order_date)
```
We can use `DATE_TRUNC` to aggregate dates at a very granular level-- down to the second. Here are the most common options used when truncating and their corresponding outputs:

<pre>
INPUT                                               OUTPUT
DATE_TRUNC('second', 2020-07-10 12:20:01)         2020-07-10 12:20:01 
DATE_TRUNC('day', 2020-07-10 12:20:01)            2020-07-10 00:00:00
DATE_TRUNC('month', 2020-07-10 12:20:01)          2020-07-10 00:00:00
DATE_TRUNC('year', 2020-07-10 12:20:01)           2020-01-10 00:00:00
</pre>

There are instances where we might want to retrieve a given part of a date. For instance, we want to know what day of the week sees the more sales. To get the day of the week, we would use `DATE_PART`. This function allows us to pull the part of the date that we are interested in. Let's look at the following example:

```
SELECT DATE_PART('dow', order_date) AS day_of_week
       SUM(total) AS total_qty
FROM orders
GROUP BY 1
ORDER BY 2 DESC
```
We use `DATE_PART` in the `SELECT` stament. Its first argument is `dow` which stands for *day of the week* since that is the metric we want to evaluate upon. DOW will return a numeric value form `0 - 6` representing Sunday to Saturday, then we sum all the orders. The one and two in the query represent the columns in the `SELECT` statement.

### Examples of working with dates:

1.   Return the dollar ammount for all sales in a yearly basis. Sort in HI-LO way for the dollar amount.
```
SELECT DATE_TRUNC('year', occurred_at) AS year,
       SUM(total_amt_usd) as total_amt_usd_year
FROM orders
GROUP BY DATE_TRUNC('year', occurred_at)
ORDER BY SUM(total_amt_usd) DESC;
```

2.  Return the best performing months in terms of dollar amounts:
```
SELECT DATE_PART('month', occurred_at) AS month,
       SUM(total_amt_usd) as total_amt_usd_year
FROM orders
GROUP BY DATE_PART('month', occurred_at)
ORDER BY SUM(total_amt_usd) DESC;
```

3.  Return the best performing years in terms of total orders placed:
```
SELECT DATE_PART('year', occurred_at) AS ord_year,  
       COUNT(*) AS total_sales
FROM orders
GROUP BY 1
ORDER BY 2 DESC;
```

4.  Return the best performing months in terms of total orders placed:
```
SELECT DATE_PART('month', occurred_at) AS month,
       COUNT(*) as total
FROM orders
GROUP BY DATE_PART('month', occurred_at)
ORDER BY SUM(total) DESC;
```

5.   Return the month and year in which Walmart spend the most amount of dollars in gloss paper:
```
SELECT DATE_TRUNC('month', occurred_at) AS order_date, accounts.name,
       SUM(orders.gloss_amt_usd) AS gloss_tot_amt
FROM orders
JOIN accounts
ON orders.account_id = accounts.id
WHERE accounts.name = 'Walmart'
GROUP BY 1, 2
ORDER BY 3 DESC
LIMIT 1;
```
<a name='3'></a>

## CASE Statements

`CASE` statements are basically SQL's way to handle `IF - THEN` logic. It is followed by at least one pair of `WHEN` and `THEN` statements -- SQL's equivalent of `IF THEN` and it ends with the word `END`. `ELSE` is an optional argument and it is used evaluate conditions that were not meet in the case statement. We can make any conditional statement using any conditional operator, such as `WHERE`, `BETWEEN`, `WHEN` and `THEN`. We can also combine multiple conditional statements using `AND` and `OR`. The results of the case statement will be displayed in a *derived* column. Example:
```
SELECT CASE WHEN total > 500 THEN 'Over 500'
            ELSE '500 & under' END AS total_group
            COUNT(*) AS order_count
FROM orders
GROUP BY 1;
```
Let's look at this query in more detail. We use the `CASE` statement in the `SELECT` clause. The 'main' condition looks at whether the order total is greater than 500. If it is, it will be counted and display in the 'Over 500' category. If the total is less than 500 then it will be aggregated on the '500 & under' category. We group the results by `1` which is the first term in the select statement. 

### Examples:

1.  Classify each order by level. Assign order to the group *Large* if the order total in usd is greater than 3000 and to the *Small* group otherwise. Return the account id, the total for the order and the groping:
```
SELECT account_id, total_amt_usd,
CASE WHEN total_amt_usd > 3000 THEN 'Large'
ELSE 'Small' END AS order_level
FROM orders;
```

2.  Classify the orders into 3 categories based on total number of items. Categories are: "At Least 2000", "Between 1000 and 2000", and "Less than 1000"
```
SELECT CASE WHEN total >= 2000 THEN 'At Least 2000'
       WHEN total >= 1000 AND total < 2000 THEN 'Between 1000 and 2000'
       ELSE 'Less than 1000' END AS order_category,
COUNT(*) AS order_count
FROM orders
GROUP BY 1;
```

3.   Segment the customers into 3 tiers based on the amount they spent in orders in usd. The top tier corresponds to customers that have a Lifetime value (total sales for all orders in usd) greater than 200,000. Second tier for purchases between 200,000 and 100,000. And the third tier for purchases under 100,000. Return the account name, total sales of all orders and the tier they correspond to:
```
SELECT accounts.name, 
       SUM(orders.total_amt_usd) AS total_amt_spent,
       CASE WHEN SUM(orders.total_amt_usd) >= 200000 THEN 'Tier 1'
       WHEN SUM(orders.total_amt_usd) > 100000 AND  SUM(orders.total_amt_usd) < 200000 THEN 'Tier 2'
       ELSE 'Tier 3' END AS customer_tier
FROM orders
JOIN accounts
ON orders.account_id = accounts.id
GROUP BY 1
ORDER BY 2 DESC;
```

4.   Return the same query as above but this time only for orders that took place after 2015. Include the transaction date. 
```
SELECT accounts.name, orders.occurred_at,
       SUM(orders.total_amt_usd) AS total_amt_spent,
       CASE WHEN SUM(orders.total_amt_usd) >= 200000 THEN 'Tier 1'
       WHEN SUM(orders.total_amt_usd) > 100000 AND  SUM(orders.total_amt_usd) < 200000 THEN 'Tier 2'
       ELSE 'Tier 3' END AS customer_tier
FROM orders
JOIN accounts
ON orders.account_id = accounts.id
WHERE orders.occurred_at > '2016-12-31'
GROUP BY 1, 2
ORDER BY 3 DESC;
```

5.   Segment the sales reps based on performace. If sales rep has more than 200 orders include the rep in the *top performing* group, *regular* otherwise. Return a table with the rep's name, the total number of orders, and the category. Sort in `DESC` order. 
```
SELECT sales_reps.name, 
       COUNT(*) AS num_order,
       CASE WHEN COUNT(*) > 200 THEN 'Top Performer'
       ELSE 'Regular' END AS sales_rep_performance
FROM orders
JOIN accounts
ON accounts.id = orders.account_id
JOIN sales_reps
ON sales_reps.id = accounts.sales_rep_id
GROUP BY 1
ORDER BY 2 DESC;
```

6.   Let's revise the criteria and add a new category for the query above. Now, identify a top performer when the rep has more than 200 orders or more than \$750,000 in total sales. Also create a 'medium' category for reps with more than 150 orders or $500,000 in sales. Everyone else who does not meet this criteria would go to the 'low' performance category. Sort by dollar amount in `DESC`.
```
SELECT sales_reps.name,
       SUM(orders.total_amt_usd) AS total_spent,
       COUNT(*) AS num_order,
       CASE WHEN COUNT(*) > 200 OR SUM(orders.total_amt_usd) > 750000 THEN 'top'
       WHEN COUNT(*) > 150 OR SUM(total_amt_usd) > 500000 THEN 'middle'
       ELSE 'low' END AS rep_performance
FROM orders
JOIN accounts
ON accounts.id = orders.account_id
JOIN sales_reps
ON sales_reps.id = accounts.sales_rep_id
GROUP BY 1
```