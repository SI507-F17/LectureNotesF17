# 507 | Lecture 6 | October 11, 2017 | More on BeautifulSoup, Scraping, Caching

# Admin

New schedule — to be released on syllabus soon
Next up, after fall break: midterm take-home assignment

# Continuing from section

Try using BeautifulSoup on [https://www.lingscars.com/](https://www.lingscars.com/) , doing the following:

- Cache the data
- Extract the Menu
- Extract the names of all cars sold at Lings Cars, grouped by Brand Name
  - (What data structure will you use?)
- Extract each of the deals featured on home page, and this information about each deal:
  - Car's picture/picture URL
  - Name
  - Description
  - Type of Engine
  - Gearbox
  - Paint
  - Rent per month
  - Amount of rent you’d need to pay each year
  - Extract the number of visitors currently (right now — at the moment you cached your data) and number of visitors today (this day, up to the moment you cached your data)
- *How will you store all this data?*

Take a few minutes to think about this problem, write some code, if you didn’t get to do this in section. Check out the website, explore it! Do some visual debugging to think about how you could complete that task.

You certainly do not have to write all of the code to do it, just try to get an understanding of it. (If you finish the rest, do try and complete the code — or think of other things that would be interesting to gather and save from this page!)

After that, get together with someone else and try answering these following questions:


1. **Create an outline of BeautifulSoup code you’ll need to write.**
  1. What questions will you need to answer? What will you need to find out? e.g. what container surrounds the information about each deal on the website.
  2. What is the series of steps, in English, you will need to take?


    -- I want a deal, one at a time
    --- within the deal:
    - the paint (links, found in the class attr)
    - name
    - description
    - rent per month


    from bs4 import BeautifulSoup, Tag

    children_of_element = <some bsoup instance>.children
    for child in children_of_element:
        # each thing child,
        # could be a Tag object -- a BeautifulSoup instance -- something that you can call BeautifulSoup methods on, get BeautifulSoup attrs of
        # could also be a string -- a navigable string
        # for example -- strings have a .find method


**It might be a good idea to define a class of your own to manage this data and save it somewhere else (e.g. writing it to a bunch of CSV files). What class will you define to manage the data?**


  1. What will it be called? What will one instance represent?
  2. What will its instance variables be? Any class variables or no?
  3. What will its methods be?
  4. Any special methods to define — `__str__`, `__contains__`, `__repr__`, etc? Why (or why not)?


Something to examine — there is an example here of using `.parent` and `.children` attributes in a BeautifulSoup object…


    import requests
    from bs4 import BeautifulSoup as Soup

    rtext = requests.get("https://www.lingscars.com/").text
    soup = Soup(rtext,'html.parser')

    res = soup.find_all('span',{"class":"font-blue"})
    one = res[0]
    print(one.parent) # see the result -- too far in, want to go up a level to access...

    # or,

    footnote = soup.find("div",{"class":"makes-footnote"})
    print(footnote.children) # an iterator type!
    # (More on this soon, like the dict_keys, but these we can't just print and see)
    for child in footnote.children:
        print(child)


https://www.crummy.com/software/BeautifulSoup/bs4/doc/

# Using additional modules, broadening your scraping

Scraping is not exclusively BeautifulSoup, though it’s a useful tool. Other tools useful to combine with your knowledge of scraping may be:

- Using and installing additional, new modules, referring to their documentation
- “Crawling”, like you read about in your reading last night, moving from link to link — a tiny version of which you’re sort of doing in Project 3 (but with caching — crawling amid one domain can be very hard on that website’s server!)
- Additional scraping modules (there are a number of others) and modules that allow a program to ‘act’ as a browser, like [Mechanize](https://pypi.python.org/pypi/mechanize/)
- Other types of scraping, many of which rely on the markup language XML, which you read about, and [XPath](https://www.w3schools.com/xml/xpath_examples.asp)
- Other types of code structure
- More complex data storage

We don’t have enough time in this course to look at all of these in detail, but the skills you learn practicing BeautifulSoup and planning BeautifulSoup programs that integrate with other code will be helpful in learning many of these and practicing them, since they address similar or identical markup language and have somewhat similar library documentation to unpack and figure out.

Those last two, we’ll be doing more with in ensuing weeks.

But relying on some other modules, that there are some cool examples for. Here’s on, which of course you could make much more complex:


## Exercise
1. Use the wikipedia module to retrieve the HTML of the Harry Potter Wikipedia page (you’ll need to `pip3 install wikipedia`, or create a virtual environment, activate it, and install the `wikipedia` module in it
  1. HINT: To use it, look at the `page()` function it has, and the  `html()` method of a page object…
  2. Documentation: https://pypi.python.org/pypi/wikipedia
2. Create a BeautifulSoup object using this HTML
3. Write a function `print_section_titles()` that accepts a Wikipedia page BeautifulSoup object and prints out all the section titles in a numbered list
  1. HINT: ‘Inspect’ the Wikipedia page in your browser to see how section titles are created in HTML
  2. HINT: use `find_all()` to retrieve tags by CSS class
  3. HINT: use `get_text()`  from the `wikipedia` module
  4. Call `print_section_titles()` for the Harry Potter page — The first few lines of your output should look something like this (may NOT have the same text):

> 1 Plot
> 2 Early years
> 3 Voldemort returns
> 4 Supplementary works
> 5 Harry Potter and the Cursed Child

Write a function `print_references()` that accepts a Wikipedia page BeautifulSoup object and prints out all references in a numbered list

  - Call `print_references()` for the Harry Potter page
  - The first few lines of your output should look something like this (may NOT have the same text):


> 1 "Harry Potter and the Cursed Child to be eighth book". BBC News.
> 2 Peter Svensson (27 March 2012). "Harry Potter breaks e-book lockdown". Yahoo. Retrieved 29 July 2013.
> 3 Allsobrook, Dr. Marian (18 June 2003). "Potter's place in the literary canon". BBC News. Retrieved 15 October 2007.

**CHALLENGE:**
Write code that allows these functions to be called interactively — a user enters a search term, and then sees the section headings and the references printed out.

**ADDITIONAL CHALLENGE:**
Pick more details of information that should be printed out from any given Wiki page, and write a function to access and print those.

**ADDITIONAL EVEN HARDER CHALLENGE:**
Then, write code that will handle disambiguation in your function. For example, if you search “Harry”, you should get a prompt asking you to select which of the possibilities for “Harry” you actually want the page for, of all the possibilities Wikipedia comes up with. (Here’s an example of that disambiguation page that you could work with… https://en.wikipedia.org/wiki/Harry … but you can get there even faster using the `wikipedia` module — try out some examples with the documentation!)

May want to consider — how are you going to handle this interactive experience? How should you organize your code? How are you going to break the problem up into different functions?


# Taking a look at how to approach this

We’ll also post solutions later.


    import wikipedia
    from bs4 import BeautifulSoup, Tag

    harry_wiki_page = wikipedia.page("Harry Potter")
    harryp_html = harry_wiki_page.html()
    soup = BeautifulSoup(harryp_html)
    print(soup.prettify())
    # https://en.wikipedia.org/wiki/Harry_Potter

    sample_wiki_disambig = wikipedia.page("Harry")
    sample_html = sample_wiki_disambig.html() # invoke html method on page instance
    sample_soup = BeautifulSoup(sample_html)



# More on caching and complex code structure

https://www.programsinformationpeople.org/runestone/static/publicpy3/UsingRESTAPIs/cachingResponses.html

Examining the function(s) you saw in Project 2:


    import json, requests

    def params_unique_combination(baseurl, params_d, private_keys=["api_key"]):
        alphabetized_keys = sorted(params_d.keys())
        res = []
        for k in alphabetized_keys:
            if k not in private_keys:
                res.append("{}-{}".format(k, params_d[k]))
        return baseurl + "_".join(res)


    def sample_get_cache_itunes_data(search_term,media_term="all"):
        CACHE_FNAME = 'cache_file_name.json'
        try:
            cache_file = open(CACHE_FNAME, 'r')
            cache_contents = cache_file.read()
            CACHE_DICTION = json.loads(cache_contents)
            cache_file.close()
        except:
            CACHE_DICTION = {}
        baseurl = "https://itunes.apple.com/search"
        params = {}
        params["media"] = media_term
        params["term"] = search_term
        # params["sort"] = "popular"
        unique_ident = params_unique_combination(baseurl, params)
        if unique_ident in CACHE_DICTION:
            return CACHE_DICTION[unique_ident]
        else:
            CACHE_DICTION[unique_ident] = json.loads(requests.get(baseurl, params=params).text)
            full_text = json.dumps(CACHE_DICTION)
            cache_file_ref = open(CACHE_FNAME,"w")
            cache_file_ref.write(full_text)
            cache_file_ref.close()
            return CACHE_DICTION[unique_ident]



## **Questions for us to address**


- What is this code doing? At a high level?
- In more specific detail, function by function, line by line?
  - Try to add comments (in your own file, not this one) — for those who took 506 or completed the waiver assignment, this is a refresher! What is each line of each of these functions doing?
- What is the utility behind this overall setup for saving data from the internet?
- -- A larger question: What is caching, really?
- What are the downsides? the upsides? of this setup for “caching”?
- How could you write code in a program that does *exactly the same thing as this code* (so, not addressing some of those ‘downsides’ challenges yet) — but in a different way? What might be worth changing, and why?
- How could you write code using this pattern to cache data for scraping, HTML data? What might need to change? How?
