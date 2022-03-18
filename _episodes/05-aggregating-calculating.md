---
title: "Aggregating & calculating values"
teaching: 15
exercises: 5
questions:
- "How can we aggregate values in SQL for reports?"
- "Can SQL be used to make calculations?"
objectives:
- "Use SQL functions like `AVG` in combination with clauses like `Group By` to aggregate values and return results for reports."
- "Make calculations on fields using SQL."
keypoints:
- "SQL can be used for reporting purposes."
- "Queries can do arithmetic operations on field values."
---

## Aggregation

SQL contains functions which allow you to make calculations on data in your database for reports. Some of the most common functions are `MAX, MIN, AVG, COUNT, SUM`, and they will: `MAX` (find the maximum value in a field), `MIN` (find the minimum value in a field), `AVG` (find the average value of a field), `COUNT` (count the number of values in a field and present the total), and `SUM` (add up the values in a field and present the sum).

Let's say we wanted to get the average `Citation_Count` for each of the `ISSNs`. We can use `AVG` and the `GROUP BY` clause in a query:

~~~
SELECT ISSNs, AVG(Citation_Count)
FROM articles
GROUP BY ISSNs;
~~~
{: .sql}

`GROUP BY` is used by SQL to arrange identical data into groups. In this case, we are arranging all the citation counts by ISSNs. `AVG` acts on the `Citation_Count` in parentheses. This process is also called **aggregation** which allows us to combine results by grouping records based on value and calculating combined values in groups.

As you can see, it is difficult to tell though what ISSN has the highest average citation count and the least. We can improve upon the query above by using `ORDER BY` and `DESC`. 

~~~
SELECT ISSNs, AVG(Citation_Count)
FROM articles
GROUP BY ISSNs 
ORDER BY AVG(Citation_Count) DESC;
~~~
{: .sql}

> ## Challenge
> Write a query using an aggregate function that returns the number of article titles per ISSNs, sorted by title count in descending order. Which ISSN has the most titles?  (Hint to choosing which aggregate function to use - it is one of the common aggreggate functions `MAX, MIN, AVG, COUNT, SUM`.)
>
> > ## Solution
> > ~~~
> > SELECT ISSNs, COUNT(Title)
> > FROM articles
> > GROUP BY ISSNs
> > ORDER BY count(Title) DESC;
> > ~~~
> > {: .sql}
> {: .solution}
{: .challenge}

## The `HAVING` keyword

SQL offers a mechanism to filter the results based on aggregate functions, through the `HAVING` keyword.

For example, we can adapt the last request we wrote to only return information about journal `ISSNs` with 10 or more published articles:

~~~
SELECT ISSNs, COUNT(*)
FROM articles
GROUP BY ISSNs
HAVING count(Title) >= 10;
~~~
{: .sql}

The `HAVING` keyword works exactly like the `WHERE` keyword, but uses aggregate functions instead of database fields.  When you want to filter based on an aggregation like `MAX, MIN, AVG, COUNT, SUM`, use `HAVING`; to filter based on the individual values in a database field, use `WHERE`.

Note that `HAVING` comes _after_ `GROUP BY`. One way to think about this is: the data are retrieved (`SELECT`), can be filtered (`WHERE`), then joined in groups (`GROUP BY`); finally, we only select some of these groups (`HAVING`).

> ## Challenge
> Write a query that returns, from the `articles` table, the average `Citation_Count` for each journal ISSN 
> but only for the journals with 5 or more citations on average.
>
> > ## Solution
> > ~~~
> > SELECT ISSNs, AVG(Citation_Count)
> > FROM articles
> > GROUP BY ISSNs
> > HAVING AVG(Citation_Count)>=5;
> > ~~~
> > {: .sql}
> {: .solution}
{: .challenge}

## Calculations

In SQL, we can also perform calculations as we query the database. Also known as computed columns, we can use expressions on a column or multiple columns to get new values during our query. For example, what if we wanted to calculate a new column called `CoAuthor_Count`:

~~~
SELECT Title, ISSNs, Author_Count -1 as CoAuthor_Count
FROM articles
ORDER BY Author_Count -1 DESC;
~~~
{: .sql}

In section [6. Joins and aliases](https://librarycarpentry.org/lc-sql/06-joins-aliases/index.html) we are going to learn more about the SQL keyword `AS` and how to make use of aliases - in this example we simply used the calculation and `AS` to separate the new column from the original SQL table data.

We can use any arithmetic operators (like `+`, `-`, `*`, `/`, square root `SQLRT` or the modulo operator `%`) if we would like.

If you would like to learn more about calculated values, the Software Carpentry Databases and SQL lesson includes a useful episode on [Calculating New Values](https://swcarpentry.github.io/sql-novice-survey/04-calc/index.html). 
