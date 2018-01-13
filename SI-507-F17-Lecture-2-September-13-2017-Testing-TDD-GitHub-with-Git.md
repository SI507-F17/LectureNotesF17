 # 507 F17 Lecture 2 | September 13, 2017 | Testing & TDD, GitHub with Git

# Admin
- Glad to see people posting on Piazza! Keep it up, help each other, etc.
- Your Project 1 is due September 17th, this upcoming Sunday.
- We have set office hours times — Thursday 2:30-4 PM (see syllabus), and possibly an additional time on Monday mornings (TBA)
- Any questions?


# Collaborating & Testing
- How do you know what a project does? Let’s look at a GitHub repository: https://github.com/openmichigan/OERca for example
- Those instrs — the README
- Such a thing as “README-driven development” (or documentation-driven development)
  - Formalized version of what most people do anyway
  - “What do I want this code to do? What do I want to make sure it does not do?”, etc.


## Markdown

A special way of writing plain text that gets rendered into HTML.

GitHub has a special tool such that when you create a file specifically called `README.md` (“md” is the extension for *markdown* files), it’ll render it nicely, like you saw on that GitHub repository.

To learn about it, you can check out [this Markdown tutorial](https://www.markdowntutorial.com/)!

(And you’ll see soon, later today when you play with GitHub some more.)



# Test-Driven Development (TDD)
- What is it?
- Why is it a good idea?
- (Your homeworks in other classes, sometimes)
- In a software company, you’re relatively likely to either hear about or use it
  - Plus, always useful — even if you’re writing a script to organize 1 CSV file
  - Do it in your head, write it out!
- Readme-driven → test-driven


# Thinking about testing
- How will you describe the code in English?
- What are the specifics of what you want to make sure the code does?
- What are the specifics of what you want to make sure the code does *not* do?
- Make sure you’re specific enough:
  - Test all the things that might go wrong
  - Test things that cover all cases
  - Be careful about *what* specifically you want to test
  
# Python Unittest Module
- gives us a syntax for writing up a test
- let’s break it down

The bold are the things you change

    import unittest # can do this within any Python file -- it's in the standard library

    # depending on other code

    class CodeTests(unittest.TestCase): # making a subclass of unittest.TestCase
      def test_name_of_method(self): # create a method with a name. Must begin with "test"
        # any setup code for this test method
        self.assertEqual(<thing you are testing>, <thing that should be equal to>, <optional descriptive message about what you are testing>) # or another test method with appropriate arguments

    # at the very end of your file
    unittest.main(verbosity=2) #verbosity determines how much info you get

What should you focus on putting there?

## What’s happening here?
- leveraging class definition
- doing a bunch of magic in the background
- (more on this later)
## This is not the only way to test
- Different designs and libraries that allow you to perform them (nose, py.test)
- But this one is built into the standard library (so what we’re using for now)
- A version of this is what powers the tests that you see in some parts of the interactive textbook (e.g. # 1 https://www.programsinformationpeople.org/runestone/static/publicpy3/Classes/ExtraExercises.html)


# Testing Code, Testing Functions, Testing Classes
## Return value tests vs side-effect tests
- does something get changed
  - often, result of class constructors…
- does something get evaluated
- what should be equal to what?
- https://www.programsinformationpeople.org/runestone/static/publicpy3/Testing/Testingclasses.html
# SetUp and TearDown
    import unittest

    class Testing_Card(unittest.TestCase):
      def setUp(self):
        # any code that the rest of the test methods within this class need to rely on, make it an element of the Test Case class
        self.card_test = Card(2,3)
        self.card_test_large = Card(1,12)

      def test_constructor_defaults(self):
        # assert methods go here... e.g.
        self.assertIsInstance(c.cards, list)

      def tearDown(self):
        # e.g. close any files you opened in setup or in tests!


If `[setUp()](https://docs.python.org/3.4/library/unittest.html#unittest.TestCase.setUp)` succeeded, `[tearDown()](https://docs.python.org/3.4/library/unittest.html#unittest.TestCase.tearDown)` will be run whether the test method succeeded / passed or not.

For example: if you have a test that requires items to exist, or certain state - you put these actions(creating object instances, initializing db, preparing rules and so on) into the setUp.

Each test should stop in the place where it was started - this means that we have to restore app state to it's initial state - e.g close files, connections. That goes in teardown.

# Unittest output
- “verbosity”
- what’s happening here?
- using other code — filling in a pattern
- pattern provides us with rules that are specific and rules that are implied (if you want this to happen, you have to… <fill in the blank> — see above)

Let’s see:

- running a test that passes vs
- running a test that fails
  - Same test, different code
# Organizing your test code

Why is this set of code and tests a problem? What’s wrong with it?
What will happen when we test the code?
(Because of how the `unittest` module works/what it expects)


    def subtract_one(num): # this function should return the input, minus 1
      return num - 2 # This function code isn't what we want -- it should fail a test!

    def add_one(num): # this function should return the input, plus 1
      return num+1

    class SampleTest(unittest.TestCase):
      def test_1(self):
        self.assertEqual(subtract_one(4),3)
        self.assertEqual(add_one(3),4)
    # Note that you can write pretty much any test with assertEqual


## Organizing your TestCase subclasses
- Nice to organize them so that when you run a test suite (what a set of tests is frequently called, can also mean other things in other contexts), it’s clear what belongs to what
- e.g. one TestCase class for testing the Deck class in your Project 1, one for testing the Card class …
- Why is this useful?
- If you can put it in one sentence nicely, it’s probably nice as one test method
  - Balance between too much and too little
# assertEqual vs assertTrue, vs assertIsInstance, etc
- many assert statements included in unittest module: https://docs.python.org/3.5/library/unittest.html#assert-methods
- cool, useful, but all possible with assertEqual
- let’s take a look at testing types, for example


     # I want to write a test that the result of function return_tuple is a tuple
     #def return_tuple( ...

     class SampleTest1(unittest.TestCase):
       def test_tupletype(self):
         self.assertEqual(type(return_tuple(a)),type((3,4))) # I know (3,4) is a tuple!

(Better to spend energy on testing the right things than particularly weird or confusing test syntax  now — if assertEqual makes sense and others don’t, stick with that, you’re good to go! It’s basically the root of what all other assert methods do. Just be aware all these are available, and eventually you may want to use them.)

Same goes for setUp — it’s good to know because this style will be expected at a company. However…

# Testing and stress cases
- **What IS an stress case?**
  - Like: stressful for your code, if your code could be stressed (thankfully, it cannot…)
  - For example?


- **How do you decide what to test?**
  - (This is where you think about TDD, descriptions, general testing ideas)
  - Think of it as working backward: practice
  - Try out some other things
  - Think: what is it I’d’ve needed to know before I wrote this code to show you?

- **Take an English description of a function…**
  - What kind of edge cases do you have to be concerned about? What does the documentation not tell you?
    - This is the evolution of a project
      - Documentation
      - Tests
      - Code
      - Iterate: documentation & tests, code…
        - sticking to this pattern will make sure it always *works* (it’s not always easy to stick to!)
      - Combine this with ad-hoc debugging:
        - invoke this, does it work as expected?
      - Try things out — how does this seem? If I write this, and invoke it like this?
        - OK, now add to docs, tests… walk through the formal procedure

  - This stuff plus documentation/spec is a circle, and that’s good. (“What happens if the input is 0? an empty list? The instructions don’t say …”)

  - This is time for *communication* — w/ yourself, your instructors, your project/code-writing partners, people you manage, people you work with, people you design with, your designers…
    - They need to be on the same page as you (— or at least, you all have to know how to get to each others’ pages)

**Take a function described like this:**

> The function best_two_keys should take a dictionary as input. The dictionary will have keys that are strings, and values associated with each of the keys that are integers. The function should return a tuple of the two key strings that have the two highest integer values.

This is missing some stress case description, right? What are the stress cases here that we need to make decisions about?

- Ties — what if 3, 4, 5 have the same largest int value?
- What if the dictionary has less than 2 keys? (1, 0)
- What if a dictionary isn’t passed in the function***
- What if the values aren’t ints, what if they’re both strings, what if the keys are ints or another type — type mismatch, what if some key-val pairs are string-int, but some aren’t **
- What if what’s returned from the function is not a tuple?
- Need to know whether the items in the tuple are strings

What should we test? (in English)

With a neighbor…

**We should test:**

-

**Write at least one of those tests:**





----------

~ ~ ~ ~ ~


# Back to version control
## Review from last week

+506 - F17 | Lecture 1 | Introduction to the course | September 5, 2017  (as a reference)


-  `git init` CREATES a git repository which immediately starts trying to keep track of everything. It can get quite confusing to have git repositories inside others — it is possible! But it can be confusing, and I would recommend avoiding it for now. Only do this inside a directory that represents a project.
- `git status` can never hurt — worst it can do is give you an error if you type it somewhere you don’t have a git repository! Helps you figure out what’s going on.
- Every single character and space is likely to matter, as with all things you type at the command prompt.
- `git` preceding a command at your command prompt means “I’m treating this as a git command” — only some git commands work. So you’ve learned about bash commands — `cd` ,`ls` ,`pwd` , etc. You also use GIT via the command prompt, but it is its own special software. You simply use it with the command prompt.
  - It’s like Python that way — you installed Python 3 in the background, and now when you run programs, they run using the Python 3 interpreter, but you write them using a text editor like Sublime and run them using the command prompt: `python my_program.py` …
  - `git init` to create a repo in a directory to be able to keep track of all the stuff in it, `git add <filename>` to make the git repo keep track of that particular file, `git commit -m "message"` to save a snapshot in time in the git repository with a message that describes what’s true in the project at that moment
## Follow the following steps, reviewing from Tuesday, for a few minutes —
- (First, make sure you’ve created a GitHub account and followed the steps from the Tuesday readings)
- Create a new directory on your computer
- `cd` to inside that new directory
- `git init` to create a new git repository in the directory
- Create a file in the new directory and write a little bit in it…
- Save the file.
- `git add` whatever the file is
- `git status` to see the status of the repo, figure out what’s goin’ on
- `git commit -m "Added initial file"` to make your first commit (could put something else in the message if you want)
    - remember `:q`  if you accidentally open the command line text editor, to get out of it
- Make another change to the file in the directory or add a new file to the directory, save …
- `git add` each file you’ve changed/added
- `git commit -m "Added further changes (or any other specific comment)"`  to make another commit

Also, so you don’t have to log in to github every time, type, at the command prompt:

    $ git config --global user.name "Jane Doe"
    $ git config --global user.email janedoe@example.com

Replace “Jane Doe” with your name, however you want to be identified on GitHub
Replace janedoe@example.com with the email that you want to be identified with
Anything is fine (just don’t assume that these will be private, they won’t be)

This stores your login info so you won’t be prompted for your password as often in the activities we’ll do today & in the future.


## What are you going to do today?

A diagram of explanations…



…but OK, now what?

LAB WORK TODAY: Use these notes as a reference, and try to

- Make a remote connection to a GitHub repository you create (from the Git repository on your computer you created last week)
- Push files to that GitHub repository

(In a bit we’ll get back together and discuss any problems with this, and then you’ll go on to collaborate with a partner.)


## “OK, I have this project with a Git repository that I really like, but I want to be able to work on it on my computer at work, not just my computer at home. What do I do?”


- This is similar to the solution you are currently in. You have a project with a history in a Git repo *on your computer*, but it’s only accessible on your computer. Git, and GitHub, and the tools that Git gives you, can help you with this.
- If you create a repository on the GitHub website and use the proper Git commands and URLs to `push` the repository to GitHub, you’ll be able to access it from any other computer that has Git! (We’ll talk about how in a moment.)
- “GitHub repository” — place online (on the GitHub website) that holds information from a **Git repository** that you have on a computer.

**Follow these steps:**

- Create a new repository on your GitHub account that will be specifically for your project (the toy project you created above):  https://github.com/new once you’re logged in to GitHub. It should look something like this:
![](https://d2mxuefqeaa7sj.cloudfront.net/s_691B72759D1F246404133F2D9706F5B9A38FA78860C1A7DC9E5307A5D8822692_1485377082588_file.png)


Fill in any unique name and brief description (toy-project_<your initials> might be a good name, it’ll be clear and meaningful for you). Keep the repository public. **DO NOT click the checkboxes to add a readme, gitignore, or license right now.** We’re going to follow a specific step-by-step process to get used to git and github, and these will force us to follow a slightly more confusing process.

Then click the green **Create Repository** button at the bottom of the screen. You should be taken to a screen that looks like this:


![](https://d2mxuefqeaa7sj.cloudfront.net/s_691B72759D1F246404133F2D9706F5B9A38FA78860C1A7DC9E5307A5D8822692_1485377411285_file.png)


GitHub gives you a lot of nice hints. But they can be a bit confusing if you don’t know what they mean.

**The second header of theirs pertains to our current situation. We have a repository, but we want to put it on GitHub.**


- Open up your command prompt and make sure you have `cd` -ed  to that directory


- `git status` to check out what the status of things is

Still inside the same directory where your git repo is, type:

- `git remote add origin` + **whatever your link is (GitHub will tell you on this screen!)**
  - For example, for mine above, since I chose to call my GitHub repo **reimagined-potato**, and I’m signed in to my GitHub account, it shows me that I should type (or even just copy right from their screen up there ^):
  - `**git remote add origin git@github.com:aerenchyma/reimagined-potato.git**` ****

This means, translated to English:

> I’m adding a remote place to store my code and connecting it to this git repository on my computer.
>
> I’m calling the remote place  `origin` , which is the default name for a remote place for code to live that is the home place for the code. This is my code, and my git repo, and my GitHub repo and my GitHub account, so I’m calling it **origin** as convention dictates.
>
> This is the special GitHub url that specifies where the **remote place** is located on the internet. It’s now connected to my git repo on my computer that I created earlier.

Finally, you want to *push* the code that you have in your git repository, along with all the history and commits that go with it, TO GitHub (so you can later access it somewhere else).

- `git push -u origin master`

This means:

> Push all of the data currently in this git repository to the remote place called **origin** (on the main “master” branch, which is the only one we are going to work with right now). the **-u** means you’re prompting for a logy in. It may prompt you for your GitHub password.

You should see something like this:

![](https://d2mxuefqeaa7sj.cloudfront.net/s_691B72759D1F246404133F2D9706F5B9A38FA78860C1A7DC9E5307A5D8822692_1485379194504_file.png)


That means it was successful! It’s online! Let’s take a look at it:  e.g. https://github.cogm/aerenchyma/reimagined-potato (This is one I created yesterday, to take the above screenshots)

Cool.


## What can we do with this?

Well, first, it’s a backup for you (more on this shortly). It’s online, not just your computer, and it has the whole history of your project!

It’s also a way for you to collaborate with others. Today, we’re going to look at how you can do a few things (A Preview), like:

- Work on the same project on 2 different computers if you need to
- Take a look at a project I’m working on, for example, that I’ve shared publicly, and decide that you want to work on it on your own computer, but you want to add something to it, you want it to be a little different than what I’m doing


## “I left my laptop at work! 😔 But, I pushed the project I was working on to a GitHub repository. Now, I have another computer at my home, so I want to get it onto my home computer and keep working on it.”

Once a project is on GitHub, you have access to it anywhere as long as you have your login info, are using a computer with git installed, and know how to use git commands! `git clone <git url>` !


- Go to the webpage of the project you were working on somewhere else. (I’m going to go to the mad lib generator code I wrote, which makes madlibs.) https://github.com/aerenchyma/madlib-generator


- `cd` in the command prompt to the place where you want a directory containing that project to go. (I’m going to put it in my `SI206` folder, which is on my `Desktop` .)


- Click the Green **Clone or download** button in the corner of the screen. You should then see something like this:
![](https://d2mxuefqeaa7sj.cloudfront.net/s_691B72759D1F246404133F2D9706F5B9A38FA78860C1A7DC9E5307A5D8822692_1485385239500_file.png)


That text box with a URL that appears is the special git URL from which you can CLONE the repository: get it from GitHub onto your computer, using a git command.

Note that this is NOT the URL in the browser. That URL specifies the place where you can see all this nice stuff that describes the repository. You want to copy the URL in the text box that appears, and then


- `git clone` + **whatever that url is**
- For example, in this case, making sure you have `cd` -ed to the place you want the new project’s folder to appear:
  - `git clone git@github.com:aerenchyma/madlib-generator.git`
  - You can see it follows a pattern: git@github.com + <github username>/<github-repo-name>.git
- You’ll see something like this:
![](https://d2mxuefqeaa7sj.cloudfront.net/s_691B72759D1F246404133F2D9706F5B9A38FA78860C1A7DC9E5307A5D8822692_1485385427487_file.png)


That means it’s successful! You’ve *cloned* the repository from GitHub onto your computer. Let’s take a look at it in the command prompt with `ls` and `cd`  and Finder (My Computer on Windows).


----------

***AN IMPORTANT THING TO NOTE:***
*This* `*git clone*` *step and the* `*git push*` *step we looked at first are NOT bidirectional. That means that just because you* `*git clone*` *something does NOT mean that you can push to it.*

*In this case, if it’s YOUR repository, and you log in, git can connect that it’s the same account. I can make changes inside this folder I cloned, and add them, and commit them, and then push them — no prob.*

*BUT.*

*You could also clone my madlib-generator. Nothin’ stopping you!*

*However, you cannot* `*git push*` *to my madlib generator. Because it’s mine, not yours. It’s under my account.*

*Soon, we’ll look at how you could make changes to the madlib generator and ask me to accept them and put them in my project. First, scenarios to set us up for that.*


## “I’m back at work. But I left my old computer at home, and I did more work on my project last night that I want to continue with now! I pushed it to GitHub, though: I made some edits, then did:
## `git add`
## `git commit -m "Some new very special edits"`
## `git push -u origin master`
## So it *is* on GitHub. How can I keep working on my *work* computer where I left off at home?”

This one you can do in the same repository you’re working with, although you might not see an effect because you haven’t done work that you pushed up to GitHub on another computer.


- `cd` to the correct directory where the git repo is (you’re probably already there now)
- `git pull`
  - This means “Pull down all the changes that are in the remote version of this repository.”


----------

**BE CAREFUL:**
If you had gone back to work, made some changes, saved them, added them, committed them, AND THEN you thought: *Oh no, I forgot that I made some changes last night and pushed them to GitHub, I want to add those in*…

… that can create some problems. Luckily, Git provides you neat abilities to deal with this situation! What might happen is called a *merge conflict:* Git will try to combine the changes in the remote repo on GitHub with the new changes you made LOCALLY, on your computer. And those two might conflict.

We’ll look at how to deal with that later.

For the *moment*, make sure that if you have pushed any work to GitHub that isn’t in your LOCAL version of the repository, make sure you do `git pull` BEFORE you do any new work!

----------


## “My friend Yu-Jen is working on a project that I really like. But I’d like to have my own version and do some different stuff with it on my own computer, and be able to keep track of the work I do on this new version of the project in a repository on GitHub. What should I do?”

**Forking!**


1. On the GitHub website, Fork a repository to YOUR GitHub account by clicking the **Fork** button on someone else’s repository page, like this:
![](https://www.dropbox.com/s/i8jh430i63yxlk3/Screenshot%202017-09-11%2001.27.29.png?raw=1)


[https://www.dropbox.com/s/i8jh430i63yxlk3/Screenshot%202017-09-11%2001.27.29.png?dl=0](https://www.dropbox.com/s/i8jh430i63yxlk3/Screenshot%202017-09-11%2001.27.29.png?dl=0)

1. Follow all the steps to `git clone` above
2. Make edits, `git add` ,`git commit` ,etc
3. `git push` to push your commits to YOUR version of the repository

**Questions? comments? trouble?**


# Exercise
- Find a partner! (You can do this with three if you need to, but it’ll make more sense to have two Person Bs to learn this process than to have two Person As.) No matter what, look at what you’re doing with one another/talk about it together to make sure you understand it.
  - Both of you won’t be doing the same thing, but you should help each other, talk through it, etc.
- One person (Person A) should create a git repository, and add and commit a file to it that has some text in it
- Person A should then create a GitHub repository on their account to hold the data
  - Make a remote connection between the git repository and the GitHub repository
  - And push all the data to Person A’s GitHub repository
- **The other person (Person B)** should log into GitHub and go find Person A’s new GitHub repository online.
  - Careful — GitHub search is terrible. Sometimes it’s best to go to github.com/**theusername** and search for a repository from there, in the person’s repository list.
- Then, Person B should press the **fork** button to *fork* the repository that belongs to Person A.
- Person B should clone from the fork they just made.
- Person B should make a change to the cloned files in their own text editor. Add and commit the change. Push to their fork.

At this point, Person A should have a git repo on their computer and a GitHub repository connected to it, with at least one file that has some data in it.

Person B should have a GitHub repo forked from the repo started by Person A. They should have cloned that repo to their computer, so that now they have a directory that is a Git repository. Both Person B’s git repository for this project and the GitHub repository fork should have at least one more change and commit in the project than Person A does.

(Any questions? Raise your hand, Anand or Jackie will help!)

**Now the brand new part;** *making a pull request*.

> (“Original project creator, I think you should use the stuff I added to your project. Will you pull these committed changes in to your version from mine?”

Person B should go to their own GitHub repository page, online. They should see something like this…

<show live>

Click that **New pull request** button.

Once you get here, look up/make it clear — when a fraction of the class is here, we’ll demonstrate to make sure you see it live, and you can follow along. We’ll supply additional documentation to help with things that we believe will help later.
