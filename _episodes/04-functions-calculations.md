---
title: "Functions and Calculations"
teaching: 15
exercises: 5
questions:
- "How can we produce reports using SQL?"
- "Can SQL be used to make calculations?"
objectives:
- "Use SQL functions like `AVG` to return results for reports."
- "Make calculations on fields using SQL."
keypoints:
- "SQL can be used for reporting purposes."
- "Queries can do arithmetic operations on field values."
---

## Functions

SQL contains functions which allow you to make calculations on data in your database for reporting purposes. Some of the most common functions are `MAX, MIN, AVG, COUNT, SUM`. Let's say we wanted to get the average `Citation_Count` for `ISSNs`. We can use `AVG` and the `GROUP BY` clause in a query:

~~~
SELECT ISSNs, AVG(Citation_Count)
FROM articles
GROUP BY ISSNs;
~~~
{: .sql}

GROUP BY is used by SQL to arrange identical data into groups. In this case, we are arranging all the citation counts by ISSNs. `AVG` acts on the `Citation_Count` in parentheses.

As you can see, it is difficult to tell though what ISSN has the highest average citation count and the least. We can improve upon the query above by using `ORDER BY` and `DESC`. 

~~~
SELECT ISSNs, AVG(Citation_Count) AS Avg_Citation_Count
FROM articles
GROUP BY ISSNs 
ORDER BY Avg_Citation_Count DESC;
~~~
{: .sql}

`AS` is used to create another column called `Avg_Citation_Count` to contain the calculations.

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
