---
layout: reference
---

## SQL Cheat Sheet

_____
### Basic query

~~~
SELECT column_names
FROM table_name;
~~~
- selects only the specified columns from a table.

~~~
SELECT * 
FROM table_name;
~~~
- select all of the columns in a table.

~~~
SELECT DINSTINCT column_name 
FROM table_name;
~~~ 
- selects only the unique values from a table.

~~~
SELECT column_names
FROM table_name
WHERE column_name operator value;
~~~
- selects only the data that meets certain criteria.
- you can use operators `=`,`<`,`>`, etc
- you can also combine tests using `AND`, `OR` in the WHERE clause.

~~~
SELECT column_names
FROM table_name
WHERE column_name IN (value1, value2, value3);
~~~
- selects only the data where column_name equals to `value1`, `value2`, and so on.

~~~
SELECT column_names
FROM table_name
ORDER BY column_name ASC;
~~~
- selects only the specified columns from a table, sort the results by a column in `ASC` (ascending) or `DESC` (descending) order.

_____
### Aggregation

~~~
SELECT aggregate_function(column_name)
FROM table_name;
~~~
- Aggregate results by grouping records based on value and calculating combined values in groups. 
- E.g. `SELECT COUNT(*) FROM table_name` will display the total number of records.
- You can use aggregate functions `COUNT`, `SUM`, `MAX`, `MIN`, `AVG`.

~~~
SELECT column_name, aggregate_function(column_name)
FROM table_name
WHERE column_name operator value
GROUP BY column_name;
~~~
- `GROUP BY` tells SQL what field or fields we want to use to aggregate the data. If we want to group by multiple fields, we give `GROUP BY` a comma separated list.

~~~
SELECT column_name, aggregate_function(column_name)
FROM table_name
GROUP BY column_name
HAVING aggregate_function(column_name) operator value;
~~~
- The `HAVING` keyword works exactly like the `WHERE` keyword, but uses aggregate functions instead of database fields.

_____
### Joins and aliases

~~~
SELECT column_names
FROM table_name1
JOIN table_name2 
ON table_name1.column_name = table_name2.column_name;
~~~
- Combine data from two tables where the values of column_name in the two tables are the same.
- Instead of `ON`, you can use the `USING` keyword as a shorthand. E.g. `USING (coolumn_name)`.

~~~
SELECT alias1.column_name1, alias1.column_name2, alias2.column_name3
FROM table_name1 AS alias1
JOIN table_name2 AS alias2
ON alias1.column_name = alias2.column_name;
~~~
- we can use aliases to assign new names to things in the query.
- we can use as to rename column names too. E.g. `SELECT journal_title AS journal`.

_____
### Saving queries

~~~
CREATE VIEW viewname AS
SELECT column_names
FROM table_name;
~~~
- create a stored query or virtual table in database for repeated queries

_____
### Commenting

~~~
-- Select all columns
SELECT * 
-- From the table_name
FROM table_name
~~~
- we can create comments in SQL queries to help us/others understand the query better

_____
### Operators

Arithmetic operators
`+` `-` `*` `/` 

Comparison operators
`=` `<` `>` `<=` `>=` `<>` 

Logical operators
`ALL` `AND` `ANY` `BETWEEN` `EXISTS` `IN` `LIKE` `NOT` `OR` `SOME`
