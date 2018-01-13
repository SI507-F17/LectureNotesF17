# 507 | Lecture 5 | October 4, 2017 | Scraping, BeautifulSoup

# Admin
- Project 3 released
- Project 2 grades released soon
- 507 Friday office hours now **12-1 pm Fridays**, per casual vote, in NQ 1243

Interested in being a tutor to a SI 106 student/students, or already available for Python tutoring?  (106 is the undergraduate introduction to Python programming course, similar but not identical to SI 506.) Professor Steve Oney is curious about people who tutor based on student requests

Questions?

# Scraping: What is it?
- Grabbing data from the web, but not the way you did before (e.g. 506, waiving 506)
- Pulling, or “scraping”, data out of **markup language**

You read about markup languages — code that powers what you seen in a browser. HTML, as well as CSS and XML. So you’ve seen some of the structure behind a page. Let’s look at this one…

For our purposes, we’ll be focusing primarily on HTML, and data *stored* & shared using HTML.


## How are markup languages useful for a data-oriented programmer?
- HTML provides the *meaningful structure* of the page (not the visual changes, colors, etc, with the conventional system)
- This is also important for accessibility
  - Screenreaders look at HTML
- HTML has particular identifiers
  - Specific to a tag
  - True of a set of tags
- HTML has a hierarchical structure a lot like file systems
  - Parents, children

Check out `samplehtml.html` (download it from Canvas > Files > Code Samples)

    <body>
      <div id="overall">
        <div class="page-section" id="main-section">
          <h1> A main heading. </h1>
          <h2> (A sub heading.)</h2>
          <ol>
            <li> First item in ordered list</li>
            <li> Second item in ordered list</li>
            <li> Third item in ordered list</li>
          </ol>
          <div class="page-section" id="below-section">
            <h2>Another sub heading.</h2>
            <p>Some text goes here in a paragraph tag. <br> If you want to learn more about this stuff, take SI 339!</p>
            <span>
              <p>An image from the comic XKCD below.</p> <br> <br>
              <img width=500 id="xkcdimg1" alt="Image of XKCD comic" property="img-123" src="https://imgs.xkcd.com/comics/all_you_can_eat_2x.png" />
              <p>Find more similar stuff at <a class="external" id="comic" href="http://xkcd.com">the comic web site</a>.
              <p>Or just check out your homework after you sign into <a class="external" id="lms-canvas" href="http://canvas.umich.edu">Canvas</a>.
            </span>
          </div>
        </div>
      </div>
    </body>

So, just look at this HTML format text. What can you determine about the *information structure* of this page?

- What attribute(s) are unique to the link to the XKCD comic (the website)?
- What attribute(s) are unique to *all the links* on this page, but nothing else?
- What attribute(s) are unique to the text items in the ordered list?
- What about the section of the page with the image? How could you identify that? What attribute(s) are unique to it?
- What about these three lines of text — what’s true about all of them but nothing else in this html document?
  > An image from the comic XKCD below.
  > Find more similar stuff at the comic web site.
  > Or just check out your homework after you sign into Canvas.

Open up that HTML document in a browser (sample.html…) — find them that way.

(If you open a `.html` document with Finder or My Computer, it’ll generally default to opening in a browser. If you want to see the text, you can specify your text editor.)


# Interacting with HTML in Python — BeautifulSoup

BeautifulSoup is not the *only* library that can be used for “scraping’ and “crawling” (more on that later) the web in Python. But it is one of the most common, and one you’ll learn in this course.

When you import BeautifulSoup…


    from bs4 import BeautifulSoup

What you are importing is a class definition.

When you installed `bs4` — remember, you either need to install via virtual environment OR `pip3 install`… to install to your Python 3. (Anaconda includes bs4 already, if you have that.)

The `BeautifulSoup` class is pretty complicated and fancy.
Let’s take a look at some code using it, and then we’ll dig into it more deeply.

On Canvas: `bsoup_ursulav.py` (Ursula Vernon is an author and artist whose website this code deals with.


    import requests
    from bs4 import BeautifulSoup

    # Caching the data so we don't hit her server too much
    try:
      ursulav_data = open("ursulav.html",'r').read()
    except:
      ursulav_data = requests.get("http://www.redwombatstudio.com/").text
      f = open("ursulav.html",'w')
      f.write(ursulav_data) # more in the chapter on Files in textbook
      f.close()
      # ursulav_data should be a big string of HTML data, regardless, at this point in program

    # Create a BeautifulSoup instance, using the html parser
    soup = BeautifulSoup(ursulav_data, 'html.parser')
    # print(soup.prettify())

    # What does this do? What type is div_one after this?
    div_one = soup.find("div",{"class":"content"})
    # print(div_one.prettify()) # Why would you uncomment this?


    # What does this do?
    some_list_elems = div_one.find_all("p")
    # Consider: what type is EACH ELEMENT of some_list_elems?

    option_texts = []
    for e in some_list_elems:
        option_texts.append(e.text)
    # Consider: what type is EACH ELEMENT of option_texts?

    # <a href="/blog">Go to Ursula's website!</a>

    all_links = [x['href'] for x in soup.find_all('a')]
    # Consider: what type is EACH ELEMENT of all_links?

    # What does this code do? How would you explain it?
    all_imgs = soup.find_all('img') # all_imgs is a list of beautifulsoup instances
    for i in all_imgs:
        print(i.get('alt',"No alt text..."))




1. Go through this code and chunk it into bits to explain in English. If you had to write an outline of what is happening in this code, in English, what would you say? Try to answer the questions included in the comments.
2. Next goal: **add to this code** so that you can access and print out the text from these four navigation links on separate lines, i.e. you should ultimately print out, at the end,


> HOME
> THE ARTIST
> BLOG
> CONTACT
![](https://www.dropbox.com/s/fvioo0b79nj4l03/Screenshot%202017-10-02%2017.18.14.png?raw=1)


[://www.dropbox.com/s/fvioo0b79nj4l03/Screenshot%202017-10-02%2017.18.14.png?dl=0](https://www.dropbox.com/s/fvioo0b79nj4l03/Screenshot%202017-10-02%2017.18.14.png?dl=0)

Check out http://www. .com/ to figure out what code to write to do that…

We’ll cut this exercise after a while so we can talk about how to approach it — focus on making sure you understand this code and what it’s doing, and could change it to do things that are a little different.


# Dealing with BeautifulSoup and HTML data

`BeautifulSoup`  **constructor input: a string formatted in an HTML way ,** and **the string name of the parser it should use (for us, usually** `**"**``**html.parser"**`)

**Its** `**BeautifulSoup**` **instances:**

  - have a number of useful methods that take input, such as `find` and `find_all`
  - depending on what the input was to the instance, may have useful attributes
    - e.g. `text`
  - sometimes can be indexed into, the same way a dictionary (an instance of class `Dict` in Python…) can be
    - e.g. if `soup1` is a BeautifulSoup instance, sometimes — `soup1[``'``href``'``]` or `soup1['alt']`
    - like dictionaries, you can invoke a `get` method on them, which will work variously depending upon what data’s in the instance — e.g. `soup1.get(``'``alt``'``)` or `soup1.get('aria-text')` …


## Some gotchas
- The method `find` returns a `BeautifulSoup` instance… if it can find one
- The method `find_all` returns a list of `BeautifulSoup` instances (or an empty list)
- You can think of things like — each `BeautifulSoup` instance has the same *potential*, though different instances may have very different data / different amounts of data in them
  - Which allows/causes different methods and attributes to work
- HTML is not always the way you might wish it were (a problem for you, programmer accessing data; often a potential problem for accessibility… 539 will teach you more about that)
- Various tags, classes, and ids of selections
  - “Whoa, that’s weird, but I guess…”
  - Not everyone has expected you to look at their markup
- Diagramming some of that code…


- And, finally, the way you’re literally accessing the data to scrape


# Using & caching data for scraping
- Generally: HTML is found on the internet
- Interpreted and rendered in your web browser
  - our examples use Chrome, nice developer tools
  - also exist in Firefox, Safari — to follow along with me, I recommend Chrome
- Takes a long time to get data from the internet sometimes
- Not nice to other people’s servers if you hit them constantly
  - One person refreshing a page…
  - vs a program basically refreshing or loading a page 1000 times as you try to access data on it
  - Causes the person paying for hosting to pay more $$
  - Maybe causes a page to crash

So: access the HTML data and save it in a file — *caching*

Still the same scraping process

Less weight on someone else’s server


## Accessing HTML data from the internet (scraping)
- There are multiple ways to do this
- One recommended you’ve seen before — use `requests`
  - Just because you’re not requesting data from an *API* doesn’t mean you don’t get the structured data that’s at the page
  - Just this page: is not made for a program to interact with
  - It’s pretty, things to click on — it’s made for a human to interact with
  - Still — includes structured data … hence, scraping!
    - **For programs to interact with websites and get data that** ***aren’t*** **intended specifically for programs —applications — to interact with**.

## Caching: the basic idea
- save data on your computer so fewer requests get made

This also happens in your browser

And in our textbook, there’s a suggestion of a more complex system with which to cache data…

But for now, make it as simple as possible while still useful

Note if you *only* make a request and save it to a file *every time the program runs* — it doesn’t save you that many requests. Or maybe it does, but still a new request *every time you run the program.*

Good goal of caching: if you run the program a second time, only re-make an internet request if you *have to*. (Lost the data that’ll work for your proof of concept, for example.)

**Will this work if the data changes a lot, online**?
In practice, no.

For us, *at the moment*, yes. If you have data from some point in time from a web page, that’s enough — we’ll assume that’s a persistent version we can try with.

As we move forward, we’ll think about other ways to deal with the issues that arise from this type of problem — there’s no single answer.

**At first**, we’ll focus on minimizing our internet requests (and crashing as few servers as possible!).


## Caching HTML data, with exception clauses

We will be talking about complex systems for caching later on (pretty soon)
For now, the primary goal is to ensure

- We save the data we need/primarily rely on for scraping programs on our own computers, so we don’t hit a server too much
- Use exception syntax to do so, so you only make a request when you need to, but always have your code work the same way

# Debugging with BeautifulSoup
- Visual!
- Consider the actual markup — it isn’t always “good” or “perfect”
- Consider the hierarchy


## **Exercise**

A little complication on some of the stuff you’ll deal with in Project 3

Start here: https://www.nps.gov/state/mt/index.htm

Plan to write code to get & cache data from that URL

And then, from there…

What data do you need to access, and what do you need to figure out, in order to count and print out the **number of alerts currently in effect at Glacier National Park**?

(Recommendation: focus on your *plan* — write out in English what you’ll need to do — before translating it into code; writing some notes about code you’ll want to look up syntax for as you go. For example… <live>)

**n.b.** If the Glacier page (https://www.nps.gov/glac/index.htm) looks like this, the result would be **3** …

![A screenshot of the Glacier National Park page, showing alerts currently in effect, plus the beginning of the next section of the page -- there are 3 alerts in effect, in this image.](https://www.dropbox.com/s/o5pdvjlcxncpu0t/Screenshot%202017-10-02%2017.36.29.png?raw=1)


[https://www.dropbox.com/s/o5pdvjlcxncpu0t/Screenshot%202017-10-02%2017.36.29.png?dl=0](https://www.dropbox.com/s/o5pdvjlcxncpu0t/Screenshot%202017-10-02%2017.36.29.png?dl=0)



## A couple funny warnings/stories about caching (mostly about not caching)
- UMSI site last year
- Yelp in 2012
