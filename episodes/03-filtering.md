---
title: "Filtering"
teaching: 20
exercises: 10
questions:
- "How can I filter data?"
objectives:
- "Write queries that `SELECT` data based on conditions, such as `END`, `OR`, and `NOT`."
- "Understand how to use the `WHERE` clause in a statement."
- "Learn how to use comparison keywords such as `LIKE` in a statement."
keypoints:
- "Use `WHERE` to filter and retrieve data based on specific conditions."
- "Use `AND, OR, and NOT` to add additional conditions."
- "Use the comparison keyword `LIKE` and wildcard characters such as `%` to match patterns."
---


## Filtering

SQL is a powerful tool for filtering data in databases based on a set of conditions. Let's say we only want data for a specific ISSN, for instance, for the _Acta Crystallographica_ journal from the `articles` table. The journal has an ISSN code `2056-9890`.  To filter by this ISSN code, we will use the `WHERE` clause.

~~~
SELECT *
FROM articles
WHERE ISSNs='2056-9890';
~~~
{: .sql}


We can add additional conditions by using `AND`, `OR`, and/or `NOT`. For example, suppose we want the data on _Acta Crystallographica_ published after October:

~~~
SELECT *
FROM articles
WHERE (ISSNs='2056-9890') AND (Month > 10);
~~~
{: .sql}

Parentheses are used merely for readability in this case but can be required by the SQL interpreter in order to disambiguate formulas.

If we want to get data for the *Humanities* and *Religions* journals, which have
ISSNs codes "2076-0787" and "2077-1444", we can combine the tests using OR:

~~~
SELECT *
FROM articles
WHERE (issns = '2076-0787') OR (issns = '2077-1444');
~~~
{: .sql}

When you do not know the entire value you are searching for, you can use comparison keywords such as `LIKE`, `IN`, `BETWEEN...AND`, `IS NULL`. For instance, we can use `LIKE` in combination with `WHERE` to search for data that matches a pattern.

For example, using the `articles` table again, let's `SELECT` all of the data `WHERE` the `Subject` contains "Crystal Structure":

~~~
SELECT *
FROM articles
WHERE Subjects LIKE '%Crystal Structure%';
~~~
{: .sql}

You may have noticed the wildcard character `%`. It is used to match zero to many characters. So in the SQL statement above, it will match zero or more characters before and after 'Crystal Structure'. 

Let's see what variations of the term we got. Notice uppercase and lowercase, the addition of 's' at the end of structures, etc.

To learn more about other comparison keywords you can use, see Beginner SQL Tutorial on [SQL Comparison Keywords](https://beginner-sql-tutorial.com/sql-like-in-operators.htm).


> ## Challenge
> Write a query that returns the `Title`, `First_Author`, `Subjects`, `ISSNs`, `Month` and `Year`
> for all papers where `Subjects` contains "computer" and that have more than 4 citations.
>
> > ## Solution
> > ~~~
> > SELECT Title, First_Author, Subjects, ISSNs, Month, Year
> > FROM articles
> > WHERE (Subjects LIKE '%computer%') AND (Citation_Count > 4);
> > ~~~
> > {: .sql}
> {: .solution}
{: .challenge}

You can continue to add or chain conditions together and write more advanced queries.
