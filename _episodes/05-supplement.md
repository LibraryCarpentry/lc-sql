---
title: "Database design supplement"
teaching: 15
exercises: 0
questions:
- "What do I need to know to create my own databases in SQL?"
objectives:
- "Understand best practices for designing databases in SQLite or other SQL programs"
keypoints:
- "Planning out your database design early helps avoid misunderstanding your data or not being able to ask the questions you want of the data"
- "SQLite is one of many database management systems"
---

Database Design

## Q & A on Database Design (review if time)

1. Order doesn't matter
2. Every row-column combination contains a single _atomic_ value, i.e., not
   containing parts we might want to work with separately.
3. One field per type of information
4. No redundant information
     * Split into separate tables with one table per class of information
	 * Needs an identifier in common between tables – shared column - to
       reconnect (foreign key).


## Other database management systems

* Access or Filemaker Pro
    * GUI
    * Forms w/QAQC
	* But not cross-platform
* MySQL/PostgreSQL
    * Multiple simultaneous users
	* More difficult to setup and maintain
