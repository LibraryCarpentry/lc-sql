---
title: "Introduction to SQL"
teaching: 15
exercises: 0
questions:
- "What is SQL?"
- "Why is it significant?"
- "What is the relationship between a relational database and SQL?"
objectives:
- "define a relational database"
- "name the major components of relational database design"
- "explain what SQL is and why to use it"
- "identify library skills that translate to using SQL"
keypoints:
- "SQL is a powerful language used to interrogate and manipulate relational databases"
- "Librarians have skills that allow them to transition into using SQL to organize and access data"
---



## What is SQL?

**S**tructured **Q**uery **L**anguage, or SQL (sometimes pronounced "sequel"), is a powerful language used to interrogate and
manipulate relational databases. It is not a general
programming language that you can use to write an entire program. However, SQL
queries can be called from programming languages to let any program work
with databases. There are several different variants of SQL, but all support the
same basic statements that we will be covering today.

## Relational databases

Relational databases consist of one or more tables of data. These tables have
_fields_ (columns) and _records_ (rows). Every field has a data _type_. Every
value in the same field of each record has the same _type_. These tables can be
linked to each other when a field in one table can be matched to a field in another
table. SQL _queries_ are the commands that let you look up data in a database or
make calculations based on columns.

## Why use SQL

Using SQL lets you keep the data separate from the analysis. There is no risk of
accidentally changing data when you are analysing it. If the data is changed,
a saved query can be re-run to analyse the new data.

SQL is optimised for handling large amounts of data. Data types help
quality control of entries - you will receive an error if you try to enter a word
into a field that should contain a number. Understanding the nature of relational
databases, and using SQL, will help you in using databases in programming languages
and in doing similar things using programming languages such as R or Python.

## Why are Librarians well suited to SQL?
Librarianship is about information management. We help sort and organise
information and we help people find information. Most of us go through mediated queries
to help people find the information they need e.g. conducting a search via
a library catalogue. With SQL, you can directly construct your database queries
without the constraints (e.g. field name or search limitations) imposed by
a mediated search interface. Librarians are good at searching information so
don’t be afraid – constructing queries using SQL is simply a different and more
direct way of finding information. 

## Database Management Systems

There are a number of different database management systems for working with
relational data. We're going to use SQLite today, but basically everything we
teach you will apply to the other database systems as well (e.g., MySQL,
PostgreSQL, MS Access, Filemaker Pro). The only things that will differ are the
details of exactly how to import and export data and possibly some differences in datatype.

## Database Design

* Every row-column combination contains a single _atomic_ value, i.e., not
   containing parts we might want to work with separately.
* One field per type of information
* No redundant information
    * Split into separate tables with one table per class of information
    * Needs an identifier in common between tables – shared column - to
       reconnect (foreign key).

## Introduction to SQLite Manager

Let's all open the database we downloaded in SQLite Manager by clicking on the
open file icon.

You can see the tables in the database by looking at the left hand side of the
screen under Tables.

To see the contents of a table, click on that table and then click on the Browse
and search tab in the right hand section of the screen.

If we want to write a query, we click on the Execute SQL tab.


## Dataset Description

The data we will be using consists of 5 csv files that contain tables of article titles, journals, languages, licenses, and publishers. The information in these tables are from a sample of 51 different journals published during 2015.

'articles.csv' 
* Contains individual article Titles and the associated citations and metadata
* (16 fields, 1001 records)
* Field names: `id`, `Title`, `Authors`, `DOI`, `URL`, `Subjects`, `ISSNs`, `Citation`, `LanguageID`, `LicenseID`, `Author_Count`, `First_Author`, `Citation_Count`, `Day`, `Month`, `Year`

'journals.csv'
* Contains various journal Titles and associated metadata. The table also associates Journal Titles with ISSN numbers that are then referenced in the 'articles' table by the `ISSNs` field.
* (5 fields, 51 records)
* Field names: `id`, `ISSN-L`,`ISSNs`, `PublisherID`, `Journal_Title`

'languages.csv'
* ID table which associates language codes with id numbers. These id numbers are then referenced in the 'articles' table by the `LanguageID` field.
* (2 fields, 4 records)
* Field names: `id`, `Language`

'licenses.csv'
* ID table which associates License codes with id numbers. These id numbers are then referenced in the 'articles' table by the `LicenseID` field.
* (2 fields, 4 records)
* Field names: `id`, `Licence`

'publishers.csv'
* ID table which associates Publisher names with id numbers. These id numbers are then referenced in the 'journals' table by the `PublisherID` field.
* (2 fields, 6 records)
* Field names: `id`, `Publisher`


## A Note About Data Types

| Data type                          | Description                                                                                              |
|------------------------------------|:---------------------------------------------------------------------------------------------------------|
| CHARACTER(n)                       | Character string. Fixed-length n                                                                         |
| VARCHAR(n) or CHARACTER VARYING(n) | Character string. Variable length. Maximum length n                                                      |
| BINARY(n)                          | Binary string. Fixed-length n                                                                            |
| BOOLEAN                            | Stores TRUE or FALSE values                                                                              |
| VARBINARY(n) or BINARY VARYING(n)  | Binary string. Variable length. Maximum length n                                                         |
| INTEGER(p)                         | Integer numerical (no decimal).                                                                          |
| SMALLINT                           | Integer numerical (no decimal).                                                                          |
| INTEGER                            | Integer numerical (no decimal).                                                                          |
| BIGINT                             | Integer numerical (no decimal).                                                                          |
| DECIMAL(p,s)                       | Exact numerical, precision p, scale s.                                                                   |
| NUMERIC(p,s)                       | Exact numerical, precision p, scale s. (Same as DECIMAL)                                                 |
| FLOAT(p)                           | Approximate numerical, mantissa precision p. A floating number in base 10 exponential notation.          |
| REAL                               | Approximate numerical                                                                                    |
| FLOAT                              | Approximate numerical                                                                                    |
| DOUBLE PRECISION                   | Approximate numerical                                                                                    |
| DATE                               | Stores year, month, and day values                                                                       |
| TIME                               | Stores hour, minute, and second values                                                                   |
| TIMESTAMP                          | Stores year, month, day, hour, minute, and second values                                                 |
| INTERVAL                           | Composed of a number of integer fields, representing a period of time, depending on the type of interval |
| ARRAY                              | A set-length and ordered collection of elements                                                          |
| MULTISET                           | A variable-length and unordered collection of elements                                                   |
| XML                                | Stores XML data                                                                                          |


## SQL Data Type Quick Reference

Different databases offer different choices for the data type definition.

The following table shows some of the common names of data types between the various database platforms:

| Data type                                               | Access                    | SQLServer            | Oracle             | MySQL          | PostgreSQL    |
|:--------------------------------------------------------|:--------------------------|:---------------------|:-------------------|:---------------|:--------------|
| boolean                                                 | Yes/No                    | Bit                  | Byte               | N/A            | Boolean       |
| integer                                                 | Number (integer)          | Int                  | Number             | Int / Integer  | Int / Integer |
| float                                                   | Number (single)           | Float / Real         | Number             | Float          | Numeric       |
| currency                                                | Currency                  | Money                | N/A                | N/A            | Money         |
| string (fixed)                                          | N/A                       | Char                 | Char               | Char           | Char          |
| string (variable)                                       | Text (<256) / Memo (65k+) | Varchar              | Varchar / Varchar2 | Varchar        | Varchar       |
| binary object	OLE Object Memo	Binary (fixed up to 8K)   | Varbinary (<8K)           | Image (<2GB)	Long | Raw	Blob          | Text	Binary | Varbinary     |

