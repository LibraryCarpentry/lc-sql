---
title: Joins and aliases
teaching: 25
exercises: 20
---

::::::::::::::::::::::::::::::::::::::: objectives

- Understand how to link tables together via joins.
- Understand when it is valuable to use aliases or shorthand.

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: questions

- How do I join two tables if they share a common point of information?
- How can I use aliases to improve my queries?

::::::::::::::::::::::::::::::::::::::::::::::::::

## Joins

The SQL `JOIN` clause allows us to combine columns from one or more tables in a database by using values common to each. It follows the `FROM` clause in a SQL statement. We also need to tell the computer which columns provide the link between the two
tables using the word `ON`.

Let's start by joining data from the `articles` table with the `journals` table. The `ISSNs` columns in both these tables links them.

```sql
SELECT *
FROM articles
JOIN journals
ON articles.ISSNs = journals.ISSNs;
```

`ON` is similar to `WHERE`, it filters things out according to a test condition.  We use the `table.colname` format to tell the SQL manager what column in which table we are referring to.

We can represent `a LEFT` join using the following diagram.

![](fig/left-join-articles-journals_40.png){alt='Join Diagram for Example'}

Alternatively, we can use the word `USING`, as a short-hand.  In this case we are telling DB Browser that we want to combine `articles` with `journals` and that the common column is `ISSNs`.

```sql
SELECT *
FROM articles
JOIN journals
USING (ISSNs);
```

This figure shows the relations between the tables and helps to visualise joining or linking the tables in the database:
![](fig/articles-erd-v02.png){alt='Articles Database'}
We will cover [relational database design](08-database-design.md) in the next episode. In addition to visual above, *[SQL Join Types Explained Visually](https://dataschool.com/how-to-teach-people-sql/sql-join-types-explained-visually/)* provides visual/animated examples to help convey to learners what is happening in SQL `JOIN`s.

When joining tables, you can specify the columns you want by using `table.colname` instead of selecting all the columns using `*`. For example:

```sql
SELECT articles.ISSNs, journals.Journal_Title, articles.Title, articles.First_Author, articles.Month, articles.Year
FROM articles
JOIN journals
ON articles.ISSNs = journals.ISSNs;
```

Joins can be combined with sorting, filtering, and aggregation.  So, if we wanted the average number of authors for articles on each journal, we can use the following query:

```sql
SELECT articles.ISSNs, journals.Journal_Title, ROUND(AVG(articles.Author_Count), 2)
FROM articles
JOIN journals
ON articles.ISSNs = journals.ISSNs
GROUP BY articles.ISSNs;
```

The `ROUND` function allows us to round the `Author_Count` number returned by the `AVG` function by 2 decimal places.

:::::::::::::::::::::::::::::::::::::::  challenge

## Challenge

Write a query that `JOINS` the `articles` and `journals` tables and that returns the `Journal_Title`, total number of articles published and average number of citations for every journal ISSN.

:::::::::::::::  solution

## Solution

```sql
SELECT journals.Journal_Title, count(*), avg(articles.Citation_Count)
FROM articles
JOIN journals
ON articles.ISSNs = journals.ISSNs
GROUP BY articles.ISSNs;
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

You can also join multiple tables. For example:

```sql
SELECT articles.Title, articles.First_Author, journals.Journal_Title, publishers.Publisher
FROM articles
JOIN journals
ON articles.ISSNs = journals.ISSNs
JOIN publishers
ON publishers.id = journals.PublisherId;
```

:::::::::::::::::::::::::::::::::::::::  challenge

## Challenge:

Write a query that returns the `Journal_Title`, `Publisher` name, and number of
articles published, ordered by number of articles in descending order.

:::::::::::::::  solution

## Solution

```sql
SELECT journals.Journal_Title, publishers.Publisher, COUNT(*)
FROM articles
JOIN journals
ON articles.ISSNs = journals.ISSNs
JOIN publishers
ON publishers.id = journals.PublisherId
GROUP BY Journal_Title
ORDER BY COUNT(*) DESC;
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

There are different types of joins which you can learn more about at [SQL Joins Explained](https://www.geeksforgeeks.org/sql-join-set-1-inner-left-right-and-full-joins/).

## Aliases

As queries get more complex, names can get long and unwieldy. To help make things clearer we can use aliases to assign new names to items in the query.

We can alias both table names:

```sql
SELECT ar.Title, ar.First_Author, jo.Journal_Title
FROM articles AS ar
JOIN journals  AS jo
ON ar.ISSNs = jo.ISSNs;
```

And column names:

```sql
SELECT ar.title AS title, ar.first_author AS author, jo.journal_title AS journal
FROM articles AS ar
JOIN journals  AS jo
ON ar.issns = jo.issns;
```

The `AS` isn't technically required, so you could do:

```sql
SELECT a.Title t
FROM articles a;
```

But using `AS` is much clearer so it is good style to include it.

:::::::::::::::::::::::::::::::::::::::: keypoints

- Joining two tables in SQL is an good way to analyse datasets, especially when both datasets provide partial answers to questions you want to ask.
- Creating aliases allows us to spend less time typing, and more time querying!

::::::::::::::::::::::::::::::::::::::::::::::::::


