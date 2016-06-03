---
title: "Joins and aliases"
teaching: 30
exercises: 30
questions:
- "Linking tables together and using shorthand"
objectives:
- "FIXME"
keypoints:
- "FIXME"
---

## Joins

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

> ## Challenge:
>
> Write a query that returns the genus, the species, and the weight
> of every individual captured at the site.
{: .challenge}

Joins can be combined with sorting, filtering, and aggregation.  So, if we
wanted average number of authors for articles on different journals, we
could do something like

~~~
SELECT articles.issns, journal_title, ROUND(AVG(author_count), 2)
FROM articles
JOIN journals
ON articles.issns = journals.issns;
GROUP BY articles.issns;
~~~
{: .source}

It is worth mentioning that you can join multiple tables. For example:

SELECT title, first_author, journal_title, language
FROM articles
JOIN journals
ON articles.issns = journals.issns
JOIN languages
ON languages.id = articles.languageid

> ## Challenge:
>
> Write a query that returns the number of genus of the animals caught in each
> plot in descending order.
{: .challenge}

> ## Challenge:
>
> Write a query that finds the average weight of each rodent species
> (i.e., only include species with Rodent in the taxa field).
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
{: .challenge}

> ## Challenge 2
> How many specimens are of each gender are there for each year?  
{: .challenge}

> ## Challenge 3 
> How many specimens of each species were captured in each type of plot?  
{: .challenge}

> ## Challenge 4 
> What is the average weight of each taxa?  
{: .challenge}

> ## Challenge 5
> What is the percentage of each species in each taxa?  
{: .challenge}

> ## Challenge 6
> What are the minimum, maximum and average weight for each species of Rodent?  
{: .challenge}

> ## Challenge 7 
> What is the hindfoot length for male and female rodent of each species?
> Is there a Male / Female difference?  
{: .challenge}

> ## Challenge 8
> What is the average weight of each rodent species over the course of the years?
> Is there any noticeable trend for any of the species?  
{: .challenge}

Proposed solutions:

> ## Solution 1
> ~~~
> `SELECT plot_type, count(*) AS num_plots  FROM plots  GROUP BY plot_type  ORDER BY num_plots DESC`
> ~~~
{: .solution}

> ## Solution 2
> ~~~
> `SELECT year, sex, count(*) AS num_animal  FROM surveys  WHERE sex IS NOT null  GROUP BY sex, year`
> ~~~
{: .solution}

> ## Solution 3
> ~~~
> `SELECT species_id, plot_type, count(*) FROM surveys JOIN plots ON surveys.plot_id=plots.plot_id WHERE species_id IS NOT null GROUP BY species_id, plot_type`
> ~~~
{: .solution}

> ## Solution 4
> ~~~
> `SELECT taxa, AVG(weight) FROM surveys JOIN species ON species.species_id=surveys.species_id GROUP BY taxa`
> ~~~
{: .solution}

> ## Solution 5
> ~~~
> `SELECT taxa, 100.0*count(*)/(SELECT count(*) FROM surveys) FROM surveys JOIN species ON surveys.species_id=species.species_id GROUP BY taxa`
> ~~~
{: .solution}

> ## Solution 6
> ~~~
> `SELECT surveys.species_id, MIN(weight) as min_weight, MAX(weight) as max_weight, AVG(weight) as mean_weight FROM surveys JOIN species ON surveys.species_id=species.species_id WHERE taxa = 'Rodent' GROUP BY surveys.species_id`
> ~~~
{: .solution}

> ## Solution 7
> ~~~
> `SELECT surveys.species_id, sex, AVG(hindfoot_length) as mean_foot_length  FROM surveys JOIN species ON surveys.species_id=species.species_id WHERE taxa = 'Rodent' AND sex IS NOT NULL GROUP BY surveys.species_id, sex`
> ~~~
{: .solution}

> ## Solution 8
> ~~~
> `SELECT surveys.species_id, year, AVG(weight) as mean_weight FROM surveys JOIN species ON surveys.species_id=species.species_id WHERE taxa = 'Rodent' GROUP BY surveys.species_id, year`
> ~~~
{: .solution}