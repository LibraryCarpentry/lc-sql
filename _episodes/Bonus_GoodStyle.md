---
title: "Good Style"
teaching: 10
exercises: 0
questions:
- "What is good SQL Style, and how can I abide by SQL conventions?"
objectives:
- "Understand the foundation for making clean, readable SQL queries."
keypoints:
- "There are many ways to write an SQL queries, but some look better than others."
---

## An Introduction to good style

There are many ways to write an SQL queries, but some look better than others. Abiding by good style guidelines will make your SQL queries easier to read, especially if you are sharing them with others.
These are some quick tips for making your SQL look clean.

## Pick column names that are precise and short

When choosing column names, it's important to remember that a large part of what you type in your query will be composed of your column names. Choosing a column name that is one or two words (without any spaces!) will ensure that your queries are easier to type and read. If you include spaces in your column names, you will get an error message when you try to run your queries, so we would recommend using CamelCase, or An_Underscore.

## Capitalization (sometimes) matters

In section two, we talked about SQL keywords/commands being case-insensitive ("We have capitalised the words SELECT and FROM because they are SQL keywords. This makes no difference to the SQL interpreter as it is case-insensitive, but it helps for readability and is therefore considered good style."). But did you know that in some SQL programs, depending on the settings, table and column names are column sensitive? If your query isn't working, check the capitalization.

## Readability

As you may have noticed, we are able to write our query on one line, or on many. The general consensus with SQL is that if you can break it into components on multiple lines, it becomes easier to read. Using multiple lines and indenting, you can turn something that looks like this:

~~~
SELECT articles.Title, articles.First_Author, journals.Journal_Title, publishers.Publisher FROM articles JOIN journals ON articles.ISSNs = journals.ISSNs JOIN publishers ON publishers.id = journals.PublisherId;
~~~
{: .sql}

Into something that looks like this:

~~~
SELECT articles.Title, articles.First_Author, journals.Journal_Title, publishers.Publisher
FROM articles
JOIN journals
ON articles.ISSNs = journals.ISSNs
JOIN publishers
ON publishers.id = journals.PublisherId;
~~~
{: .sql}

In some programs (such as MySQL), there will be tools that can automatically "beautify" your code for better readability.

{: .sql}
