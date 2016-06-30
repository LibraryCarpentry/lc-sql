---
title: "Database design -- supplement"
teaching: 15
exercises: 0
questions:
- "What is SQL? Why is it significant?"
objectives:
- "to understand the signifance and utilty of SQL"
keypoints:
- "SQL is one of many database management systems"
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
