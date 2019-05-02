---
layout: page
title: Setup
root: .
---

## Software Requirements

## DB Browser for SQLite

You  will need to install [DB Browser for SQLite](http://sqlitebrowser.org) to complete these lessons. DB Browser for SQLite provides a graphical user interface for connecting to and interacting with a SQLite database. This application bundles SQLite, so you won't need to install SQLite separately.

Note: on Windows, the PortableApp download is recommended as the regular version may take a long time to install on certain systems.

### Download the data

To import data, you'll need to open DB Browser for SQLite and download a zip file containing the data files for this tutorial.

1. Download the data files doaj-article-sample.zip from 
[Zenodo](https://github.com/LibraryCarpentry/lc-sql/tree/gh-pages/files).
2. Open the zip file with the zip utlity on your machine and save the folder and files to a location where you can easily find them. For example, your Desktop.
2. Contained in the zip file are two files, doaj-article-sample.db and doaj-article-sample.db.sql. You can either open the database file (less steps) or import the SQL file (more steps).

### Open the database file

1. Open DB Browser for SQLite.
2. Choose File->Open Database from the menu bar at the top of your screen.
3. Navigate to where you saved the doaj-article-sample folder and/or files. For example, your Desktop.
4. Select doaj-article-sample.db.

### Import the SQL file

1. Open DB Browser for SQLite.
2. Choose File->Import->Database from SQL file from the menu bar at the top of your screen.
3. Navigate to where you saved the doaj-article-sample folder and/or files. For example, your Desktop.
4. Select doaj-article-sample.db.sql.
5. You will be prompted to 'Save As' (i.e. this is the name of the database).
6. Type 'doaj-article-sample' in the Save as box.
7. Make sure that 'SQLite database files' is selected in the drop down and that you save the database to a location where you can easily find it, again, like your Desktop.
8. Click Save.
9. You should see an 'Executing SQL...' prompt and an 'Import completed.' prompt when finished.
10. Click OK.
11. You will see one more prompt which says, "Do you want to save the changes made to the database file...".
12. Click Save.

## Alternatives: SQLite and SqliteOnline

### SQLite

This step is optional. If you are completing the tutorial with DB Browser for SQLite, you won't need to install SQLite separately. If you would like to run SQLite commands directly on the command line, you may need to install [SQLite](https://www.sqlite.org/) separately.

#### Linux and Mac OS x

SQLite command line tools come preinstalled on Linux and Mac OS x.

In order to check they are available type `sqlite3` at the terminal command line. To exit type `.exit`.

#### Windows

On Windows download the [Windows Installer](https://github.com/swcarpentry/windows-installer/releases/download/v0.3/SWCarpentryInstaller.exe)
Copy the file to a directory and open the directory using the windows command line. Type `sqlite3`.

For a more detailed explanation see this [tutorial](http://www.sqlitetutorial.net/download-install-sqlite/).

### SqliteOnline

This step is optional. If you are completing the tutorial with DB Browser for SQLite, you won't need to use SqliteOnline separately. If you are experiencing trouble with DB Browser for SQLite and/or SQLite or if you would like to run SQL commands online via a browser (nothing to install), then visit [https://sqliteonline.com/](https://sqliteonline.com/).

#### Open the database file in SqliteOnline

1. Choose File->Open DB from the SqliteOnline menu bar.
2. Navigate to where you saved the doaj-article-sample folder and/or files. For example, your Desktop.
3. Select doaj-article-sample.db.

#### Open the SQL file in SqliteOnline

1. Choose File->Text-SQL->Open SQL from the SqliteOnline menu bar.
2. Navigate to where you saved the doaj-article-sample folder and/or files. For example, your Desktop.
3. Select doaj-article-sample.db.sql. 
4. You should see the SQL in a text box below the home icon.
5. Click the 'Run' button in the SqliteOnline menu bar.
