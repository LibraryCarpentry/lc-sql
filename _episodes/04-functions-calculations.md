---
title: "Aggregation & calculating values"
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

SQL contains functions which allow you to make calculations on data in your database for reports. Some of the most common functions are `MAX, MIN, AVG, COUNT, SUM`. Let's say we wanted to get the average `Citation_Count` for `ISSNs`. We can use `AVG` and the `GROUP BY` clause in a query:

~~~
SELECT ISSNs, AVG(Citation_Count)
FROM articles
GROUP BY ISSNs;
~~~
{: .sql}

`GROUP BY` is used by SQL to arrange identical data into groups. In this case, we are arranging all the citation counts by ISSNs. `AVG` acts on the `Citation_Count` in parentheses. This process is also called **aggregation** which allows us to combine results by grouping records based on value and calculating combined values in groups.

As you can see, it is difficult to tell though what ISSN has the highest average citation count and the least. We can improve upon the query above by using `ORDER BY` and `DESC`. 

~~~
SELECT ISSNs, AVG(Citation_Count) AS Avg_Citation_Count
FROM articles
GROUP BY ISSNs 
ORDER BY Avg_Citation_Count DESC;
~~~
{: .sql}

`AS` is used to create another column called `Avg_Citation_Count` to contain the calculations. This is what is called an alias which will be covered later in the lesson.

> ## Challenge
> Write a query that returns the title count grouped by `ISSNs` in descending order. Which ISSN has the most titles?
>
> > ## Solution
> > ~~~
> > SELECT  ISSNs, COUNT(Title) AS Title_Count
> > FROM articles
> > GROUP BY ISSNs
> > ORDER BY Title_Count DESC;
> > ~~~
> > {: .sql}
> {: .solution}
{: .challenge}

## The `HAVING` keyword

SQL offers a mechanism to filter the results based on aggregate functions, through the `HAVING` keyword.

For example, we can adapt the last request we wrote to only return information about journal `ISSNs` with 10 or more published articles:

~~~
SELECT ISSNs, COUNT(*) as Record_Count
FROM articles
GROUP BY ISSNs
HAVING Record_Count >= 10;
~~~
{: .sql}

The `HAVING` keyword works exactly like the `WHERE` keyword, but uses
aggregate functions instead of database fields.

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
SELECT Title, ISSNs, Author_Count -1 AS CoAuthor_Count
FROM articles
ORDER BY CoAuthor_Count DESC;
~~~
{: .sql}

We can use any arithmetic operators (`+`, `-`, `*`, and `/`) if we would like. 

If you would like to learn more about calculated values, the Software Carpentry Databases and SQL lesson includes an episode on [Calculating New Values](https://swcarpentry.github.io/sql-novice-survey/04-calc/index.html) which is useful. 
