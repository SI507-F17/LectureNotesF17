# SI 507 | Lecture 12 | Introduction to Web Development, Project planning questions

# Admin
- This week’s schedule, see announcement
- And some time today…

Questions?

# Putting things together
- So far you’ve learned a lot of things about writing code in Python that accesses, and processes data in a number of different ways
- A bunch about planning for and collaborating on projects, and a few occasions to experience doing those things
- You can imagine — and should think about, for your final project — how getting data from queries like you did for Project 6,
  - combined with a number of ways of processing and analyzing data you’ve already looked at
  - could combine to get a cool result
- What you’re learning about Flask today — introduction to a lot
  - Take it slow, though
  - Trust it bit by bit
  - Like opening a door to a whole new world of development!
  - Don’t worry if there’s a lot you don’t understand yet — there’s a lot you haven’t done yet! But with what you have, you can plug into this in a pretty cool, pretty extendable way.
- Now, an introduction to a popular web development **design pattern**


# Model - View - Controller
## A lot of complex web applications
- Are built using a web framework, relying on others’ code to write things more simply
- Function a lot like a complex interface to a database — powered by a database


## MVC is the design pattern a lot of web frameworks follow, or *can* follow.

In this course, we’re going to go over the *basic idea* of what that design pattern is, and introduce you to a web framework called **Flask —** there’s a lot to the Flask web framework and web development in general, but here, we’re going to focus on plugging what you know from 507 (and 506 or other experience) into Flask and the MVC design pattern.

So: a few new concepts, and how to take code and plug in some more to do what you want.


# Models

Code that deals with databases

We’re not going to look at this much/at all, but it’s an important part of this design pattern. In web apps, things often work a little differently than writing scripts to deal with databases/do data analysis in SQL, which you’ve started to look at in class these past couple weeks. After this, writing models in web apps will be easier to learn — but we don’t have enough time to go into depth.

Models outline how the tables are formed — what is the *schema* of the database the application is going to rely on? What tables will there be, and what columns will each table have?


# Views

Code that deals with what you *see* in an application

If you’re a front-end developer, the code you write is primarily code that deals with the Views — what you see — though not necessarily only.

If you’re a designer, code you write or designs you make will probably affect programmers working on view code (if you’re not writing it yourself!). How much interaction you have with the code will probably depend upon your role, your company, etc.

507 is not a design course. We’re going to focus on…


# Controllers

Code — basically — that handles the *Python logic* and often *sends data to the views*.
Code in the “controllers” may:

- Access data from databases
- Save new data TO databases
- Create files
- Open or deal with data from files
- Grab data from the internet using an API or scraping
- Process data with conditionals, functions, class definitions, etc, etc, etc, all kinds of logic that determines what data is
  - used
  - accessed
  - sent to a view for a user to see

You’ve already written code that does all of that stuff, in various ways.

Today we’re gonna look at how you can fit that into a pattern that the **Flask web framework** provides.


# Flask

A library (and a whole lot of other libraries that go with it) in Python that make it easier to create a web application.


## Interlude: Developing a web application on your own computer

Remember the local server we ran earlier, where you saw files in a file on your computer in a web browser?

And the local Postgres server you’re running whenever you run database code?

Flask, the framework, the library that allows you to use it, comes with a local server that does fancier things than that one before.

The code we’re providing is set up so that if you run the program in the right way, you start up the server and the application will run on it.


## **Creating a virtual environment for Flask**

Download `flask-requirements.txt` from Canvas.

These are what you need for a *simple* Flask application that we’re going to run AND for if you want to run ALL of the possible examples we might link for you (there are a couple things included here that you don’t need to run the simplest examples from this class session and that you DON’T need for project 6.5 — but you do need a few of them, so may as well install them all in your virtual environment).

Create a virtual environment. Call it whatever you want, that will remind you that this is a venv for a flask project from this class.

Then activate the virtual environment, and THEN, and run `pip install -r flask-requirements.txt` (make sure you’ve accessed the place in your computer where you saved the `**flask-requirements.txt**` file!)


## Run your first Flask application

Download `first_flask_app.py`

That’s a whole web application — a very simple one.

`cd` to the place it is,  with your virtualenv from above activated, and then type:
`python first_flask_app.py runserver`

Check out what’s happening in your terminal!

In a browser, type in and check out this URL: `http://localhost:5000`
And then…

`http://localhost:5000/user/yourname` (You can run literally that, OR replace **yourname** with your actual name — see what happens)

Let’s talk about what’s happening here…

Exit it / stop it running on the local server by typing `Control + C` (even if you use a Mac, still Ctrl, not Cmd)

# View functions

Each of these functions that has `@app.route( …` above it is what’s called a **view function** in Flask.

View functions are basically where the **controller** code lives.

**When a view function returns text**, the Flask server, which is fancier than the simple local server we ran before, will parse the return value so **it will be rendered in HTML in the browser.**

**When you go to** `**http://localhost:5000**` **in your web browser, you’re making a request,** **via the browser**, to this specific port, this specific “location” on your local server.

And seeing the result in the browser. Just like you see when you go to `http://google.com` on the internet — you’re seeing the location on the internet represented by that web address

(behind the scenes, it’s actually a specific set of numbers representing this “google.com” location on the internet, but we have a way of looking up with numbers go with that address so it shows you the right thing in the right place — and your browser handles that lookup without you having to deal with it)

Flask has, built in, various ways of moving data around a Flask application, between what are called “routes”


> Those @ signs indicate **decorators** (you can read about them here: http://interactivepython.org/runestone/static/webfundamentals/Frameworks/decorators.html but you don’t actually have to understand them completely in order to use Flask, as long as you use them correctly like this! — n.b. some things in that textbook overall are outdated, so I havn’t assigned or pointed to much of it, but others are very useful!)

This application has a bunch of controller code, but it’s not doing anything special for the Views (no extra code, just sends data right to the browser that manages the request, basically), and there are no databases involved.

You can make them more complicated, though.


## Exercise (practice) — play around & we’ll review

Try to make a new route in this Flask application:

- at `/itunes/<artist>`
- whatever artist name is at the end of the URL (look at the above **yourname** example…)
- this view function should make a request to the iTunes API (see project 2) — no caching! (Caching setups are a little different on the web, although unfortunately we won’t be able to get there in this course)
- Access data and build up a list of song titles, and return a string of song titles separated in some way from the view function

Let’s check this out…


## An example with some **Views** code

(fork and clone and then run the same way, e.g. `python views_app.py runserver` , `cd`'d inside the folder you clone)
https://github.com/SI507-F17/507_Views_Flask_Example

Running it, you’ll see something like this, if you put in some examples for non-valid  (e.g. `/values`, `/showvalues` …)
and valid (e.g. `/showvalues/a`
or `/showvalues/supercalifragilisticexpialidocous` or `/showvalues/aaaaa`  … )
routes:

![](https://www.dropbox.com/s/n1tmejvx0fx5o2f/Screenshot%202017-11-28%2022.43.28.png?raw=1)


[https://www.dropbox.com/s/n1tmejvx0fx5o2f/Screenshot%202017-11-28%2022.43.28.png?dl=0](https://www.dropbox.com/s/n1tmejvx0fx5o2f/Screenshot%202017-11-28%2022.43.28.png?dl=0)

But what’s happening here?

**First, to mention:**
From now on, we’ll *primarily* show Flask application code in its own directory, because if you later build out a more complicated Flask application, it’ll be important to save all in its own directory, to deal with the structure of the application as well as keeping it together for Git/GitHub!


  It is possible to have complete applications that are just 1 file and can be run from wherever they’re saved, like a couple examples you’ve seen/will see today. But in general, it’s best to save Flask app code in its own directory — say you add to it, you’ll need to deal with a specific directory structure then.
# A little bit about views (and understanding views)

We are not going to focus on any design here at the end of this course — but there are some aspects of view code that are closely related to the controllers code you’re already (from other things you’ve done in this course, etc) rather familiar with.

One of the questions to ask yourself in a controller may be — what data do I need to send to the view?

And to answer that, you need to know: What is the view waiting for? What structure of data? Called what?

Because…

There’s a structure for writing code for Views that interacts with Python objects, called **templating code.** Flask generally relies on a formal language structure called **Jinja templating** — you can read about the Jinja2 templating language here: https://en.wikipedia.org/wiki/Jinja_(template_engine) , http://jinja.pocoo.org/ (overall docs), http://flask.pocoo.org/docs/0.12/templating/ (this may include stuff about Flask you’re not yet familiar with)

You are not responsible for writing any templating code — just for understanding a little bit of it in Project 6.5: looking at this view, what do I need to send to it in the return from my view function?

To help with that, Flask allows you to import a function called `render_template` (also a bunch of others that can help you pass data around from one view to another, interacting with a database, etc, but more on that another time). You use it to return from the function, e.g.

`return render_template(``'``nameoftemplatefile.html``'``, datavars_to_send_to_view=its_value, other_data_var_to_send=its_value_here, …)`

In that example, `datavars_to_send_to_view` AND `other_data_var_to_send`, whatever their values, would be what is available to the template saved in a special directory called `templates` called, in this case, `**nameoftemplatefile.html**`.

You have to save all the `.html` files that are your TEMPLATES (view code files) for the application in a special directory, inside the directory that contains your main flask application file. This directory **must** be called `templates` — it’s part of Flask that `render_template` will look for a template of the right name (like in that case, `nameoftemplatefile.html` … ) inside the `templates` subdirectory of wherever the main app Python file lives.

That’s what’s happening in that example above — we render a template that is waiting for a list of song titles called `song_names`, calls it `song_titles`, and sends that to the Jinja templating code in the view file `songs.html` that we’ve built and saved in the `templates` directory.


# Requests…

Behind the scenes, so to speak, what Flask is doing at the return value of each view function is creating what you know as a **response object**.

Its text data… is whatever you send and manage with your return value from your view function —

it just the text data you’re returning right there, wrapped in a response object…

OR it is text data wrapped up in template HTML code and rendered, with data sent to the template (view) code…

Either way, it’s a **response thing**, and you know how to deal with those from the other end! This is the first time you’ve made your *own* (well, the first time you’ve probably thought about it this way).


## Try it out (prove it to yourself)

Run, in the right directory, where you saved it, `python first_flask_app.py runserver`, and *don’t* Ctrl+C to stop it yet

Then write a file of code:

`**get_data.py**`

    import requests

    resp = requests.get("http://localhost:5000")
    print(resp.text)

And run that file (in a different Terminal/Git Bash/command prompt window than the one that is running the local server!). `python get_data.py`

What prints? Why?

# Project 6.5

See: https://github.com/SI507-F17/507-Project6.5

Due Sunday 11:59 pm

# Another example — other complexity/features

**Using more complex html to e.g. make forms and send the data from one place in the app to another** —
Open the file `new_form_example.py` from Canvas and check it out; run the application in the directory where it’s saved,
`python new_form_example.py runserver` … and go to the routes you want to interact with, see what happens.

(This is another single file application — though still, recommend putting the file in its *own* directory in case you end up wanting to build on it!)

**Could try:** that HTML that gets returned from a route?
Create a directory just for this app, add a `templates` folder, make a template for the form and return an invocation of `render_template` instead of just returning this fairly ugly formatted HTML string.


There are also examples possible that use **models** code, and a bunch of other kinds of complexity — defining code about databases and saving data to databases, interacting with databases in a complex/interactive web application — but those are more complex than we have time for today. That’s something you could explore additionally at a later date with this as a starting point if you’re interested.

(Other classes that deal with similar ideas, sometimes in different languages and with different goals: SI 664, SI 699 — maybe others)
****

# Planning & working on your final projects

You’ll get a little more feedback from us in response to your Project 6 milestones, but

**Consider as you go and wrap up your plan:**

- Where do you want your focus to be? (complex scraping, dealing with an API, complex queries or analysis, ?? make sure you’re not scoping beyond what you can do in this amount of time AND are fulfilling reqs!)
- What’s the flow of data through the application?
  - Can you draw a flow chart for what needs to happen in the program first?
- What about a list of things *you* need to set up, in order of dependencies
  - What do you have to decide, or write and test, before you can do the next thing, etc?
- Other questions?
- Take some time to brainstorm together (in section or office hours, too, after you wrap up 6.5)
- Piazza thread: share your ideas? Pinned — Link: https://umich.instructure.com/courses/181375/external_tools/67
