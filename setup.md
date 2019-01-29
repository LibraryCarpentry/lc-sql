---
layout: page
title: Setup
root: .
---

## Software Requirements


### DB Browser for SQLite

You  will need to install [DB Browser for SQLite](http://sqlitebrowser.org) to complete these lessons. DB Browser for SQLite provides a graphical user interface for connecting to and interacting with a SQLite database. This application bundles SQLite, so you won't need to install SQLite separately.

Note: on Windows, the PortableApp download is recommended as the regular version may take a long time to install on certain systems.

### SQLite


This step is optional. If you are completing the tutorial with DB Browser for SQLite, you won't need to install SQLite separately. If you would like to run SQLite commands directly on the command line, you may need to install [SQLite](https://www.sqlite.org/) separately.

#### Linux and Mac OS x

SQLite command line tools come preinstalled on Linux and Mac OS x.

In order to check they are available type `sqlite3` at the terminal command line. To exit type `.exit`.

#### Windows

On Windows download the [Windows Installer](https://github.com/swcarpentry/windows-installer/releases/download/v0.3/SWCarpentryInstaller.exe)
Copy the file to a directory and open the directory using the windows command line. Type `sqlite3`.

For a more detailed explanation see this [tutorial](http://www.sqlitetutorial.net/download-install-sqlite/).



## Import

To import data, you'll need to open DB Browser for SQLite and download a zip file containing the data files for this tutorial.

1. Download the data files doaj-article-sample.zip from
    [Figshare](https://doi.org/10.6084/m9.figshare.3409471)
2. Create a New Database (click on the button at the upper left)
3. Choose a name for the database (for example, joaj-article-db)
4. The next screen will present a "Create Table" option. We will create our tables by importing CSV files, so you can close this screen (or click on Cancel)
5. You should now see Tables(0), Indices(0), Views(0), and Triggers(0) in your Database window.
6. Start the import under File->Import->Table from CSV file...
7. Navigate to the directory where your doaj-article-sample folder is located
8. Select the first file to import (start with articles.csv) and click "open"
9. Keep the tablename "articles" suggested by DB Browser (for later imports, continue to use articles, journals,
    licences, languages  publishers),
10. Make sure that the checkbox for "Columnn names in first line" is selected (This is important! Otherwise, your column headers will be considered to be the first row of data)
11. Under  "Fields separator", make sure that ',' (comma) is selected (efault)
12. Use '' as "Quote character" (default)
13. Leave "Trim fields?" checked (default)
14. Press __OK__
15. If successful, you'll receive an "Import Complete" notification.

## Modify

Your import is complete, but all your columns are currently stored as text fields. You may want to modify this so that some data is stored as numeric or integer rather than text. 

1. From your main database screen, select "articles", then click on "Modify Table" fromt he menu above
2. Set the data types for each field: choose TEXT for fields with text:
   (`Title`, `Authors`, `DOI`, `URL`, `Subjects`, `ISSNs`, `Citation`, `First_Author`),
   and INTEGER for fields with numbers:
   (`id`, `LanguageId`, `LicenceId`, `Citation_Count`, `Author_Count`, `Day`, `Month`, `Year`).
3. Click __OK__
