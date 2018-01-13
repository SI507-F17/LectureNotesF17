# SI 507 F17 | Lecture 13 | Visualizing and processing data, Project work

# Admin

Questions?

Food & coffee… please take some!

# Visualization options & examples

Skills for each of these — not so much about the visualizing data (SI 649 - InfoViz, will teach you a lot more about that specifically).

Instead, the idea here is to stretch your knowledge of Python a little bit that you’ve built over the course of this semester.


# General planning — recommendations

**Consider as you go and wrap up your plan:**

- *Where do you want your focus to be?* (complex scraping, dealing with an API, complex queries or analysis, ?? make sure you’re not scoping beyond what you can do in this amount of time AND are fulfilling reqs!) For example…
  - If you’re focused on complex things in the process of the application, you may want to choose a visualization option like a carefully planned Excel file or an HTML file to display results in a cool way that doesn’t require as much new learning, focusing that on databases / data gathering / structuring /etc

  - Something new — using methods and processes you’ve practiced before (just perhaps in a new way) — rather than focusing on learning a new system

  - But if you’re using data that is not as challenging to get and process — e.g. you read about setting up access from an API that uses OAuth, you succeeded, now to move on to more challenging things — learning a new charting library or playing with Flask a little bit might be more fun AND you may have time to complete it!

- **Class Minimum Viable Product That Fulfills Requirements**
  - You do need to get data from a OAuth API or scraping
  - Because that practices skills from this semester
  - You may get additional data from an API that does not require OAuth if you want, but that does not fulfill the stated requirements — otherwise it’s not fair. This is a chance to practice skills in a freeform way — build your project so you’ll be able to, add some extra stuff that you may ultimately decide to take out (e.g. some extra scraping, etc)
  - If using Flask — OK not to do everything the “best” way — assuming you started learning Flask last week, that’s a tiny amount of experience! You could spend a whole semester learning this.

- Think, continually: What’s the flow of data through the application?
  - Can you draw a flow chart for what needs to happen in the program first?

- What about a list of things *you* need to set up, in order of dependencies
  - What do you have to decide, or write and test, before you can do the next thing, etc?

**From last week:**

- Take some time to brainstorm together, solve problems together if you can
- Piazza thread: share your ideas? Pinned

Questions to address here/at large? (More individual question time later)

# Plot.ly

Getting started (need to sign up for an account, free tier — meaning you shouldn’t use any super private data because it’ll be publicly available at link on site…): https://plot.ly/python/getting-started/

Check out your account settings to get an API key and set up your plot.ly configuration: https://plot.ly/settings/api

What is your goal?

See code examples on Canvas > Lecture 13 > Viz Examples > Plotly examples

- One simpler (plot1) example with fake data
- One more complex bar chart example with real twitter data (fill in `twitter_info.py` from the twitter apps console) and fake Facebook data (just for example)
# Embedding Videos & Playlists
## In HTML docs

iframes — https://www.w3schools.com/tags/tag_iframe.asp

One way to achieve this goal.

(Images different — you can render an image with `<img src=``"``imagespecificurlhere``"``>` tag… ) https://www.w3schools.com/tags/tag_img.asp


**Remember:** https://www.programsinformationpeople.org/runestone/static/publicpy3/#string-formatting !

**Spotify playlist embedding:** https://news.spotify.com/us/2012/08/17/how-to-embed-a-spotify-play-button-on-your-blog-forum-or-website/, also with iframes

Don’t need to embed if you don’t want to — as long as you show data somehow, text is OK! But this is an option, too.

## In Flask… (in HTML docs)

There are a lot of complicated ways to use Flask that we don’t have time for this semester — it’s OK to explore, of course, but make sure you’re focusing more on consolidating your knowledge from parts of the semester into a final project that fulfills these requirements than learning about Flask.

Here are some examples of using Flask as your visualizing, post Project 6.5:


- (Partial/all-the-basics solution to your section exercise, as you discussed in class) https://github.com/SI507-F17/section-week-13
  - You don’t have to have nice CSS for your Flask app to work but you *can* (e.g. use what you learned from 539 if you have taken/are taking that course!)
-
# Matplotlib

https://matplotlib.org/users/pyplot_tutorial.html (more useful)
Goal — get a list of data/lists of data where you know what they represent via your processing throughout the program, follow example to create a plot and save an image
https://matplotlib.org/examples/pylab_examples/simple_plot.html

From part of that example code…

    import numpy as np

`numpy` is a Python library that is helpful for a lot of scientific computing and specific mathematical operations

e.g. more precise use of decimals in various ways, so you’ll see “numpy arrays” that are a lot like Python lists, except that they can be dealt with in more precise mathematical ways for e.g. stats, charts…

A lot of `matplotlib` examples depend on types that are specific to the `numpy` library

But some like this:


    import matplotlib.pyplot as plt
    plt.plot([1,2,3,4], [1,4,9,16], 'ro') # 'r' indicates the color, 'o' is dots -- like scatter plot -- instead of a line
    plt.axis([0, 6, 0, 20])
    plt.show()

Note: for `.show()`, shows image — often you have to close the image to stop the program running

(ok to save it or screenshot it to show example — don’t have to use `save_image` functions but OK if you do — whatever works best for you, just make sure to show us an example of your project working when you submit it, as instructed!)

So if you choose to do this, looking at other code and basing your idea off it, trying it out (simpler examples), understanding it, and adapting it, is a good way to go. Minimum viable first — as always.



# Project work time
## Straw polls…


## We advise…

Making sure these have been done OK:

[ ] Write code to get data from your API / Website
[ ] Use “dummy data" and create a visualization
[ ] Complete a first version of a test suite

Outline plan in comments

Complete test suite

Write pieces bit by bit and test them as you go

Don’t spend all or most of your energy on the visualization — just make sure you can show us *something*. The process leading up to it is the bulk of the work and even more important (both in terms of 507 concepts and points!)


## For questions


## Queue: [link]


Before asking me or Anand in class, write your question on Piazza so we can read it:

- What is happening and how is it different from what you expect
- Is there any context we need to know about how your code overall works
- Do you have sample code you are referring to, including line numbers, to share (if show, please share some — a screenshot with line numbers is OK)
- If you’re getting an error, what exactly is the error message *and* what is YOUR guess about what it means
- What examples have you looked at? documentation?
- If you’ve tried other things that were also not successful, what were they and what happened when you tried them (specifically)?

This will help us — and others — answer your questions better, and will likely help you as well
