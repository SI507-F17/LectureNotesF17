# SI 507 | Lecture 10 | November 8, 2017 | SQL, PostgreSQL databases & Python

# Admin

Any questions?


# Today

SQL
Database and tool setup
Database exercises
Some time to review code for OAuth and work on your Project 5


# Why use a database?
- Much more efficient lookups than data in — e.g. an Excel file
- Relationships between tables give you power to get complicated aggregate information
- Useful: backs a lot of web and mobile applications, for example — a place to store data


# What is a database?
- In simplest form, a set of data items (rofw AKA tuples, entities, objects) with their attributes (columns AKA fields)


- A “table” is for all of the items of a particular “type” — all songs, all students, all artists… whatever (usually denoted by the name of the table, means something to you, the programmer)
  - the “rows” are the items (or “tuples”)
  - the “columns” are the attributes of each item-thing

For example:

**Table: Tracks** ****— one row for each **song**, 4 attributes of each being saved

| Name              | Artist          | Album                   | Plays |
| ----------------- | --------------- | ----------------------- | ----- |
| London Calling    | The Clash       | London Calling          | 235   |
| Anarchy in the UK | The Sex Pistols | Never Mind the Bollocks | 144   |
| Blitzkrieg Bop    | The Ramones     | The Ramones             | 89    |

Or


**Table: Students**

| Name  | Assn 1 | Assn 2 | Assn 3 |
| ----- | ------ | ------ | ------ |
| Suzy  | 0.89   | 0.92   | 0.74   |
| Toby  | 0.78   | 0.88   | 0.82   |
| Patty | 0.92   | 0.84   | 0.80   |


So far, that’s pretty much just a spreadsheet. And yeah, you can store data in spreadsheets — sometimes you want to!

But databases also have

- internal data structures to support *fast* queries
- nice relational structure possible…

**Relational databases**, which are the most common kind, include support for

- “keys” that uniquely identify items/tuples — like a unique id for each row in a table


- *linkages among items using keys*, to define more complex data structures


- ***structured query language***, which supports a wide range of queries to operate on data stored within the DB.
  - And ways to interact with the database files using Structured Query Language (SQL) via Python!
# What is a database server?

Some databases, like the SQLite you read about, save data in literal files on your computer (or on a server, if you have a web app running. Think of it as a huge computer that can broadcast into the internet). But these are rare.

More likely, you have to set up a *local database server*  and “project” the database into your local internet. It’s still accessible *on your computer*, and the data is still being saved *on your computer*. But you have to have your local database server “started”, or running, before you can interact with the database using Python.

Lots of ways to interact with databases, but we’re going to focus in this course on using Python to do so.


# PostgreSQL (and other databases)

There are many *types* of relational databases. There are also some types of databases that are *not* relational databases — but since relational databases are generally the most commonly used, we’re going to focus on those.

Specifically, we’re going to use a database called “PostgreSQL”, or “Postgres”. It runs on a database server.

There are differences between databases, but those differences are often very minor.


## Things that might vary between types of databases
- Data types of columns the database tables can have (not the same as *Python* data types, but analogous in many ways, e.g. ‘string’ or ‘int’ — there are basic mappings of string:a specific database datatype, etc. INTEGER is in fact… just the same, an Integer!)
- Operations you can do on a database — e.g. add a bunch of things at once, update things in certain ways (we won’t get to that yet today)
- Software you can use to interact with the database
- Sometimes even: ease of installing the setup on a certain operating system…
- Speed in certain circumstances, utility in certain circumstances (we won’t really go into that in this course — this is a deep subject)


## What you *need* to know for now
- We’re using PostgreSQL
- There’s a Python library you can use to interact with Postgres databases called `psycopg2`, which you’ll need to install with `pip`


# Time for installation
- Install your postgres server
- Run your postgres server (for this windows installation, this is automatic, for this mac installation, you have to do something to start it)
- Create a database

We’ll take a few minutes — want to make sure everyone’s installation is working. Follow these instructions if you haven’t (also linked on Canvas! https://umich.instructure.com/courses/181375/pages/postgresql-setup-instructions):

+Postgres Database setup (for mac)
 ****[**https://labkey.org/Documentation/wiki-page.view?name=installPostgreSQLWindows**](https://labkey.org/Documentation/wiki-page.view?name=installPostgreSQLWindows) (for Windows) **Also:** [https://w3resource.com/PostgreSQL/connect-to-postgresql-database.php](https://w3resource.com/PostgreSQL/connect-to-postgresql-database.php)
+Configuring pgAdmin (a tool for viewing data in your databases). You can also use [DBeaver](https://dbeaver.jkiss.org/) or [TeamSQL](https://teamsql.io/) for db visualization (or another if you know it and prefer it)

Brief review of what you should be able to do to confirm this is working! (May vary by operating system and individual setup, so if you’re having problems, let us know — also help each other if you’ve got it working!)

If you finish this, make sure you have done a `pip` install of the library `psycopg2`, and you can download the `pgexample`s code files from Canvas in Lecture 10 and take a look at them:


- `pgexample_multiplerows_one-by0one.py`
- `pgexample_multiplerows_byname.py`
- And AFTER looking at those, `pgexample_relationships.py`, which shows some more complicated database code.

We will come back to these as a group shortly.

**Goal:**

- Have installed postgres
- Be able to create a database

Other things: like running software to visualize your data, etc — NOT necessary today. Nice, but not necessary.

# What *is* SQL?

**Structured Query Language**
Formal language to interact with pretty much all relational databases

In this class: we’ll be using Python to run SQL and interact with the database, instead of using a specific program to write “raw” SQL — but you’ll still be writing SQL and putting it in a Python program.

Python is simply handling the interactions between a script and the database — the place where the data lives in “tables”


## Things you can do with SQL
- Create Tables in a database (`CREATE` statements)
  - Specify what Columns/Fields each table has when you create it
- Delete tables from a database (`DROP` statements)
- Change the structure of tables in a Database (`ALTER` statements)
- Insert data into tables in a database (`INSERT` statements — these have very specific syntax, which you’ll see)
- Make **queries** to a database
  - “Given a specific syntax, here’s the data I want” → see the data! (We’re going to use Python to do this, so you can then further deal with the data in your Python program)
  - Many kinds of queries…


# Why are they called relational databases?

Relationships you can build between tables in databases one of the most powerful things about them

“Build complex data structures”

Don’t repeat any information, and yet store a lot of data that has different relationships between it!

We’ll see a lot more examples of this after getting accustomed to basic database syntax and operations.

Thinking about a database / data stored in it…

## Diagramming exercise… (and example)
- Example diagram of an application with Songs and Artists…
## **Exercise**
-  Now: Say you want to write a script to save data about Movies:
  - Movies, Directors, Actors, Soundtracks

How many tables should there be?
What should each table represent?
What relationships should exist between tables?

  **Different types of relationships!**
  One : Many
  Many : Many
    An association or join table — each row consists of:
      an id of *the relationship*, an id of each of the entities in the relationship
  (and One : One)

Movies
Soundtrack-lists
Songs
SongArtists
MovieDirectors
MovieActors

Get together with people sitting near you:  draw the diagram, indicating relationships between tables

  In each table: What fields will it have?


# Visually representing/understanding what’s in a database


## Interacting with the database — e.g. via a command line interface

`psql DATABASE_NAME`

Some examples..


## Interacting with a database via pgAdmin
  Here’s a little bit of an instruction about viewing data in pgAdmin: https://popmednet.atlassian.net/wiki/spaces/KB/pages/3801143/How+to+view+data+in+pgAdmin
# Some sample code & exercises


## Some specifics for using Python to interact with Postgres databases

Download and look at the scripts `pgexample_multiplerows_onebyone.py` and `pgexample_multiplerows_byname.py`.

Let’s walk through them…

Try them out!

Think: what are they doing?

Then look at the database: what data does it have in it? Are you surprised?


- with pgAdmin
- with the `psql` command line interface

See if it works — any questions?



# Time to work on OAuth / Project 5
## First, a highlight on Piazza


## Then
- General questions?
  - And a reminder about the Twitter OAuth1 code / verifier… what’s good to look at
- Work time…
