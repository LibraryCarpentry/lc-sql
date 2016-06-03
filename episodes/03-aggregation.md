---
title: "Aggregation"
teaching: 30
exercises: 30
questions:
- "Using queries to summmarise data"
objectives:
- "FIXME"
keypoints:
- "FIXME"
- "The code of conduct, license, Makefile, and contribution guidelines should not be modified."
- "The README, authors' list, and citation instructions must be updated for each lesson."
- "The home page, reference guide, setup instructions, discussion page, and instructors' guide must be updated for each lesson."
- "The Makefile stores commonly-used commands."
---

## `COUNT` and `GROUP BY`

Aggregation allows us to combine results by grouping records based on value and
calculating combined values in groups.

Let’s go to the articles table and find out how many entries there are.
Using the wildcard simply counts the number of records (rows)

~~~
SELECT COUNT(*)
FROM articles;
~~~
{: .source}

We can also find out how many authors have participated in these articles.

~~~
SELECT COUNT(*), SUM(author_count)
FROM articles;
~~~
{: .source}

There are many other aggregate functions included in SQL including
`MAX`, `MIN`, and `AVG`.

> ## Challenge
>
> Write a query that returns: total weight, average weight, and the min and
> max weights for all animals caught over the duration of the survey. Can you
> modify it so that it outputs these values only for weights between 5 and 10?
{: .challenge}

Now, let's see how many articles were published in each journal. We do this
using a `GROUP BY` clause

~~~
SELECT issns, COUNT( * )
FROM articles
GROUP BY issns;
~~~
{: .source}

`GROUP BY` tells SQL what field or fields we want to use to aggregate the data.
If we want to group by multiple fields, we give `GROUP BY` a comma separated list.

> ## Challenge
>
> Write queries that return:
>
> 1. How many individuals were counted in each year.
a) in total;
b) per each species.
> 2. Average weight of each species in each year.
Can you modify the above queries combining them into one?
{: .challenge}

## The `HAVING` keyword

In the previous lesson, we have seen the keywords `WHERE`, allowing to
filter the results according to some criteria. SQL offers a mechanism to
filter the results based on aggregate functions, through the `HAVING` keyword.

For example, we can adapt the last request we wrote to only return information
about articles with a 10 or more published articles:

~~~
SELECT issns, COUNT( * )
FROM articles
GROUP BY issns
HAVING COUNT( * ) >= 10;
~~~
{: .source}

The `HAVING` keyword works exactly like the `WHERE` keyword, but uses
aggregate functions instead of database fields.

If you use `AS` in your query to rename a column, `HAVING` can use this
information to make the query more readable. For example, in the above
query, we can call the `COUNT(*)` by another name, like
`occurrences`. This can be written this way:

~~~
SELECT issns, COUNT( * ) AS occurrences
FROM articles
GROUP BY issns
HAVING occurrences >= 10;
~~~
{: .source}

Note that in both queries, `HAVING` comes _after_ `GROUP BY`. One way to
think about this is: the data are retrieved (`SELECT`), can be filtered
(`WHERE`), then joined in groups (`GROUP BY`); finally, we only select some
of these groups (`HAVING`).

> ## Challenge
>
> Write a query that returns, from the `species` table, the number of
`genus` in each `taxa`, only for the `taxa` with more than 10 `genus`.
{: .challenge}

## Ordering aggregated results.

We can order the results of our aggregation by a specific column, including
the aggregated column.  Let’s count the number of articles published in each
journal, ordered by the count

~~~
SELECT issns, COUNT( * )
FROM articles
GROUP BY issns
ORDER BY COUNT( * ) DESC;
~~~
{: .source}

## Saving queries for future use

It is not uncommon to repeat the same operation more than once, for example
for monitoring or reporting purposes. SQL comes with a very powerful mechanism
to do this: views. Views are a form of query that is saved in the database,
and can be used to look at, filter, and even update information. One way to
think of views is as a table, that can read, aggregate, and filter information
from several places before showing it to you.

Creating a view from a query requires to add `CREATE VIEW viewname AS`
before the query itself. For example, if we want to save the query giving
the number of journals in a view, we can write

~~~
CREATE VIEW journal_counts AS
SELECT issns, COUNT(*)
FROM articles
GROUP BY issns;
~~~
{: .source}

Now, we will be able to access these results with a much shorter notation:

~~~
SELECT *
FROM journal_counts;
~~~
{: .source}

Assuming we do not need this view anymore, we can remove it from the database
almost as we would a table:

~~~
DROP VIEW journal_counts;
~~~
{: .source}

You can also add a view using _Create View_ in the _View_ menu and see the
results in the _Views_ tab just like a table

> ## Challenge
>
> Write a query that returns the number of each species
caught in each year sorted from most often caught species to the least
occurring ones within each year starting from the most recent records. Save
this query as a `VIEW`.
{: .challenge}