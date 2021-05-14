---
title: "Selecting and sorting data"
teaching: 15
exercises: 5
questions:
- "What is a query?"
- "How do you query databases using SQL?"
- "How do you retrieve unique values in SQL?"
- "How do you sort results in SQL?"
objectives:
- "Understand how SQL can be used to query databases"
- "Understand how to build queries, using SQL keywords such as `DISTINCT` and `ORDER BY`"
keypoints:
- "SQL is ideal for querying databases"
- "SQL queries have a basic query structure starting with `SELECT` field FROM table with additional keywords and criteria that can be used." 
---

## What is a query?
A query is a question or request for data. For example, "How many journals does our library subscribe to?" When we query a database, we can ask the same question using a common language called Structured Query Language or SQL in what is called a statement. Some of the most useful queries - the ones we are introducing in this first section - are used to return results from a table that match specific criteria.


## Writing my first query

Let's start by opening DB Browser for SQLite and the doaj-article-sample database (see Setup). Choose `Browse Data` and the `articles` table. The articles table contains columns or fields such as `Title`, `Authors`, `DOI`, `URL`, etc.

Let’s write a SQL query that selects only the `Title` column from the `articles` table.

~~~
SELECT title
FROM articles;
~~~
{: .sql}

## Capitalization and good style

In the first query above, we have capitalized the words `SELECT` and `FROM` because they are SQL keywords. Even though capitalization makes no difference to the SQL interpreter, capitalization of these SQL terms helps for readability and is therefore considered good style. As you write and expand your own queries, it might be helpful to pick an option, such as [CamelCase](https://en.wikipedia.org/wiki/Camel_case), and use that style when naming tables and columns. Some tables and columns require capitalization and some do not. An occasional change of capitalization for these table and column names may be needed. 

Example:

~~~
SELECT Title, Authors, ISSNs, Year
FROM Articles;
~~~

instead of 

~~~
SELECT Title, authors, ISSNs, Year
FROM articles;
~~~
{: .sql}

If we want more information, we can add a new column to the list of fields right after `SELECT`:

~~~
SELECT Title, Authors, ISSNs, Year
FROM articles;
~~~
{: .sql}

Or we can select all of the columns in a table using the wildcard `*`.

~~~
SELECT *
FROM articles;
~~~
{: .sql}

## Unique values

There may be a situation when you need to retrieve unique records and not multiple duplicate records. The SQL `DISTINCT` keyword is used after `SELECT` to eliminate duplicate records and fetch only unique records. Let's return all of the unique `ISSNs` in a SQL query.

~~~
SELECT DISTINCT ISSNs
FROM articles;
~~~
{: .sql}

Note, some database systems require a semicolon `;` after each SQL statement. If we select more than one column, then the distinct pairs of values are returned.

~~~
SELECT DISTINCT ISSNs, Day, Month, Year
FROM articles;
~~~
{: .sql}

## Sorting

We can also sort the results of our queries by using the keyword `ORDER BY`. Let's create a query that sorts the articles table alphabetically by ISSNs using the `ASC` keyword in conjunction with `ORDER BY`. 

~~~
SELECT *
FROM articles
ORDER BY ISSNs ASC;
~~~
{: .sql}

The keyword `ASC` tells us to order it in ascending order. Instead, we can use `DESC` to get the descending order sorting by `First_Author`.

~~~
SELECT *
FROM articles
ORDER BY First_Author DESC;
~~~
{: .sql}

`ASC` is the default, so by omitting `ASC` or `DESC`, SQLite will sort ascending (ASC).

We can also sort on several fields at once, in different directions. For example, we can order by `ISSNs` descending and then `First_Author` ascending in the same query.

~~~
SELECT *
FROM articles
ORDER BY ISSNs DESC, First_Author ASC;
~~~
{: .sql}

> ## Challenge
> Write a query that returns `Title`, `First_Author`, `ISSNs` and `Citation_Count` from
> the articles table, ordered by the top cited article and alphabetically by title.
>
> > ## Solution
> > ~~~
> > SELECT Title, First_Author, ISSNs, Citation_Count
> > FROM articles
> > ORDER BY Citation_Count DESC, Title ASC;
> > ~~~
> > {: .sql}
> {: .solution}
{: .challenge}
