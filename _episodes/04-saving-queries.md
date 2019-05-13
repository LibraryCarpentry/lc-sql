---
title: "Saving queries"
teaching: 20
exercises: 10
questions:
- "How can I save a query for future use?"
- "How can I remove a saved query?"
objectives:
- "Learn how to save repeated queries as 'Views' and how to drop them."
keypoints:
- "Saving queries as 'Views' allows you to save time and avoid repeating the same operation more than once."
---

## Saving queries for future use

It is not uncommon to repeat the same operation more than once, for example
for monitoring or reporting purposes. SQL comes with a very powerful mechanism
to do this: views. Views are queries saved in the database. You query it as a 
(virtual) table that is populated every time you query it.

Creating a view from a query requires you to add `CREATE VIEW viewname AS`
before the query itself. For example, if we want to save the query giving
the number of journals in a view, we can write:

~~~
CREATE VIEW journal_counts AS
SELECT issns, COUNT(*)
FROM articles
GROUP BY issns;
~~~
{: .sql}

Now, we will be able to access these results with a much shorter notation:

~~~
SELECT *
FROM journal_counts;
~~~
{: .sql}

Assuming we do not need this view anymore, we can remove it from the database
almost as we would a table:

~~~
DROP VIEW journal_counts;
~~~
{: .sql}

In DBBrowser for SQLite, you can also create a view from any query by omitting 
the `CREATE VIEW viewname AS` statement and instead, clicking the small Save 
icon at the bottom of the Execute SQL tab and then clicking __Save as view__. 
Whatever method you use to create a view, it will appear in the list of views 
under the Database Structure tab.


> ## Challenge
>
> Write a query that returns the number of articles published in each journal
> on each month, sorted from most popular journal to the ones with least
> publications each month starting from the most recent records. Save this
> query as a `VIEW`.
>
> > ## Solution
> > ~~~
> > CREATE VIEW journal_counts AS
> > SELECT COUNT(*), month
> > FROM articles
> > GROUP BY issns, month
> > ORDER BY  count(*) desc, month desc;
> > ~~~
> > {: .sql}
> {: .solution}
{: .challenge}

