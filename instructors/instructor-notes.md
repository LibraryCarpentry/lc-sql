---
title: Instructors' Guide
---

***

# Tips and Tricks

***

## Making a handout

To make a handout for this lesson, adapt/print from [https://librarycarpentry.org/lc-sql/reference](https://librarycarpentry.org/lc-sql/reference).

***

# General notes of SQL

> **database** (dā'tə-bās') noun:
> "A collection of data arranged for ease and speed of search and retrieval by a computer"
> 
> — The American Heritage® Science Dictionary
> {: .quotation}

- Three common options for storing data
- Text
  - Easy to create, work well with version control
  - But then we have to build search and analysis tools ourselves
- Spreadsheets
  - Good for simple analyses
  - But don't handle large or complex data sets well
- Databases
  - Include powerful tools for search and analysis
  - Can handle large, complex data sets.

## Overall

- Libraries often start off with spreadsheet-based projects and there are a number of examples provided in the [Introduction to SQL](01-introduction.md) where they might move to a database and use SQL. The *What are some of the uses of SQL in libraries* section can be possibly turned into a group exercise where workshop participants can share some projects that can benefit from moving to a database.

- If you are short on time, consider pointing workshop participants to the [Ordering and commenting](04-ordering-commenting.md) and [Saving queries](07-saving-queries.md) episodes to refer to later.

- The [Extra challenges](11-extra-challenges.md) episode is optional if workshop participants want to try additional challenge exercises later. Depending on time it can be done as homework or at the end of a workshop.

- [Database design](08-database-design.md) episode can be positioned at the start, during, at the end of the lesson. It adds more time and can be a more complex episode to teach but it also helps with providing further background on how databases can be helpful with structured data.

- Some advanced learners may have heard that NoSQL databases (i.e., ones that don't use the relational model) are the next big thing, and ask why we're not teaching those.
  The answers are:
  
  1. Relational databases are far more widely used than NoSQL databases.
  2. We have far more experience with relational databases than with any other kind,
    so we have a better idea of what to teach and how to teach it.
  3. NoSQL databases are as different from each other as they are from relational databases.
    Until a leader emerges, it isn't clear *which* NoSQL database we should teach.

## Import CSV in SQLite

For instructors demonstrating the use of SQLite, [Aaron Culich](https://github.com/aculich) recommends using a [Directory of Open Access Journals (DOAJ)](https://doaj.org/) example, importing a dataset CSV file from the CERN repository [Zenodo](https://zenodo.org/). The example is below:

```bash
$ sqlite3 output.db
sqlite> .mode csv
sqlite> .import dataset-final-20160825-zenodo.csv
sqlite> .schema
```

## Resources

- Where to go for more SQL tutorials: [https://brohrer.github.io/sql\_resources.html](https://brohrer.github.io/sql_resources.html).
- Software Carpentry has some starter lesson material on interacting with databases with [Python](https://swcarpentry.github.io/sql-novice-survey/10-prog) and [R](https://swcarpentry.github.io/sql-novice-survey/11-prog-R).


