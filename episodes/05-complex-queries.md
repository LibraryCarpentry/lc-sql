---
title: "Order of Execution & Building Complex Queries"
teaching: 15
exercises: 0
questions:
- "What is the order of execution in SQL queries?"
- "How can you organise and comment more complex SQL queries?"
objectives:
- "Understand how to build queries, and the order in which to build the parts."
keypoints:
- "Queries often have the structure: SELECT data FROM table WHERE certain criteria are present." 
---

## Order of Execution

Let's say we had the following query:

~~~
SELECT Title, Authors
FROM articles
WHERE ISSNs = '2067-2764|2247-6202'
ORDER BY First_Author ASC;
~~~
{: .sql}

What is interesting to note about this query is that we don't necessarily have to display the `First_Author` column in our results in order to sort by it. 

We can do this because sorting occurs earlier in the computational pipeline than field selection.

The computer is basically doing this:

1. Filtering rows according to WHERE
2. Sorting results according to ORDER BY
3. Displaying requested columns or expressions.

Clauses are written in a fixed order: `SELECT`, `FROM`, `WHERE`, then `ORDER
BY`. It is possible to write a query as a single line, but for readability,
we recommend to put each clause on its own line.


## Building Complex Queries

Consider the following query:

~~~
SELECT *
FROM articles
WHERE (ISSNs = '2076-0787') OR (ISSNs = '2077-1444') OR (ISSNs = '2067-2764|2247-6202');
~~~
{: .sql}

SQL offers the flexibility of iteratively adding new conditions but you may reach a point where the query is difficult to read and inefficient. For instance, we can use `IN` to improve the query and make it more readable:

~~~
SELECT *
FROM articles
WHERE (ISSNs IN ('2076-0787', '2077-1444', '2067-2764|2247-6202'));
~~~
{: .sql}

We started with something simple, then added more clauses one by one, testing
their effects as we went along.  For complex queries, this is a good strategy, to make sure you are getting what you want.  Sometimes it might help to take a subset of the data that you can easily see in a temporary database to practice your queries on before working on a larger or more complicated database.

When the queries become more complex, it can be useful to add comments. In SQL, comments begin with `--` and end at the end of the line. For example, a
commented version of the above query can be written as:

~~~
-- Select all columns
SELECT * 
-- From the article table
FROM articles
-- Select only the records that have the following ISSNs in them
WHERE (ISSNs IN ('2076-0787', '2077-1444', '2067-2764|2247-6202'));
~~~
{: .sql}

Although SQL queries often read like plain English, it is *always* useful to write comments especially when the queries become more complex. 
