---
title: "Introduction to SQL"
teaching: 15
exercises: 0
questions:
- "What is SQL?"
- "Why is it significant?"
- "What is the relationship between a relational database and SQL?"
objectives:
- "Define a relational database."
- "Explain what SQL is and why to use it."
- "Identify library and information skills that relate to using SQL"
keypoints:
- "SQL is a powerful language used to interrogate and manipulate relational databases."
- "People working in library- and information-related roles have skills that allow them to use SQL to organize and access data."
---



## What is SQL?

**S**tructured **Q**uery **L**anguage, or SQL (sometimes pronounced "sequel"), is a powerful language used to interrogate and
manipulate relational databases. It is not a general 
programming language that you can use to write an entire program. However, SQL
queries can be called from programming languages to let any program interact
with databases. There are several variants of SQL, but all support the
same basic statements that we will be covering today.

## Relational databases

Relational databases consist of one or more tables of data. These tables have
_fields_ (columns) and _records_ (rows). Every field has a data _type_. Every
value in the same field of each record has the same _type_. These tables can be
linked to each other when a field in one table can be matched to a field in another
table. SQL _queries_ are the commands that let you look up data in a database or
make calculations based on columns.

## Why use SQL?

SQL is well established and has been around since the 1970s. It is still widely used 
in a variety of settings. 

SQL lets you keep the data separate from the analysis. There is no risk of
accidentally changing data when you are analysing it. If the data is changed,
a saved query can be re-run to analyse the new data.

SQL is optimised for handling large amounts of data. Data types help
quality control of entries - you will receive an error if you try to enter a word
into a field that should contain a number. Understanding the nature of relational
databases, and using SQL, will help you in using databases in programming languages 
such as R or Python.

Many web applications (including WordPress and ecommerce sites like Amazon) run on a SQL (relational) database. Understanding SQL is the first step in eventually building custom web applications that can serve data to users.

## Why are people working in library- and information-related roles well suited to SQL?
Librarianship is about information management. As librarians, we help sort and organise
information, and we help people find information. Most of us go through mediated queries
to help people find the information they need, e.g., we assist with or conduct a search via
a library catalogue. With SQL, you can directly construct your database queries
without the constraints (e.g., field name or search limitations) imposed by
a mediated search interface. Librarians are good at searching information – constructing queries using SQL is simply a different and more
direct way of finding information. 

> ## What are some of the uses for SQL in libraries?
> 
> * You can use SQL to make macro or large scale changes to metadata records in library databases, for instance, updating journal names so that they are consistent or normalised throughout the database.
> 
> * For situations where you have to interact with database administrators in your library or wider organisation, you can learn the fundamentals of SQL to become more fluent in the terminology.
> 
> * Because SQL querying is similar to natural language queries, you can use it to organise a variety of projects (e.g. programme evaluation) and ask questions of the data before going on to use other data analysis tools.
> 
> * You can use SQL to query your library database and explore new views that are not necessarily provided via library systems patron facing interfaces.
> 
> * SQL can be used to keep an inventory of items, for instance, for a library's makerspace, or it can be used to track licenses for journals.
> 
> * For projects involving migrating and cleaning data from one system to another, SQL can be a handy tool.
> 
> * With spreadsheets of data scattered throughout folders, SQL can be a useful tool for connecting this data and bringing it together in a database or central data warehouse where it can be accessible to different roles in the library and queried in one place.
> 
> * It can also help with initial exposure with interacting with a system, in preparation for interacting with a application programming interface or API later on.
> 
> In addition, you can read about these two perspectives:
> 
> * [An Introduction to SQL for Librarians](http://ruthtillman.com/an-introduction-to-sql-for-librarians/)
> 
> * [Data Science is Different Now: Learn SQL](https://veekaybee.github.io/2019/02/13/data-science-is-different/)
>
{: .callout}

## Database Management Systems

There are a number of different database management systems for working with
relational data. We're going to use SQLite today, but basically everything we
teach you will apply to the other database systems as well (e.g., MySQL,
PostgreSQL, MS Access, Filemaker Pro). The only things that will differ are the
details of exactly how to import and export data and possibly some differences in datatype.

## Introduction to DB Browser for SQLite

Let's all open the database we downloaded via the setup in DB Browser for SQLite.

You can see the tables in the database by looking at the left hand side of the
screen under Tables.

To see the contents of a table, click on that table and then click on the Browse 
Data tab above the table data.

If we want to write a query, we click on the Execute SQL tab.

There are two ways to add new data to a table without writing SQL: 

1. Enter data into a CSV file and append	
2. Click the "Browse Data" tab, then click the "New Record" button.

The steps for adding data from a CSV file are:

1. Choose "File" > "Import" > "Table" from CSV file... 
2. DB Browser for SQLite will prompt you if you want to add the data to the existing table.


## Dataset Description

The data we will be using consists of 5 csv files that contain tables of article titles, journals, languages, licenses, and publishers. The information in these tables are from a sample of 51 different journals published during 2015.

__articles__  
* Contains individual article Titles and the associated citations and metadata
* (16 fields, 1001 records)
* Field names: `id`, `Title`, `Authors`, `DOI`, `URL`, `Subjects`, `ISSNs`, `Citation`, `LanguageID`, `LicenseID`, `Author_Count`, `First_Author`, `Citation_Count`, `Day`, `Month`, `Year`

__journals__  
* Contains various journal Titles and associated metadata. The table also associates Journal Titles with ISSN numbers that are then referenced in the 'articles' table by the `ISSNs` field.
* (5 fields, 51 records)
* Field names: `id`, `ISSN-L`,`ISSNs`, `PublisherID`, `Journal_Title`

__languages__  
* ID table which associates language codes with id numbers. These id numbers are then referenced in the 'articles' table by the `LanguageID` field.
* (2 fields, 4 records)
* Field names: `id`, `Language`

__licenses__  
* ID table which associates License codes with id numbers. These id numbers are then referenced in the 'articles' table by the `LicenseID` field.
* (2 fields, 4 records)
* Field names: `id`, `Licence`

__publishers__  
* ID table which associates Publisher names with id numbers. These id numbers are then referenced in the 'journals' table by the `PublisherID` field.
* (2 fields, 6 records)
* Field names: `id`, `Publisher`


## A Note About Data Types

The main data types that are used in doaj-article-sample database are `INTEGER` and `TEXT` which define what value the table column can hold. 


## SQL Data Type Quick Reference

Different database software/platforms have different names and sometimes different definitions of data types, so you'll need to understand the data types for any platform you are using.  The following table explains some of the common data types and how they are represented in SQLite; [more details available on the SQLite website](https://www.sqlite.org/datatype3.html).

| Data type      | Details                                                                                 | Name in SQLite            |
|:---------------|:----------------------------------------------------------------------------------------|:--------------------------|
| boolean or binary | this variable type is often used to represent variables that can only have two values: yes or no, true or false.  |doesn't exist - need to use integer data type and values of 0 or 1.|
| integer | sometimes called whole numbers or counting numbers.  Can be 1,2,3, etc., as well as 0 and negative whole numbers: -1,-2,-3, etc.|INTEGER|
| float, real, or double | a decimal number or a floating point value.  The largest possible size of the number may be specified. |REAL|
| text or string |and combination of numbers, letters, symbols.  Platforms may have different data types: one for variables with a set number of characters - e.g., a zip code or postal code, and one for variables with an open number of characters, e.g., an address or description variable. |TEXT|
|date or datetime|depending on the platform, may represent the date and time or the number of days since a specified date.  This field often has a specified format, e.g., YYYY-MM-DD|doesn't exist - need to use built-in date and time functions and store dates in real, integer, or text formats.  See [Section 2.2 of SQLite documentation](https://www.sqlite.org/datatype3.html#date_and_time_datatype) for more details.
| blob | a Binary Large OBject can store a large amount of data, documents, audio or video files.|BLOB|
