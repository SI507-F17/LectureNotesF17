# 507 | Lecture 7 | October 18, 2017 | Caching, Python specifics (iterators, generators, collections libraries)

# Admin
- Project 3 was due last night (hopefully not news)
- Your take-home midterm assignment is released
Any questions?


# Back to caching

You’ve seen a couple kinds of caching at this point, simple and otherwise, various in a number of ways. Today, I want to dig in a little more to how caching varies, why it’s important, and how we can adapt to some of the tradeoffs caching data introduces (as well as how we can’t really).

**A cache:** *a hardware or software component that stores data so future requests for that data can be served faster*

The type of caching we’ve seen so far is: storing data in a file on your computer so you can access it without having to make a request to the Internet, which takes power, an internet connection, and often, more time than it takes to open a file saved right on the computer.

You often encounter some form of *caching* when you deal with data on the internet and accessing it on a personal computer. Browser caching, for example — https://varvy.com/pagespeed/leverage-browser-caching.html  (more about it here)

Here’s a Wikipedia article about cache computing: https://en.wikipedia.org/wiki/Cache_(computing)

But we’re not running scripts on the internet at this point, so the form of caching we’re doing is creating a local duplicate of data from one point in time, so it’s:

- easier to access — faster
- easier to access — possibly a simpler operation
- safer to access — can’t crash a site by hitting it too much
- safer to access — can’t get blocked by an API rate limit

**The caching you’ve seen so far introduces some tradeoffs:**

- If you cache data, you only have that data — not new data. What if the data online changes frequently?
- If you cache data, you only have that data — not new data. What if data that *follows* from that data changes — e.g. what’s on the other end of a link, or what selector is included in the HTML…?
- If you cache data, you only have data from the moment in time at which you cached it — what if e.g. you cache data from a Twitter API, but the tweets on J.K. Rowling’s account at the moment you searched weren’t really what you were looking for?
  - e.g. @umich and images …

**There are some ways to address those tradeoffs usefully — but only some:**

e.g. the pattern you saw in section this past week: https://github.com/SI507-F17/section-week-6

**Check out** `**nytimes.py**`**, lines** 11 - 115**, again.**

**Answer these questions with a neighbor — come up with answers you’re willing to share:**


- **What decisions do you have to make when writing code like this?** Give a couple of examples. One is “How many functions do I need to define to set up a caching pattern?” Another might be “What should I call  the functions I’m defining?” but there are many…
  - Might have limitations/problems with file size — might want to separate into different files
    - How are we going to check that?
  - Make sure that the function definitions are very clear — need to make sure that you know what you’re doing, what your code will, and should do, what you expect from it
  - Expiration: need a system in mind — what’s the logic behind the system
  - How long is an article or HTML valid?
  - Why is the expiration important?
  - How many functions should there be?
  - What format should the dates be stored in?


- **What are some of the benefits to this system in comparison to the system we saw two weeks ago, when we started looking at scraping & BeautifulSoup?** Come up with at least 2.
  - It depends! Newspapers, for ex, have a lot of diff by day — sensitive to time, while NPS info may not be so sensitive to time.
  - New system leverages power of computers more (human can see that there’s a file…)
  - More automated — the person never has to go delete the cache when they invoke the code
  - It’d be easy to set up a backup — e.g. cache is deleted — actually, copied to another storage location
  - You can e.g. set different expiration dates for different data you have different ideas about, want to expire at diff times
  - Layer complication on top of it
  - It’s broken into many functions — so you could change the arch of the system, but reuse a bunch of the code you wrote


- **What are some of the** ***downsides*** **to this system in comparison to the system we saw two weeks ago with a simpler single try/except statement?** Come up with at least 1.
  - Multiple functions — can get kind of complicated in case it’s not working, possibly harder to debug
  - It’s just long! Which can be a real downside — debugging or writing
  - Might be harder to share/port to another person’s computer
    - Depends on your system setup
    - If you’d edited it to — for example, if you weren’t careful about where you’re saving old data, and you specify something that’s unique to one computer, you could be in trouble


- **If you were scraping a website and using a caching system like this, what might you need to know about the website or its maintainers to make your system work in the best way possible?**


- **What about if you were using a system like this to cache data you gathered from a REST API (or multiple APIs)? What might you want to know about the APIs you were relying on?** You should try to come up with at least 2 or 3 things — they can be really simply explained; they’re still important!


# Refactoring & caching

Refactoring is a process of re-organizing code, as we’ve discussed before, to make it “better”… in some way.

What does “better” mean?

It all depends on your context.

- Faster to run / Big O notation (not in this course)
- Fewer requests
- Less computer memory it occupies while running
- Easier to run
- Easier to understand later, for you
- Easier to understand, for someone else (in general, or a specific person/group of people)
- Easier to maintain
- Easier to change
- Fits more neatly into another project
- Allows for more functionality to be included in the project
- More modular
- …etc.

**Where are the tradeoffs?**

Frequently, some of the interesting tradeoffs are between modularity and over-complication. Refactoring takes serious time and effort.

Sometimes, there are tradeoffs between time it takes to run a program and e.g. how easy it is to write, or how easy it is to read.

(Details of efficiency of a program are something you’ll look at more if you take SI 618, and get tools to really dig into details of how efficient a program is — because when you deal with a *large* amount of data, that makes a big difference.)

If you’re dealing with even a medium-size amount, that doesn’t always matter so much — but you have to know: what do you have to do to achieve your goal for your programming project?

But you can see some differences when you look at “the caching pattern” we’ve introduced in SI 506 / that you can read about in the textbook, and compare it to what you did for BeautifulSoup a few weeks ago, maybe in your Project 3 as well, vs what you see in the Section 6 exercise, etc, etc.


- What is happening in the Section 6 code that’s different from what you see in the textbook? How does it address one of the problems we talked about before, that caching can cause?


## **Exercise**

How could you change this code, similar to code you’ve seen at least once before (if not many times!) to do *exactly the same thing* **but be arranged a little differently**?

  - It’s like revising an essay in English: how would you suggest revising this code, so it basically has the same outcome? **Try to come up with an alternative bit of code that does what this does.** As you do this, you should think about your reasoning: why do you want to change it — what is better about your way of writing the code than this way? Or even: what’s not better about the way you’ve changed it, what do you prefer about this given way?


    CACHE_FNAME = 'cache_file.json'
    try:
        cache_file = open(CACHE_FNAME, 'r')
        cache_contents = cache_file.read()
        CACHE_DICTION = json.loads(cache_contents)
        cache_file.close()
    except:
        CACHE_DICTION = {}

    def params_unique_combination(baseurl, params_d, private_keys=["api_key"]):
        alphabetized_keys = sorted(params_d.keys())
        res = []
        for k in alphabetized_keys:
            if k not in private_keys:
                res.append("{}-{}".format(k, params_d[k]))
        return baseurl + "\_".join(res)

    def get_from_datamuse_caching(rhymes_with):
        baseurl = "https://api.datamuse.com/words"
        params_diction = {}
        params_diction["rel_rhy"] = rhymes_with
        unique_ident = params_unique_combination(baseurl,params_diction)
        if unique_ident in CACHE_DICTION:
            return CACHE_DICTION[unique_ident]
        else:
            resp = requests.get(baseurl, params_diction)
            CACHE_DICTION[unique_ident] = json.loads(resp.text)
            dumped_json_cache = json.dumps(CACHE_DICTION)
            fw = open(CACHE_FNAME,"w")
            fw.write(dumped_json_cache)
            fw.close() # Close the open file
            return CACHE_DICTION[unique_ident]

(Almost exactly from https://www.programsinformationpeople.org/runestone/static/publicpy3/UsingRESTAPIs/cachingPattern.html )


Thoughts to share?


## One nice takeaway

Really takes you back to — how are you going to plan your code? How are you going to plan your program? How are you going to understand, or change, or test, someone else’s code?

These are really difficult skills to build — it takes a long time to get good at, and it’s also something many people do in very different ways.

And of course: really important ones for a developer working on a team, really useful to figure out what approaches work for you to get to a place where you can collaborate with other designers, developers, managers, scientists, researchers, teachers, statisticians, stakeholders, whomever! even if they use a different system of understanding complex projects.

# re: Refactoring — Code review and collaboration on GitHub

We’ll be looking at this even more this coming week — but there are a lot of features on GitHub that allow for useful collaboration, as well as the features that allow you to help with your own work, like those you’ve been looking at in sections over the past few weeks! https://github.com/features/code-review



# Iterators & Generators
## How do these different types of things in Python relate to one another?

From http://nvie.com/posts/iterators-vs-generators/:

![](https://d2mxuefqeaa7sj.cloudfront.net/s_85F41601BD3B6043AC23881151E1CA565EF9660E67E703770B2D5209E4261FDF_1489370183010_file.png)

## **What is an iterator?**

An iterator is just any old Python class, but one that defines an `__iter__`  method and a `__next__` method, both special methods like `__init__` and `__str__` .


![](https://d2mxuefqeaa7sj.cloudfront.net/s_85F41601BD3B6043AC23881151E1CA565EF9660E67E703770B2D5209E4261FDF_1489370582966_file.png)

## What does that mean, though?

Really basically, it’s something you can *iterate over* — something a for loop will work on.

Many instances of classes can also be treated as iterators, *because you can iterate over them*. `for <var> in <iterable seq>` , for example…

There are a lot of different subsets of iterators — some of which you’ll see later in this lecture. There’s a `map` thing that’s an iterator and a `dict_keys`  thing that’s an iterator… on and on. (Examples shortly.)

Use the `iter()` function to make stuff into iterators.

Just like making things into Integers with `int()` , this doesn’t work on everything! Only things that are valid to be turned into iterators.


## So…

When you learned about Python for loops, you learned that they have this magical-seeming property of a “hidden assignment statement” in them — the loop just always *knows* what the *next* element is, and it knows when it’s done.

The “iterator variable” in a for loop is bound, sequentially, to each thing in the sequence you’re iterating over in the for loop!


    for iterator_var in sequence:
        ...code
    # whatever is outside the loop..

In the background, this is because of iterators.

While this is not *quite* what’s really happening, it’s a lot like: a list or string, when you put it in a for loop, is converted to an iterator so it’s easy for the for loop to know what the *next* thing is every time.

Examine some code that shows the difference between a sequence like a list and an iterator…

From https://www.programiz.com/python-programming/iterator

    # define a list
    my_list = [4, 7, 0, 3]
    print(my_list[2])
    for elem in my_list:
      # do something e.g.
      print(elem)

OR


    # get an iterator using iter() function built-in to Python
    # makes these special functions like __next__ work properly on it...
    my_iter = iter(my_list) # iterator type

    ## iterate through it using next()
    my_list = [4, 7, 0, 3] # from before, cast to iter
    #prints 4
    print(next(my_iter)) # my_iter.__next__()

    #prints 7
    print(next(my_iter))

    ## next(obj) is same as obj.__next__()

    #prints 0
    print(my_iter.__next__())

    #prints 3
    print(my_iter.__next__())

    ## This will raise error, no items left
    print(next(my_iter))

    # For loop does all this behind the scenes!

    # Every time you do another round of the loop, what's happening is that the __next__ method got called on the iterator-version-of-the-sequence, but you don't see it happening.

**Iterators take up a lot less memory than lists.**

The difference is sort of like
*Drawing out a map of a trail on a piece of paper* (a list)
vs
*Having extremely clear trail directional markers and  signage on the roads to get you to the start of the trail.* Each time you get to one trail marker, it’s *completely obvious* how to get to the next one, so you don’t have to bring a map, or do all the work of keeping this big foldable thing in your pocket (an iterator)

You can cast an iterator to a list (the map/trail markers analogy doesn’t hold up as well here, unfortunately, it’s imperfect!).


## **What is a generator?**
## http://nvie.com/posts/iterators-vs-generators/
## **A generator is a function that produces a sequence of results instead of a single value.**

Any generator is also an iterator! **so it is also a factory that “lazily” produces values when something causes it to be asked for one**. (Something that causes an iterator to be ‘asked’ for a value: a loop… or an invocation of `next()` …)

    def show_new_range(n):
        i = 0
        while i < n:

        yield i # Yields a new one each time, doesn't store them all in memory in the same way

    e        i += 1
##
## Types of generators

There are two kinds of generators in Python: generator **functions** and generator **expressions**.

Generator functions are a little like a convenient shortcut for building an iterator object definition. More here: https://wiki.python.org/moin/Generators


# Why does this matter?

Iterators are all over the place in Python 3, because they save a lot of memory in the long run, which matters when you’re dealing with huge amounts of data, for one thing. Also make it easier (though with small programs you won’t really notice the difference) to run your Python programs!

The designers of Python decided this would be an important feature to add — so `.keys()` returns an instance that is an iterator. `range()` returns an iterator. `map()` and `filter()` and `zip()` functions return iterators (you can read about them: https://www.programsinformationpeople.org/runeston e/static/publicpy3/AdvancedAccumulation/intro.html) — Though for `map` and `filter`, you can do all that with list comprehensions easily. `zip` is a little more useful (while you CAN do what zip does in other ways, none of the other ways are quite as easy)

The `zip` function combines multiple lists into **one iterator that contains info like** a list of tuples:

![gif showing the process of the zip function running on 2 lists of the same length.](https://d2mxuefqeaa7sj.cloudfront.net/s_3B921EDB905D95F5A99920797F82EA5AD609CD23BC726AAB2DA876C61594AA3A_1487788579130_zip.gif)


“**Filtering**” a function on a list means returning an iterator pointing to elements for which, for each of them, some condition is true. Remember:  `filter` returns an iterator!

![](https://d2mxuefqeaa7sj.cloudfront.net/s_3B921EDB905D95F5A99920797F82EA5AD609CD23BC726AAB2DA876C61594AA3A_1487786187996_filter.gif)

# Generator functions

Any function in which the keyword `yield` appears in its body — that’s all you need to make it a generator function  ( **— a lazy factory, where the thing that makes it go is the line with the yield keyword getting evaluated in the sequence of code evaluation**).

So, why generator functions? What can you do with them, and why would you use them?

**From http://anandology.com/python-practice-book/iterators.html …**

    def integers():
        """Infinite sequence of integers."""
        i = 1
        while True:
            yield i
            i = i + 1

    def squares(): # Invoke another generator inside here...
        for i in integers(): # In this line!
            yield i * i

    def take(n, seq):
        """Returns first n values from the given input sequence, which could be an iterator... and will be cast to one if it is not."""
        seq = iter(seq)
        result = []
        try:
            for i in range(n):
                result.append(seq.next())
        except StopIteration: # Dealing with iterator
            pass
        return result

    print(take(5, squares())) # prints [1, 4, 9, 16, 25]
    print(squares()) # <generator object at x0dsfdsfds>

How would you write code that does the same thing without knowing about generators and iterators, using sequences and accumulation? (Not too different — in fact, less complicated…)




What if you had to do it for a sequence with many, many, many thousands? Takes a long time…

Probably can’t even do this (holding 1,000,000 integers in memory during your program) — computers have limits (and personal computers have pretty strict ones!) May crash, somewhere down the line…

    # Build and return a list
    def firstn(n):
      num, nums = 0, []
      while num < n:
        nums.append(num)
        num += 1
      return nums
    sum_of_first_n = sum(firstn(1000000))

But this is fine:

    # The same, with a generator that yields items instead of returning a list
    def firstn_gen(n):
      num = 0
      while num < n:
        yield num
        num += 1
    # <generator object at x0sdfasdf>
    sum_of_first_n = sum(firstn(1000000)) # Fine!

Summing 1,000,000 integers, 0-1,000,000, takes  approx 3 times the amount of time with normal iteration than with a generator on my computer, for example.

Which is to the tune of seconds, but summing integers is a tiny bit of data, so you have the slightest more complicated thing… you are REALLY going to notice.

(Depending on a variety of things about your personal computer, both of these may work — but you can keep adding more zeroes until one takes muuuuch longer than the other, at least.)


## Overall: why generators?
- Fewer intermediate variables, containers, data structures…
- More memory-efficient (efficient for your computer memory)
- More CPU-efficient (efficient for your computer processor)
- Really nice for replacing complication accumulation patterns that take a lot of memory/comparably a lot of time! (Which is the basis for everything, almost…)

Not that you should abandon accumulation forever — but be aware of these, because they can allow you a lot of power for working with immense data in a small program. (Lots of numbers, for example.)

**Another nice resource:** https://jeffknupp.com/blog/2013/04/07/improve-your-python-yield-and-generators-explained/

For example…

    l = [3,4,6,5,7]
    iter_l = iter(l)
    for i in iter_l:
        print(i)

    print(list(iter_l))
## **Exercises**
- Write a program that takes a filename and prints all the lines in that file which are longer than 40 characters, using an iterator or generator



- Write a function `peep`, that takes an iterator as argument and returns the first element and an equivalant iterator. (for example, `peep(iter([1,2,3])` `# should return 1, <iter with 1,2,3>`





- The built-in function `enumerate` takes an iterable object and returns an **iterator** (in Py3) over pairs (index number, value) for each value in the source.

**e.g.**

    >>> list(enumerate(["a", "b", "c"])
    [(0, "a"), (1, "b"), (2, "c")]
    >>> for i, c in enumerate(["a", "b", "c"]):
    ...     print(i, c)
    ...
    0 a
    1 b
    2 c
- Write a function `my_enumerate` that works **exactly** like `enumerate`


# (if time) Libraries/Modules that provide you with more Python power
## collections

https://docs.python.org/3.5/library/collections.html
Provides a bunch of new and useful containers, e.g.

Named tuples:

    import collections

    Point = collections.namedtuple('Point', ['x', 'y']) # sets up a named tuple called Point
    p = Point(11, 22) # or Point(x=11, y=22) OR Point(y=22,x=11) .. positional or keyword args
    # For those who know C++, this is a bit like a struct -- a simple object where you still want it to have a name in your program
    # But can't have methods on a named tuple the way you can on a class!

This is more on the “art” of programming, aspects of creativity: you have to decide what best suits your program’s needs, although there are many ways of doing this stuff.

**Default dictionaries:**

    import collections

    diction_listvals = collections.defaultdict(list) # means the base vals of any key in diction_listvals will automatically be a list, if you know that's what you want

    s = [('yellow', 1), ('blue', 2), ('yellow', 3), ('blue', 4), ('red', 1)]
    for k,v in s:
      diction_listvals[k].append(v)
    print(sorted(d.items())
    # prints: [('blue', [2, 4]), ('red', [1]), ('yellow', [1, 3])]

Fancy! 😄

Way more, too…
Check out Counters: https://docs.python.org/3.5/library/collections.html#collections.Counter


## Exercise

How would you write code using a `Counter` from the `collections` library to determine what the most common character is in a string `s` ?


    import collections

    s = "supercalifragilisticexpialidocious"






## itertools

https://docs.python.org/3.5/library/itertools.html
This module is full of functions that create nice iterators for super efficient looping over objects, basically, sometimes in quite complicated ways.

`cycle` , for when you don’t want to reach the END, just want to loop over the same thing again and again in a fashion (`cycle` object is an iterator, just go next forever, won’t encounter a `StopIteration` error, it just goes back to the beginning — so iterating over it is an infinite loop! Finally a way to have an infinite loop with a for loop…): https://docs.python.org/3.5/library/itertools.html#itertools.cycle

`permutations` , super useful for anagram word games… https://docs.python.org/3.5/library/itertools.html#itertools.permutations

`zip_longest` — like `zip` , but provides nicer functionality for if the lists you zip together aren’t the same length, there’s a filler value to match up with the elements from the longer list that don’t have a partner…

Some neat examples: http://programeveryday.com/post/using-python-itertools-to-save-memory/

Here’s one example of manually detecting anagrams: http://www.interactivepython.org/courselib/static/pythonds/AlgorithmAnalysis/AnAnagramDetectionExample.html (This page also goes into some algorithmic detail that you have NOT been introduced to in this class, so don’t worry about it)

But here we have a nice neat solution using this tool, as long as we have some solid boundaries…

    import itertools
    s = "HALLEYSCOMET"
    possibilities = itertools.permutations(s) # tuples of chars, basically, in an iterator
    for x in possibilities:
      wrd = "".join(x) # compose the tuple into a string again
      if x.upper() in ["".join(x.upper().split()) for x in list_of_phrases]:
        print(x) # print out any possible word from a list that shows up...

    print(len(list(possibilities))) # a LOT...!
    # This is something computers are good at and humans are not always...

    # Cool anagram (given that spaces don't matter -- what in above code ensures that?)
    # HALLEYS COMET
    # SHALL YET COME

    # Still have to do some work to make this work -- itertools isn't pure magic
    # But it does help you get somewhere neat!
    # And it can certainly help you solve data problems, or big computation problems


How many permutations are there? → You might do math wrong in your head; you might mistype a formula; sometimes those are still the right way to go -- but this will not be wrong.

And tons more opportunities in both of these modules, many of which you’ve probably written code for, essentially, either in this course or in another course.

These are more memory-efficient than most of the things you’ll write/have written — BUT it’s very difficult to use them if you don’t have a very solid idea of what you want to do, which comes from thinking about algorithms for solving problems manually.

All these rely on iterators, and some on generators specifically. Check ‘em out in more detail… you’ll see them again in some future code! (When we use them in future we’ll go into more detail.)


----------
# **Additional Notes**

**Iterables vs Iterators vs Generators**

- Iterables are python objects or data structures that can be used like `for x in iterable`
- Iterators are python objects that define `__next__(self)` and `__iter__(self)` methods for lazily loading values, thus saving runtime memory, so that you can use next(iterator) and iter(iterable). When you use `for x in iterator`, it implicitly calls
  `x = next(iterator)` for each iteration of the loop.
- Generators are an elegant way of writing iterators through functions, instead of objects.


> Think of iterators as ‘turnstiles’ at New York Subway. They only allow you to enter the station one at a time. The next method turns the turnstiles. The system does not see who is going to pass through the turnstile, till the turnstile is turned. Does that make sense? 🙂
