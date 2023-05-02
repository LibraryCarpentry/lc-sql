---
title: Ordering and commenting
teaching: 15
exercises: 0
---

::::::::::::::::::::::::::::::::::::::: objectives

- Understand how to build queries, and the order in which to build the parts.

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: questions

- What is the order of execution in SQL queries?
- How can you organize and comment more complex SQL queries?

::::::::::::::::::::::::::::::::::::::::::::::::::

## Order of execution

Let's say we had the following query:

```sql
SELECT Title, Authors
FROM articles
WHERE ISSNs = '2067-2764|2247-6202'
ORDER BY First_Author ASC;
```

What is interesting to note about this query is that we don't necessarily have to display the `First_Author` column in our results in order to sort by it.

We can do this because sorting occurs earlier in the computational pipeline than field selection.

:::::::::::::::::::::::::::::::::::::::::  callout

## The computer is basically doing this:

1. Filtering rows according to WHERE
2. Sorting results according to ORDER BY
3. Displaying requested columns or expressions.

::::::::::::::::::::::::::::::::::::::::::::::::::

Clauses are written in a fixed order: `SELECT`, `FROM`, `WHERE`, then `ORDER BY`. It is possible to write a query as a single line, but for readability, we recommend to put each clause on its own line.

## Complex queries \& commenting

The goal is to make a query easy to read and understand, even when the logic becomes complex. This can be handled in two ways:

1. Rewriting the query so that the logic is easy to follow
2. Adding comments for context and clarity.

Consider the following query:

```sql
SELECT *
FROM articles
WHERE (ISSNs = '2076-0787') OR (ISSNs = '2077-1444') OR (ISSNs = '2067-2764|2247-6202');
```

SQL offers the flexibility of iteratively adding new conditions but you may reach a point where the query is difficult to read and inefficient. For instance, we can use `IN` to improve the query and make it more readable:

```sql
SELECT *
FROM articles
WHERE (ISSNs IN ('2076-0787', '2077-1444', '2067-2764|2247-6202'));
```

We started with something simple, then added more clauses one by one, testing
their effects as we went along.  For complex queries, this is a good strategy, to make sure you are getting what you want.  Sometimes it might help to take a subset of the data that you can easily see in a temporary database to practice your queries on before working on a larger or more complicated database.

When the queries become more complex, it can be useful to add comments to express to yourself, or to others, what you are doing with your query. Comments help explain the logic of a section and provide context for anyone reading the query. It's essentially a way of making notes within your SQL. In SQL, comments begin using <code class="language-plaintext highlighter-rouge">\--</code> and end at the end of the line. To mark a whole paragraph as a comment, you can enclose it with the characters /\* and \*/. For example, a commented version of the above query can be written as:

```
/*In this section, even though JOINS (see link below this code block) are not introduced until Episode 6, we want to give an example how to
join multiple tables becasue they represent a good example of using comments in SQL to explain more complex queries.*/

-- First we mention all the fields we want to display
SELECT articles.Title, articles.First_Author, journals.Journal_Title, publishers.Publisher
-- from the first table
FROM articles
-- and join it with the second table.
JOIN journals
-- The related attributes are:
ON articles.ISSNs = journals.ISSNs
-- We want to join a third table,
JOIN publishers
-- the related attributes are:
ON publishers.id = journals.PublisherId;
```

To see the introduction and explanation of JOINS, please click to [Episode 6](06-joins-aliases.md).
{: .sql}

:::::::::::::::::::::::::::::::::::::::: keypoints

- Queries often have the structure: SELECT data FROM table WHERE certain criteria are present.

::::::::::::::::::::::::::::::::::::::::::::::::::


