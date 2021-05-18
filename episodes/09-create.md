---
title: "Creating tables and modifying data"
teaching: 15
exercises: 10
questions:
- "How can I create, modify, and delete tables and data?"
objectives:
- "Write statements that create tables."
- "Write statements to insert, modify, and delete records."
keypoints:
- "Use CREATE and DROP to create and delete tables."
- "Use INSERT to add data."
- "Use UPDATE to modify existing data."
- "Use DELETE to remove data."
- "It is simpler and safer to modify data when every record has a unique primary key."
- "Do not create dangling references by deleting records that other records refer to."
---
So far we have only looked at how to get information out of a database,
both because that is more frequent than adding information,
and because most other operations only make sense
once queries are understood.
If we want to create and modify data,
we need to know two other sets of commands.

The first pair are [`CREATE TABLE`][create-table] and [`DROP TABLE`][drop-table].
While they are written as two words,
they are actually single commands.
The first one creates a new table;
its arguments are the names and types of the table's columns.
For example,
the following statement creates the table `journals`:

~~~
CREATE TABLE journals(id text, ISSN-L text, ISSNs text, PublisherId text, Journal_Title text);
~~~
{: .sql}

We can get rid of one of our tables using:

~~~
DROP TABLE journals;
~~~
{: .sql}

Be very careful when doing this:
if you drop the wrong table, hope that the person maintaining the database has a backup,
but it's better not to have to rely on it.

We talked about data types earlier [in Introduction to SQL: SQL Data Type Quick Reference](https://librarycarpentry.org/lc-sql/01-introduction/index.html#sql-data-type-quick-reference).

When we create a table,
we can specify several kinds of constraints on its columns.
For example,
a better definition for the `journals` table would be:

~~~
CREATE TABLE "journals" (
	"id"	INTEGER NOT NULL PRIMARY KEY AUTOINCREMENT,
	"ISSN-L"	TEXT,
	"ISSNs"	TEXT,
	"PublisherId"	INTEGER,
	"Journal_Title"	TEXT,
	CONSTRAINT "PublisherId" FOREIGN KEY("PublisherId") REFERENCES "publishers"("id") 
);
~~~
{: .sql}

Once again,
exactly what constraints are available
and what they're called
depends on which database manager we are using.

Once tables have been created,
we can add, change, and remove records using our other set of commands,
`INSERT`, `UPDATE`, and `DELETE`.

Here is an example of inserting rows into the `journals` table:

~~~
INSERT INTO "journals" VALUES (1,'2077-0472','2077-0472',2,'Agriculture');
INSERT INTO "journals" VALUES (2,'2073-4395','2073-4395',2,'Agronomy');
INSERT INTO "journals" VALUES (3,'2076-2616','2076-2616',2,'Animals');

~~~
{: .sql}

We can also insert values into one table directly from another:

~~~
CREATE TABLE "myjournals"(Journal_Title text, ISSNs text);
INSERT INTO "myjournals" SELECT Journal_Title, long ISSNs journals;
~~~
{: .sql}

Modifying existing records is done using the `UPDATE` statement.
To do this we tell the database which table we want to update,
what we want to change the values to for any or all of the fields,
and under what conditions we should update the values.

For example, if we made a typo when entering the ISSNs
of the last `INSERT` statement above, we can correct it with an update:

~~~
UPDATE journals SET ISSN-L = 2076-2615, ISSNs = 2076-2615 WHERE id = 3;
~~~
{: .sql}

Be careful to not forget the `WHERE` clause or the update statement will
modify *all* of the records in the database.

Deleting records can be a bit trickier,
because we have to ensure that the database remains internally consistent.
If all we care about is a single table,
we can use the `DELETE` command with a `WHERE` clause
that matches the records we want to discard.
We can remove the journal `Animals` from the `journals` table like this:

~~~
DELETE FROM journals WHERE Journal_Title = 'Animals';
~~~
{: .sql}

But now the article `Early Onset of Laying and Bumblefoot Favor Keel Bone Fractures` from the table `articles`
has no matching journal anymore.
That's never supposed to happen:
Our queries assume there will be a row `ISSNs` in the table 'journals' 
matching every row `ISSNs`in the table `articles`.

> ## Exercise
>
> Write an SQL statement to add the journal "New Journal of Physics" (ISSNs & ISSNs: 1367-2630; publisher: "Institute of Physics (IOP)") to the table 
> `journals`. You need to add the publisher "IOP" to the table  `publishers` as well.
>
> > ## Solution
> > ~~~
> > INSERT INTO "publishers" VALUES (7,'Institute of Physics (IOP)');
> > INSERT INTO "journals" VALUES (52,'1367-2630','1367-2630',7,'New Journal of Physics');
> > ~~~
> > {: .sql}
> {: .solution}
{: .challenge}

> ## Backing Up with SQL
>
> SQLite has several administrative commands that aren't part of the
> SQL standard.  One of them is `.dump`, which prints the SQL commands
> needed to re-create the database.  Another is `.read`, which reads a
> file created by `.dump` and restores the database.  A colleague of
> yours thinks that storing dump files (which are text) in version
> control is a good way to track and manage changes to the database.
> What are the pros and cons of this approach?  (Hint: records aren't
> stored in any particular order.)
>
> > ## Solution
> > #### Advantages
> > - A version control system will be able to show differences between versions
> > of the dump file; something it can't do for binary files like databases
> > - A VCS only saves changes between versions, rather than a complete copy of
> > each version (save disk space)
> > - The version control log will explain the reason for the changes in each version
> > of the database
> >
> > #### Disadvantages
> > - Artificial differences between commits because records don't have a fixed order
> {: .solution}
{: .challenge}

[create-table]: https://www.sqlite.org/lang_createtable.html
[drop-table]: https://www.sqlite.org/lang_droptable.html

Adaped from the Software Carpentry Course "Databases and SQL", Chapter 9. 'Creating and Modifying Data'.
https://github.com/swcarpentry/sql-novice-survey/edit/gh-pages/_episodes/09-create.md
