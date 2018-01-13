# SI 507 | Lecture 11 | November 15, 2017 | More SQL and PostgreSQL databases

# Admin

Questions?


# Databases and SQL

Quick review of concepts…

- You can interact w/ databases with Python
- Postgres is a database that runs on a (local) server
- SQL is the formal language for interacting with the database
  - Using Python, using the command line `psql`, viewing data with a database viewer (pgAdmin or another)


# Back to section this week
- Building and installing and creating databases, running db server
- Writing some SQL commands via Python
- DDL → Data Definition Language (CREATE, DROP, ALTER, RENAME, TRUNCATE)
- Setting up database connection, database cursor, tables, etc
- … nice to use Python functions to set these up (as `setup database` is doing in that section code: https://github.com/SI507-F17-apd-section-thursday/section-week-10/blob/master/itunes_database.py )



# What to focus on for databases + Python (here)
- How can you use Python to make your setup “easy” (even if sometimes repetitive)
  - — what do you need to know about DDL and what do you need to know about the Python library you’re using?
- As always, break problems into smaller parts
- What SQL to write and execute and deal with using Python? What type of query do you need to do?
- Then: OK, cool, what data’s in the cursor to pull out? How to deal with it in your program? Pretty much 100% of the way there, then.


# More about SQL: complexity! What can you get?

(Say you ALREADY HAVE tables built.)


## Aggregate functions
    SELECT * FROM Songs;

    SELECT COUNT(\*) FROM Songs;

    SELECT AVG(Num_Plays) FROM Songs;

    SELECT Title, Artist FROM Songs;

    SELECT Title FROM Songs WHERE instr("Turn",Title);
## WHERE clauses
    SELECT Title, Artist FROM Songs WHERE Num_Plays>10;
## GROUP BY and ORDER BY
- Group results of queries by a specific thing
  - GROUP BY <username>
  - This is often used when there might be duplicates of something in your query result
- ORDER BY is like sorting

“SELECT the things I want FROM the table(s) I want, and these are the specifics of how I want to filter them”

## INNER JOIN queries
![](https://www.dropbox.com/s/obyvwcb0un6vbsd/Screenshot%202017-11-15%2008.38.52.png?raw=1)


[https://www.dropbox.com/s/obyvwcb0un6vbsd/Screenshot%202017-11-15%2008.38.52.png?dl=0](https://www.dropbox.com/s/obyvwcb0un6vbsd/Screenshot%202017-11-15%2008.38.52.png?dl=0)

e.g.

    SELECT Tweets.tweet_text FROM Tweets INNER JOIN Hashtags ON instr(Tweets.text, Hashtags.hashtag_text); # especially if we didn't have the "join table"


## Subqueries

For example

Query 1:

    SELECT id FROM Artists WHERE name='Nicki Minaj';

Query with subquery:

    SELECT * FROM Songs WHERE Artist_id=(SELECT id FROM Artists WHERE name='Nicki Minaj');

Could also do this in 2 steps — but sometimes you’re looking for it at once and not looking to write e.g. interim Python code!

# More about the DDL part of SQL! What can you set up?


## Constraints
- Foreign Keys
- Not null
- Unique
## Default data

`DEFAULT 1`

## Foreign keys & relationships, “join” tables
- Different ways of building and using relationships between tables
- Related to JOINs…
## On Conflict

here: “DO NOTHING” — don’t break
https://www.postgresql.org/docs/9.5/static/sql-insert.html#SQL-ON-CONFLICT

# With the songs data from last week…

e.g. the file `pgexample_relationships.py` and whatever database that generated for you.


- Write a query to get all of the song titles.
    SELECT Title FROM Songs;psql
- Write a query to get all of the songs by Nicki Minaj.
    SELECT * FROM Songs WHERE Artist_Name='Nicki Minaj';
- Write a query to get the average number of plays of all the songs.
    SELECT AVG(Num_Plays) FROM Songs;
- Write a query to get the artist ~~name~~ label (that’s even more interesting!) AND title of the song of all the songs (hint: this is harder; what’s necessary here?). — This is a different database than the example we just looked at, there are 2 tables involved.
- Anything else that seems interesting.

**Process here:**

- Open up Python file and check it out, make sure it has run.
- (Especially if you’re on a mac) Make sure your server is running. If you try to run the file and it doesn’t work, you’ll get an error saying the server’s not running! Then you can run the command to start it. (Or use the GUI, if you use Windows.)
- Check out a db viewer, psql, something, to check that the database you think exists does exist.
- If you’re using Python, make sure your connection and cursor are set up.
- (Assuming the insertion of data worked just fine)
- Make queries!


# Dealing with multiple tables

(A bunch of proposed examples to illustrate)

## Query from multiple tables
    SELECT Title, Label FROM Songs, Artists WHERE Artist_Name=Name;


## Inner JOINs

Say you have a table with Hashtags: their text, and an id each.

And a table Tweets, with Tweet text (that we know may contain Hashtags), id of a user that posted the Tweet, and the date the tweet was posted, and an id of the Tweet itself.

e.g.

    SELECT Tweets.tweet_text FROM Tweets INNER JOIN Hashtags ON instr(Tweets.text, Hashtags.hashtag_text);

“What is the overlap in the venn diagram?” In this case…

There are also other forms of JOINs — essentially representing different subsections of venn diagrams (though in this course, INNER JOINs are the important ones). From your reading: http://www.sql-join.com/

‘**JOIN tables’…**
Representing relationships in extant tables if you’re going to use it all the time

## Subqueries (less performant, but for us, OK)

For example

Say instead of having Artist_Name in both tables, in `Songs` we just had an `Artist_id` column. And in `Artists`, we had `id`, `Name`, and `Label`.

Query 1:

    SELECT id FROM Artists WHERE name='Nicki Minaj';

Query with subquery:

    SELECT * FROM Songs
      WHERE
        Artist_id=
          (SELECT id
            FROM Artists
              WHERE name='Nicki Minaj');

Could also do this in 2 steps — but sometimes you’re looking for it at once and not looking to write e.g. interim Python code!

# With Twitter data…

Download the file `twitter_database.py`, and the `oauth1`  example Python file in that folder — it has a new function that `twitter_database.py` relies on, so you’ll need to save both in the same directory!

You’ll also need to download `config_example.py`, add your own info, and resave it as `config.py`, like in section. Create any database for your config, just like in section 10 (last week), and fill in the right username for you.

Some of this is like the (neater, and slightly less complex) code you saw to insert data about songs in section. But right now, we don’t care about the insertion — “trust” that it works (as long as it does; let us know if you encounter a problem)

# Interlude on command line arguments

Another type of interactivity in Python

# Back to the twitter database
- Run the setup: `python twitter_database.py setup`
- Run a couple searches, e.g. `python twitter_database.py search programming` or `python twitter_database.py search umich`, or whatever!


- Examine the data, with queries, a visualizer, or the command line. Play around a little.


- At the bottom of the code, there are some directions to write some queries. Try those! Test them out, then see the data by printing, after that specific query, in this particular code, `db_cursor.fetchall()`.


- If you’re done: What else might you want to find out from this data, in English?
  - Translate those into queries and try them out.


# Pulling apart some code
- Glance at the CREATE TABLE statements.
  - How many tables in this database?
  - What are some constraints each of the tables have?
  - For example, what would happen if you tried to add the same tweet twice?


- How to describe in English what’s happening?
  - Dealing with constraints in a database, especially uniqueness constraints…
  - Here, we’ve taken the “easy” — longer but more straightforward — way out. There are also additional quite nice ways of dealing with this with Postgres, which you can use! `UPDATE`, `ON CONFLICT` statements… but in some ways they obscure some of the fundamentals of databases that you should get an idea of to use them
  - What’s required before each step of saving code? What would you want to plan out before writing code to save data in a database? (Often you’ll make it simpler than this! But to have some fun with complex queries and examining a semi-complex database…)
# Designing a database again

Now you know more about databases and have a little more practice

- What relationships exist in this twitter database?
- You know a little about Twitter data from the actual site, and can get more by running the oauth1 code we provided a couple weeks ago! Knowing that — what other tables, fields on tables, or relationships between tables could reasonably exist in a database representing data you’ve gathered from Twitter?

What are the revisions you’d make to your Movies database ideas (or come up with a totally new one) from last week?

- What tables
  - And what columns within them
- What relationships
- What constraints on table columns
