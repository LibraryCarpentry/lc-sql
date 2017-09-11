---
title: "Joins and aliases"
teaching: 30
exercises: 30
questions:
- "Linking tables together and using shorthand"
objectives:
- "to understand how to link tables together"
keypoints:
- "SQL is ideal for linking tables"
---

## Joins

![](../assets/img/join.png)

To combine data from two tables we use the SQL `JOIN` command, which comes after
the `FROM` command.

We also need to tell the computer which columns provide the link between the two
tables using the word `ON`.  What we want is to join the data with the same
journal name.

~~~
SELECT *
FROM articles
JOIN journals
ON articles.issns = journals.issns;
~~~
{: .source}

`ON` is like `WHERE`, it filters things out according to a test condition.  We use
the `table.colname` format to tell the manager what column in which table we are
referring to.

Alternatively, we can use the word `USING`, as a short-hand.  In this case we are
telling the manager that we want to combine `articles` with `journals` and that
the common column is `issns`.

~~~
SELECT *
FROM articles
JOIN journals
USING (issns);
~~~
{: .source}

We often won't want all of the fields from both tables, so anywhere we would
have used a field name in a non-join query, we can use `table.colname`.

For example, what if we wanted information on published articles in different
journals, but instead of their ISSN we wanted the actual journal title.

~~~
SELECT articles.issns, journal_title, title, first_author, citation_count, author_count, month, year
FROM articles
JOIN journals
ON articles.issns = journals.issns;
~~~
{: .source}

Joins can be combined with sorting, filtering, and aggregation.  So, if we
wanted average number of authors for articles on different journals, we
could do something like

~~~
SELECT articles.issns, journal_title, ROUND(AVG(author_count), 2)
FROM articles
JOIN journals
ON articles.issns = journals.issns
GROUP BY articles.issns;
~~~
{: .source}

> ## Challenge
> Write a query that returns the journal title, total number of articles published
> and average number of citations for every journal.
>
> > ## Solution
> > ~~~
> > SELECT journal_title, count(*), avg(citation_count)
> > FROM articles
> > JOIN journals
> > ON articles.issns = journals.issns
> > GROUP BY articles.issns;
> > ~~~
> > {: .sql}
> {: .solution}
{: .challenge}


It is worth mentioning that you can join multiple tables. For example:
~~~
SELECT title, first_author, journal_title, publisher
FROM articles
JOIN journals
ON articles.issns = journals.issns
JOIN publishers
ON publishers.id = journals.publisherid;
~~~
{: .source}

> ## Challenge:
>
> Write a query that returns the journal title, publisher name, and number of
> articles published, ordered by number of articles in descending order.
>
> > ## Solution
> > ~~~
> > SELECT journal_title, publisher, count(*)
> > FROM articles
> > JOIN journals
> > ON articles.issns = journals.issns
> > JOIN publishers
> > ON publishers.id = journals.publisherid
> > GROUP BY journal_title
> > ORDER BY count(*) desc;
> > ~~~
> > {: .sql}
> {: .solution}
{: .challenge}


## Aliases

As queries get more complex names can get long and unwieldy. To help make things
clearer we can use aliases to assign new names to things in the query.

We can alias both table names:

~~~
SELECT ar.title, ar.first_author, jo.journal_title
FROM articles AS ar
JOIN journals  AS jo
ON ar.issns = jo.issns;
~~~
{: .source}
And column names:

~~~
SELECT ar.title AS title, ar.first_author AS author, jo.journal_title AS journal
FROM articles AS ar
JOIN journals  AS jo
ON ar.issns = jo.issns;
~~~
{: .source}

The `AS` isn't technically required, so you could do

~~~
SELECT a.title t
FROM articles a;
~~~
{: .source}

but using `AS` is much clearer so it is good style to include it.

## Extra Challenges (optional)

SQL queries help us *ask* specific *questions* which we want to answer about
our data. The real skill with SQL is to know how to translate our scientific
questions into a sensible SQL query (and subsequently visualize and interpret
our results).

Have a look at the following questions; these questions are written in plain
English. Can you translate them to *SQL queries* and give a suitable answer?

> ## Challenge 1
> How many plots from each type are there?
>
> > ## Solution 1
> > ~~~
> > SELECT first_author, COUNT( * ) AS n_articles
> > FROM articles
> > GROUP BY first_author
> > ORDER BY n_articles DESC;
> > ~~~
> > {: .sql}
> {: .solution}
{: .challenge}

> ## Challenge 2
> How many papers have a single author? How many have 2 authors? How many 3? etc?
>
> > ## Solution 2
> > ~~~
> > SELECT author_count, count( * )
> > FROM articles
> > GROUP BY author_count;
> > ~~~
> > {: .sql}
> {: .solution}
{: .challenge}

> ## Challenge 3
> How many articles are published for each language? (Ignore articles where
> language is unknown).
>
> > ## Solution 3
> > ~~~
> > SELECT language, count( * )
> > FROM articles
> > JOIN languages
> > ON articles.languageid=languages.id
> > WHERE language IS NOT null
> > GROUP BY language;
> > ~~~
> > {: .sql}
> {: .solution}
{: .challenge}

> ## Challenge 4
> How many articles are published for each licence type, and what is the average
> number of citations for that licence type
>
> > ## Solution 4
> > ~~~
> > SELECT licence, avg( citation_count ), count( * )
> > FROM articles
> > JOIN licences
> > ON articles.licenceid=licences.id
> > WHERE licence IS NOT null
> > GROUP BY licence;
> > ~~~
> > {: .sql}
> {: .solution}
{: .challenge}

> ## Challenge 5
> Select title, first_author, author_count, citation_count, month, year, journal_title, publisher
>
> > ## Solution 5
> > ~~~
> > SELECT title, first_author, author_count, citation_count, month, year, journal_title, publisher
> > FROM articles
> > JOIN journals
> > ON articles.issns=journals.issns
> > JOIN publishers
> > ON publishers.id=journals.publisherid;
> > ~~~
> > {: .sql}
> {: .solution}
{: .challenge}
