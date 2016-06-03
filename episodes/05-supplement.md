---
title: "Database design -- supplement"
teaching: 15
exercises: 0
questions:
- "FIXME
- "What is SQL? Why is it significant?"
objectives:
- "FIXME"
- "Explain Jekyll's formatting rules."
keypoints:
- "FIXME"
- "Lessons are written in Markdown."
- "Jekyll translates the files in the gh-pages branch into HTML for viewing."
- "The site's configuration is stored in _config.yml."
- "Each page's configuration is stored at the top of that page."
- "Groups of files are stored in collection directories whose names begin with an underscore."
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