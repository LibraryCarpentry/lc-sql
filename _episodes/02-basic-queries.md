---
title: "Basic queries"
teaching: 25
exercises: 20
questions:
- "How do you query databases using SQL?"
objectives:
- "understand how SQL can be used to query databases"
keypoints:
- "SQL is ideal for querying databases"
---
## Writing my first query

Let's start by using the __articles__ table. Here we have data on every
article that has been published, including the title of the article, the
authors, date of publication, etc.

Let’s write an SQL query that selects only the title column from the
articles table.

~~~
SELECT title
FROM articles;
~~~
{: .sql}

We have capitalized the words SELECT and FROM because they are SQL keywords.
This makes no difference to the SQL interpreter as it is case-insensitive, but it helps for readability and is therefore considered good style.

If we want more information, we can add a new column to the list of fields,
right after `SELECT`:

~~~
SELECT title, authors, issns, year
FROM articles;
~~~
{: .sql}

Or we can select all of the columns in a table using the wildcard '*'

~~~
SELECT *
FROM articles;
~~~
{: .sql}

## Unique values

If we want only the unique values so that we can quickly see the ISSNs of
journals included in the collection, we use `DISTINCT`

~~~
SELECT DISTINCT issns
FROM articles;
~~~
{: .sql}

If we select more than one column, then the distinct pairs of values are
returned

~~~
SELECT DISTINCT issns, day, month, year
FROM articles;
~~~
{: .sql}

## Calculated values

We can also do calculations with the values in a query.
For example, if we wanted to look at the relative popularity of an article,
so we divide by 10 (because we know the most popular article has 10 citations).

~~~
SELECT first_author, citation_count/10.0
FROM articles;
~~~
{: .sql}

When we run the query, the expression `citation_count / 10.0` is evaluated for each
row and appended to that row, in a new column.  Expressions can use any fields,
any arithmetic operators (`+`, `-`, `*`, and `/`) and a variety of built-in
functions. For example, we could round the values to make them easier to read.

> Note that we divide by `10.0` and `16.0` instead of `10` and `16` to avoid losing the remainder.
> In SQLite, if you divide an integer by an integer, you get an integer, removing everything behind
> the decimal, making 9/10 = 0 instead of 0.9.

~~~
SELECT first_author, title, ROUND(author_count/16.0, 2)
FROM articles;
~~~
{: .sql}

> ## Challenge
> Write a query that returns the title, first_author, citation_count,
> author_count, month and year
>
> > ## Solution
> > ~~~
> > SELECT  title, first_author, citation_count, author_count, month, year
> > FROM articles;
> > ~~~
> > {: .sql}
> {: .solution}
{: .challenge}



## Filtering

Databases can also filter data – selecting only the data meeting certain
criteria.  For example, let’s say we only want data for a specific ISSN
for the _Theory and Applications of Mathematics & Computer Science_ journal,
which has a ISSN code 2067-2764|2247-6202.  We need to add a
`WHERE` clause to our query:

~~~
SELECT *
FROM articles
WHERE issns='2067-2764|2247-6202';
~~~
{: .sql}


We can use more sophisticated conditions by combining tests with `AND` and `OR`.
For example, suppose we want the data on _Theory and Applications of Mathematics
& Computer Science_ published after June:

~~~
SELECT *
FROM articles
WHERE (issns='2067-2764|2247-6202') AND (month > 06);
~~~
{: .sql}

Parentheses are used merely for readability in this case, but can be required to disambiguate formulas for the SQL interpreter.

If we wanted to get data for the *Humanities* and *Religions* journals, which have
ISSNs codes `2076-0787` and `2077-1444`, we could combine the tests using OR:

~~~
SELECT *
FROM articles
WHERE (issns = '2076-0787') OR (issns = '2077-1444');
~~~
{: .sql}

> ## Challenge
> Write a query that returns the title, first_author, issns, month and year
> for all single author papers with more than 4 citations
>
> > ## Solution
> > ~~~
> > SELECT title, first_author, issns, month, year
> > FROM articles
> > WHERE (author_count=1) and (citation_count>4);
> > ~~~
> > {: .sql}
> {: .solution}
{: .challenge}


## Building more complex queries

Now, lets combine the above queries to get data for the 3 journals from
June on.  This time, let’s use IN as one way to make the query easier
to understand.  It is equivalent to saying `WHERE (issns = '2076-0787') OR (issns
= '2077-1444') OR (issns = '2067-2764|2247-6202')`, but reads more neatly:

~~~
SELECT *
FROM articles
WHERE (month > 06) AND (issns IN ('2076-0787', '2077-1444', '2067-2764|2247-6202'));
~~~
{: .sql}

We started with something simple, then added more clauses one by one, testing
their effects as we went along.  For complex queries, this is a good strategy,
to make sure you are getting what you want.  Sometimes it might help to take a
subset of the data that you can easily see in a temporary database to practice
your queries on before working on a larger or more complicated database.

When the queries become more complex, it can be useful to add comments. In SQL,
comments are started by `--`, and end at the end of the line. For example, a
commented version of the above query can be written as:

~~~
-- Get post June data on selected journals
-- These are in the articles table, and we are interested in all columns
SELECT * FROM articles
-- Sampling month is in the column `month`, and we want to include
-- everything after June
WHERE (month > 06)
-- selected journals have the `issns` 2076-0787, 2077-1444, 2067-2764|2247-6202
AND (issns IN ('2076-0787', '2077-1444', '2067-2764|2247-6202'));
~~~
{: .sql}

Although SQL queries often read like plain English, it is *always* useful to add
comments; this is especially true of more complex queries.

## Sorting

We can also sort the results of our queries by using `ORDER BY`.
For simplicity, let’s go back to the articles table and alphabetize it by issns.

~~~
SELECT *
FROM articles
ORDER BY issns ASC;
~~~
{: .sql}

The keyword `ASC` tells us to order it in ascending order.
We could alternately use `DESC` to get descending order.

~~~
SELECT *
FROM articles
ORDER BY first_author DESC;
~~~
{: .sql}

`ASC` is the default, so by omiting ASC or DESC, SQLite will sort ASC (asceding).

We can also sort on several fields at once, in different directions.
For example, we can order by issns descending and then first_author ascending in the same query.

~~~
SELECT *
FROM articles
ORDER BY issns DESC, first_author ASC;
~~~
{: .sql}

> ## Challenge
> Write a query that returns title, first_author, issns and citation_count from
> the articles table, sorted with the most cited article at the top and
> alphabetically by title
>
> > ## Solution
> > ~~~
> > SELECT title, first_author, issns, citation_count
> > FROM articles
> > ORDER BY citation_count DESC, title ASC;
> > ~~~
> > {: .sql}
> {: .solution}
{: .challenge}


## Order of execution

Another note for ordering. We don’t actually have to display a column to sort by
it.  For example, let’s say we want to order the articles by their ISSN, but
we only want to see Authors and Titles.

~~~
SELECT authors, title
FROM articles
WHERE issns = '2067-2764|2247-6202'
ORDER first_author ASC;
~~~
{: .sql}

We can do this because sorting occurs earlier in the computational pipeline than
field selection.

The computer is basically doing this:

1. Filtering rows according to WHERE
2. Sorting results according to ORDER BY
3. Displaying requested columns or expressions.

Clauses are written in a fixed order: `SELECT`, `FROM`, `WHERE`, then `ORDER
BY`. It is possible to write a query as a single line, but for readability,
we recommend to put each clause on its own line.

> ## Challenge
> Let's try to combine what we've learned so far in a single
> query.  Using the articles table write a query to display the three date fields,
> `issns`, and `citation_count`, for articles published after June, ordered
> alphabetically by first author name. Write the query as a single line, then
> put each clause on its own line, and see how more legible the query becomes!
>
> > ## Solution
> > ~~~
> > SELECT title, authors, day, month, year, issns, citation_count
> > FROM articles
> > WHERE month>6
> > ORDER BY first_author;
> > ~~~
> > {: .sql}
> {: .solution}
{: .challenge}


