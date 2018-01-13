# 507 F17 Lecture 1: September 6 | Introduction, Project Collaboration

# **Welcome to 507!**

To see these notes on your computer: Canvas site → Pages → Lecture Resources

# **Collaboration in programming**
- What does it require?
- What does it demand of collaborators?

If you work in, surrounding, adjacent to technology or software, if technology or software of some fashion is something you use in your work, if your work is collaborative and uses technological tools — and at least one of those things will be true of almost all UMSI graduates — these are questions to be asking, and they’re questions we are going to ask in this course.

More accurately, we’ll be providing some possible answers and tools for supplying them in this course. These are things to think about. **What do you need, for skills and tools and understanding, to collaborate?**


- You need to know what you need to know
  - What you need to install, use, etc
- You need to install whatever tools you need installed
- You need to understand others’ goals
- You need to know how your skills and understanding can fit into the project, and/or which you will need to build.
- You need to know *what you* don’t *know*.
- You will need to access the code that’s being collaborated on.
- You will need to make your own contributions and share them.
- You will need to get updates from other people working on the project (ideally without a big email mess / confusion)
- You will need to get your work reviewed (code, in our case, in general, sometimes documentation)
- You will need to make your code, documentation, and other work you do on the project understandable and accessible to others
- You will need to understand the progress others have made or are currently working on, so you don’t do the same thing as someone else separately and create conflicts (literally or figuratively)
- You will need to know if the work you do on the project works as you expect it to / as others expect it to (“I think I fixed the problem you’re talking about!” / “Are you sure? What about when..”)

Our first couple weeks will take a look at these questions.

- Virtual Environments and project structure (some today!)
- Unix command review and use (some today!)
- Unit testing, stress cases (next week)
- Code documentation (next week)
- Version Control: Git and GitHub (some today!)

And more…

But we won’t stop thinking about these things in 507 after the first assignment is over. This is a course theme, and I find it a helpful larger theme.

# **Introductions**

**My name is Jackie Cohen. You can (and should) call me Jackie. I use the pronouns she/her/hers.** I am a Lecturer III at UMSI and the faculty instructor for this course. Ultimately, the decisions about course policy in this course are mine.

Many of you may know me from SI 506, either last Fall or last Winter. For those who don’t, a little bit about me…


- My primary appointment here at UMSI is teaching. This semester, I teach three courses. Other parts of my work include research on computing education and research in the School of Social Work, and contributing to open source projects with other faculty members here and elsewhere.
  - Before I was a lecturer here, I was a software engineer at a startup, where I did most of my work in Ruby -- which is a programming language that is quite similar to Python in many ways. I’ve worked in many different languages, but Python is my favorite, and I’m excited to continue sharing it with all of you.
  - Before that, I was a data analyst… and before that, I was an MSI student!
  - My undergraduate degree is in Linguistics. I know what it’s like to take a programming course with no prior experience; I started programming in college.
- You can feel free to ask me about course options, internship and job decisions, programming interviews, study strategies, and other things like that, even if they are not about this course, and I am happy to talk to you about those things in individual office hours appointments.
- I expect your honest feedback to make our class better. This is my class, but it is also yours. I won’t necessarily agree with your opinions, but I will listen to them. We’ll have opportunities to give feedback, anonymous and otherwise, and I would like your constructive, thoughtful opinion about what you need in this course, so I can take what I hear and compile it into something I believe will be useful for you. I’ve made most of my course decisions based on a combination of personal experience, past feedback, and external research, and I am always willing to answer the “why are we doing this?” question.
- I am better at faces than names, but I’m okay at names, and I am paying attention to your preferred name to be called and the pronouns you use.  Know that I welcome correction, either publicly or privately (whichever you are comfortable with) if I call you something pronounced incorrectly, etc! I usually get everyone’s name a few weeks in in a 40-person class, but I’ll definitely remember you. Some of you I know from other classes!


**You have one GSI:  Anand Doshi (pronouns: he/him/his)**.
He is a 2nd year MSI student specializing in HCI. Previously, he worked as a full-stack developer (full-stack == front end *and* back end work; back-end programming is closer to what we’ll be doing in this class, and what was done in 506) and has worked with Python for over 5 years.

He will be leading your section, whichever section you are in, and you’ll also see him in office hours and in lecture.

**You also have one Instructional Aide:  Tianshi Wang (pronouns: he/him/his).**
He is a 2nd year MHI student. He will not generally be here during lecture, but you may see him during office hours.


# **Course policies & expectations**

**First, there will be material today!** Not going to let this time period go to waste…

**Second, before we get there:**

- You should read the syllabus in detail. You’re expected to know the policies that are written in it. If there are changes to it, we’ll announce them.
- Also, there’s a google form in the assignment Syllabus Questionnaire on Canvas. You should read the syllabus and fill that out!


## **Overview**
- **HW/Project based course.** There will be approximately one project for each of the major units of material we’ll cover in this course (five or six projects). These will usually be due on Sundays. Some you’ll have about a week between learning the material in class and the deadline, some there will be almost two weeks. This will depend on the size of the project.
- **One midterm (take-home, with an honor code), one final project, no final exam.**
- Occasional weekly assignments that are small and correspond to the reading / showing an understanding of material / offering explanations.
- **Expectation of attendance in both lecture and discussion.**
  - Your time is yours, lecture is not for points, but **you are expected to know material talked about in lecture** and to catch up with the notes, etc, if you can’t attend.
  - **Discussion section attendance is required and is for points.** In discussion, there will be supplemental activities and support for projects. There will be some opportunities to waive a discussion section if you have completed a project early but you are always welcome to attend.
- **You are expected to complete the readings, if any (usually there will be some) before lecture each week. Lecture will expect that and welcome questions on them.**
  - We meet only once a week. This is the chance you have to study the material with me as a resource. Take advantage of it.
- **Three hour lectures**
  - Lecture won’t just be me talking. There’ll be a lot of activity, code writing, participation, pairing up, thinking about activities, talking, trying things out. We’ll build in one or two breaks in each session, which will vary depending on what we’re doing.
  - Come prepared to engage with material. I can wait: this time is for you more than it is for me. I expect you to come ready to ask questions and answer mine.
  - You never have to speak in front of the whole class, you may always “pass”. If you never want me to call on you in class, please speak with me privately and tell me so, and I won’t. However, I encourage you to unless it is a really unpleasant experience for you. This course is in many ways about preparing you to join a software team or company (even if you are not programming in that setting)
- **Communication in this course**
  - This is an important section of the syllabus. If you read nothing else, read this!
  - But seriously, read the whole syllabus.
- **Piazza**
  - A valuable and important resource. Please do check it, and please do ask questions on it. We will be monitoring it to help out and answer questions.
  - Answer each other’s questions! Best way to learn (and nice for getting to know each other)
  - We don’t have a lot of class time! But we always have the internet…
- **Canvas Announcements**
  - You should make sure you will receive emails when we send these (this is the default, you should if you have not specifically changed any settings or filtered out the emails). They’re important and they won’t be sent frequently. If you were on the Canvas site (if you are registered and not waitlisted) you should have received my welcome message!
- **Questions?**


# Why this course?

This is an Intermediate Programming course, so everyone here has either taken SI 506 or waived SI 506. Depending on your background, some topics in this course may be a little bit familiar to you, some may be brand new. (If you know a little bit, share your knowledge by helping others and sharing how you understand these concepts on Piazza, I’m sure it will be appreciated.)

This is a course for those who want to move beyond SI 506 and think not only about how to solve your own problems with code, but how to apply code other people have written to your own problems, and how to iteratively improve your solutions.

SI 506 is a course about learning and practicing the skill of programming and problem-solving in a way that will help you program and solve other programs that involve symbolic systems and computational thinking.

SI 507 (this course) is a course about building on your introductory programming skill to build skill and experience in using programming tools, build a more rigorous understanding of the Python language (which will help you have a more rigorous understanding of any other language/system), and gain practice and skills that will allow you to collaborate on programming and technology projects in productive ways, and move on to higher level, more specific programming courses.

**My goals in this course are to focus on a number of underlying concepts, in every project and unit of material, every lecture and section:**

- **Understanding code and what code** ***does,*** **building mental models of code.**
  - The course is primarily in Python, but the ideas we’re focusing on are not just about Python.
  - Why would someone else write code this way? Why would you? What does it do? How could you change it? How would you explain it? How could you put it to use?
- **Debugging code, fixing code, getting used to matching code you write to your goals for its functionality.**
  - This comes from understanding.
  - How can you write code that does what you want it to do? How can you fix code that does not do what you want it to do? What if you didn’t write it?
  - How can you go from ideas to a finished or partially finished project? We’ll focus on documentation and testing, comments and understanding, along with the code.
- **Refactoring and modularity, code structure, reading code, understanding the whys of writing code and reading code.**
  - Why is a project structured in the way it is?
  - Is there a better way to structure a project to fit the goals you have for it?
  - Can reformatting code structure-wise that performs the same functionality help you understand it better? For your code? for someone else’s code?
- **Experience pulling together old and new concepts to interact with the web, data, others’ systems.**
  - APIs
  - Authentication
  - Tools for collaboration — Git, and GitHub
  - Underlying Python concepts that can help you understand other programming languages
  - Installation
  - Writing good tests
  - Design patterns
  - Beginning to understand web programming — what do you need to understand about programming if you work at a tech company that makes a web app, or write tests for a company’s product, or design programs for a company or research lab or analysis, or build an application at a library, or happen to encounter someone’s web application code that sounds like you might want to use it for some goal you have…
- **Questions?**



# **OK, so where do we start?**


# Installation, Python 3 vs Python 2
- You may previously have used Python 2
- This course uses Python 3 (so does SI 506, as of this semester, for those who took it before)
- Fear not — the process of getting accustomed to a new language version is an experience most people who interact with programming will have

**If you don’t have Python 3 installed** (which is probably most people. If you have a Mac, the default Python is *not* Python 3, so you’ll still have to do this installation): follow instructions in the +Installing Git, Python3, and VirtualEnv document, in the Python 3 section.

After you’ve installed it, if you type `which python3` at the command prompt and see something kind of like this (with your computer name and your username, not m-c02sdaadg and jczetta), it’s right! Great!


![](https://www.dropbox.com/s/u597s2wwdw0eelv/Screenshot%202017-08-04%2021.39.56.png?dl=1)


[https://www.dropbox.com/s/u597s2wwdw0eelv/Screenshot%202017-08-04%2021.39.56.png?dl=0](https://www.dropbox.com/s/u597s2wwdw0eelv/Screenshot%202017-08-04%2021.39.56.png?dl=0)
**If you already have Python 3, great.**

- I*n order to make sure installations work the same for everyone, if you have e.g. Anaconda set up, that may work for many things in this course, but* ***you should make sure you have plain ‘ol Python 3 (>=3.4, I use 3.6) downloaded from Python.org***
- I am assuming you have already installed Python and run it via the command prompt on your computer. Please see an instructor at some point, office hrs or section, if this causes trouble. If you have no idea what this means, this might not be the course for you — consider 506/talk to an instructor!
- NOTE that in order to invoke a program with Python3 the way you’re likely accustomed to, after you install the Python.org Python 3, you’ll have to: `python3 newprograminpy3.py`, for example.
  - But you’re about to learn about another way to manage what version of Python gets run, too.


## **Text Editors / IDEs**
- Recommended: Atom, Sublime Text (both for all OS)
- OK to use: Any
- We’ll be doing a lot using the command prompt. When you use a text editor with a “run” option, it MAY be using a different path to get to the Python interpreter than your command prompt, and it may not behave in the way that you expect. Instructions will expect that you’re running via the command prompt (Terminal, Git Bash) but if you use a different method, you’ll probably need to rely on your Google skill (or there suddenly being a lot of free time at office hours. But don’t count on that!).
- Using an IDE (Interactive Development Environment) like PyCharm is definitely okay, and it also allows a lot more control over what version of Python you’re using. So that’s a plus! But if you don’t know how to use the IDE and aren’t comfortable getting used to new software (which is true of many of the best programmers I know), I would *not* worry about installing it now.


## **Python 3 vs Python 2**
1. **3 big differences you might notice right away,**
2. And a bunch of small differences, but most things are compatible. More detail here: https://docs.python.org/3/whatsnew/3.0.html
3.
4. `print` is a function, not a statement keyword
  1. so it must be called with parens! `print("hello")` or `print(len(``"``hello``"``))`, etc.
5. Many functions that you’re accustomed to returning a **list** type return a **iterator** type. We will discuss this in more detail in this course, a little later on. Here’s what YOU are most likely to notice:
  - **In Python 2:**
    diction = {"a":3,"b":5}
    print diction.keys() # prints ["a","b"] or ["b","a"] -- a list of the keys
  - **In Python 3:**
    diction = {"a":3,"b":5}
    print(diction.keys()) # prints: dict_keys(['a', 'b']) -- wait, what's this?
  **In BOTH, this code works just fine:**
    diction = {"a":3,"b":6}
    keys_again = diction.keys()
    for k in keys_again:
      print(k)

But what’s actually happening when the `.keys()` method is invoked is **just slightly different in Python 3** from what happens in Python 2.

The `.keys()` method returns an **iterator**, not a list. What’s the difference? Well,  for example,

    kys = diction.keys()
    print(type(kys))) # <class 'dict_keys'>

Wait, what?

That’s because the `kys` variable now holds an **iterator**. It’s a special iterator: A dict_keys kind! Save this for a week or two from now, and we’ll come back to specifics of what’s going on here (I promise).

It causes this to happen, though, too, so you don’t get too surprised:


    print(kys[0]) # hey, I wanna know what the 0th element of the list of keys from the dictionary is!

Gets you…

    TypeError: 'dict_keys' object does not support indexing

Oops. That’s because it’s an *iterator*! OK, let’s say I don’t care, I just want to do what I’m used to until this class actually learns about iterators, which is not *today*. But no need to get super frustrated before that happens. No big deal; solve your problem like this:


    diction = {"a":3,"b":5}
    kys = diction.keys()
    kys_list = list(kys) # You could also do this in one line if you really wanted to
    print(kys_list[0]) # prints either "a" or "b"

**kys_list** is what you’re used to from Python 2.

There’ll be more. First day is not for THAT much programming language theory.

**Questions?**


#
# Review: Unix / bash / shell / command prompt

https://www.programsinformationpeople.org/runestone/static/publicpy3/#unix


- `cd`
- `ls`
- `pwd`
- `cp`
- `mkdir`
- pipes: `|` and output redirection: `>` for ‘pipe to file’
- `grep` e.g. `ls | grep "pset``"` or `grep filename_here.txt hello` — what will those things do in various situations?

Running Python at the command prompt:
`python3 <filename> <any command line args>`

Bash is a programming language! Just not one we’ll go into depth in. It’s still useful to be conversant — it makes your life interacting with the computer much faster.

Check out the chapter linked above and try these out, remind yourself of how they work. Raise your hand if you have a question, and we’ll come around and help.


<break if we’re halfway through, otherwise we’ll push it forward>


# Virtual environments and project structure

(References: +Virtual Environments in Python (among readings for this week), +Installing Git, Python3, and VirtualEnv )

**Every Python project has…**

- At least one file, usually multiple (code, data, etc)
- Requirements (modules that must be installed for it to work properly)
- Usually, a purpose or a goal of some nature, some kind of result you can see or create

**Ideally,**

- Documentation
- Tests
- Maybe: output?

Requires… installations!
Different modules.

**What does it mean to install a Python module, or library? What IS a Python module?**

**Why might managing a bunch of different Python projects be difficult?**



Virtual Environments can help with that.

You have an additional reading about virtual environments that will give you detail; section will also help you practice. Right now, I just want us to look at a demonstration and answer some conceptual questions.


# Using a virtual environment (the basics)

**(More in your reading, practice in section)**

- Navigate to the project directory (wherever the virtualenv is saved)
- Activate the virtual environment
- Then see something like…

![](https://www.dropbox.com/s/g5kpdytj74fjl7t/Screenshot%202017-08-04%2022.47.16.png?dl=1)

  [https://www.dropbox.com/s/g5kpdytj74fjl7t/Screenshot%202017-08-04%2022.47.16.png?dl=0](https://www.dropbox.com/s/g5kpdytj74fjl7t/Screenshot%202017-08-04%2022.47.16.png?dl=0)

That name in parentheses is the name of the **currently activated virtual environment**. What does that mean?

With that going, any time you do `pip install` — that’s all you need, no sudo, no full path, because it’s just a virtualenv python, not your *global* Python
— it’ll get whatever from PyPi and then install it in the special Python interpreter, in this case a Python 3.6 one, that belongs to the **venv_test_name** virtual environment!

Type `deactivate` at the prompt and you go back to your normal prompt, no virtualenv activated, no access to the stuff you installed only in the virtual environment.

To activate any one, just follow the same steps with a different specific **virtualenv directory**. Ta-da.

And, of course, you could create another virtual environment for another project.

We’ll be using these in class. It’s always OK to pip3 install things globally, but it’s nice to separate these things out — not least because you can

`pip freeze` in a virtual environment and get all of the modules that are installed… JUST in that one.

**Why might you want to do that?**



# Version Control

For example, let’s say you’re writing a paper with two other people.

And then someone gets a great idea and decides to do some work on it, but they’re not totally sure everyone else will think it’s a good idea.

And then you decide you want to develop an argument in a particular way, but you’re not sure it will go with your collaborator’s new ideas…


- System to keep track of versions and changes
- Box, Drive, Dropbox do versioning
  - But fewer options than version control that programmers use
  
# What is Git? What is GitHub?

(You’ll be reading more about this this week.)

## What’s Git?

A Version Control System.  We’ll get to what that means.

Git can be installed on your computer. (Hopefully for most of you it already is! Straw poll…) If not, don’t worry yet. First, we want to get clear on what it *is*.

Git is a piece of software that basically acts as a layer on top of files in your computer, if you tell it to. It keeps track of *versions* of files and changes you make to them.


## What’s GitHub?

GitHub is a website that interacts with people’s own personal installations of the Git version control system (VCS). If you’re using Git on your computer, it’s a good idea to have a place that is NOT on your computer to save your work. That’s what GitHub can be: and it’s free! (It’s not the only such website, but it is one you will use in this course, and it’s also the most popular at the current moment.)


## Version Control

Keep track of your past! (e.g. Dropbox, Box)

But a programming VCS gives you a lot more freedom and control. We’ll look at examples this and next week, and later on.


## Installations You Need — Reference +Installing Git, Python3, and VirtualEnv

If you already have:

- Git Bash (for Windows)
- Mac, with all of the XCode Developer Tools installed (it would’ve been an installation you did because of programming that took a *very* long time)

You’re all set. Otherwise,


- Download Git Bash if you use Windows: https://git-for-windows.github.io/
- If you use Mac, download Git from this link (click on the Mac link to get it): https://git-scm.com/download

(See the announcement about installing these.)

****
##
****## **Now, try following along with these steps, thinking about what they mean (how** ***you*** **might translate them to English if it’s different from this)…**
## Git Version Control system
1. **“I’m going to start a project. I’m not sure what files and everything it’ll have in it, but I know I want to start a project.”**
  1. `$ mkdir new_directory` (Bash)
  2. `$ cd new_directory`  (Bash)
  3. `$ git init` *hey Git, start a repository in this directory — a git collection of sorts — (if Git is not installed correctly, this won’t work)*
    1. *lay a net over this directory so anything new in it will get caught and I can decide whether I want git to remember it*

2. **“I want to know what the STATUS of my project is.”**
  1. `$ git status`
  2. What do you see? Why?

3. **“I want to create a new file in my project.”**
  1. `$ touch first_file.py` (Bash — command to create a file)
  2. Open up the `first_file.py` in a text editor for editing
  3. Edit the file
  4. Save the file
  5. `$ git status`
  6. Now what do you see? Why?

4. **“I want git to keep track of my new file.”**
  1. `$ git add first_file.py` *git, go look at all the stuff that’s currently in first_file.py, keep track of it*
  2. `$ git status`
  3. Now what do you see? Why?

5. **“I want to save a snapshot of this moment in time on my project, so I can go back to it later, if I want to.”**
  1. `$ git commit -m "Adding first_file"`
    1. *hey Git, I want to save everything as it is right now that I’ve told you (Git) to look at!*
    2. *I’m noting that the situation at this moment can be described as “I’m adding the first file” so that’s what I’ve put in the descriptive message that I can look back on later…*
  2. `$ git status`
  3. What do you see now? Why?
    1. *****CLEAN WORKING DIRECTORY: THIS IS YOUR GOAL*****
  4. Why commit?
  5. Why the message? `-m "Adding first_file"`

6. **“I want to add more to my project. For now, I’ll just write more code in the first file I began before.”**
  1. Open `first_file.py` in text editor
  2. Edit the file with something
  3. Save the file
  4. `$ git status`
  5. What do you see now? Why?
    1. Why is it green?

7. **“I see that it says I’ve modified this file. What did I do again? I want to see how it’s different.”**
  1. `$ git diff HEAD` *hey Git, show me the difference between the project as it currently is and the last time I made a commit!*
  2. What do you see? Why?


8. **“Okay. I like those changes, that’s what I meant to do! Cool, I want Git to keep track of these changes so I can also come back to THIS point in my work if I want to.”**
  1. What should you do now? Why?
  2. *… <we’ll fill this in>*
  3. And repeat: ad nauseam! Let’s add another file…
  4. **NOTE: if you leave off the -m in the commit and “”, you’ll get to a weird screen.**
    1. ( ~ demo ~ of what’s going on in this situation; in-CLI text editors intro)
    2. To leave this screen and try again, `:q!`
    3. And we’ll talk more about how to deal with problems


## Back to the paper writing example…
- You start writing a paper.
- You have an idea. What if you totally changed your introduction, and made a slightly different argument? That’s a great plan. This paper is going to be even better now.
- But you don’t know. You can also see another way you can go from here. Maybe you want to come back to it and start over later…maybe this isn’t such a great idea… Maybe you won’t like the way my new idea goes.
- OK, here’s what you’ll do. You’ll save it as a new file: `history_paper_version_2.docx` and then if you want to come back, you can just reopen `history_paper_1.docx` and start working again on THAT one. It’ll be great.
- Wait! A third idea! That’s OK. You’ll just save it again as `history_paper_v3.docx` and then you can come back to the original idea. But wait, didn’t you have something in version 2 that was great that you want to keep? Or was it version one? Which file is it in?! What did you call the file again? Which one should you be working on?!
- …😔 😩
- …version control!
- Now, version control is a little complicated for things that aren’t:
  - Plain text files
  - Program files, like `.py` Python files
  - Plain data files, like `.csv` files

(Because of the things that are happening in the background for complex data files like .docx or .xlsx files, you can’t see the changes that well. You can still use git, but it’ll be a little more opaque.)
How to use it for papers nicely is something we can discuss later. But it’s the same idea, just one that people who don’t do a ton of programming have almost certainly run into before.

We’re gonna use it for programming. Many programmers do. Helpful for a bunch of reasons… this is the way projects evolve.

This isn’t all about Git and GitHub we’ll cover in this course (or in the first month), but initially, here are the *base* concepts you need in order to use Git and GitHub for your *own* purposes, version control for your *own* projects — and submission of your first HW assignment!

There are also ways to build on all of those parts of the process — dealing with more complex situations, which we’ll cover, but also making things easier for you to type/quicker/better suited to your process/etc.

# Always: **Commit early, and commit often.**

Why? That’s the power of Git version control.


## **So let’s review the process here.**
- `git init` to CREATE a git layer in your project (in a directory)


- `git add <filename>` to add a new file for git to keep track of


- `git commit -m "descriptive msg about what your changes are"`  to save that moment in time in your project, so you can always come back to it, and keep track of all the changes


- `git add <filename>`  again to add any additional changes you make in file(s)
  - and `git commit -m "descriptive message goes here"` again to commit the things you add: SAVE all those changes in git, instead of just makin’ git start taking serious notice of ‘em


- `git diff HEAD` to check out the difference between stuff you’ve just added, but not committed yet, and the last commit you made (the snapshot of the status of your project, How Things Are At This Moment)


- `git status` to check out what the *status* of the git repository is (the layer that’s keeping track of all these changes — does it know about anything new? has it noticed changes? is everything up to date?)
  - When you pause work, ideally, everything’s up to date! **Clean working directory.** Everything added/committed/deleted appropriately.
  - (There are some exceptions to this in certain cases, but they’re more complicated than we’re gonna look at now. This is the pattern to get down.)

This is like a *super useful layer* on top of your work. Can pay attention to the changes. When you tell it to, figures out exactly what the changes are, and when you tell it to, saves the state of things you’ve told it to save. Tracks all your changes as you go, as long as you tell it to. (Also, allows you to walk back in history and retrieve past states!)


## **BUT WAIT! This is all just on your computer! It’s not on the internet at all!! What?**

Huh. What? Why?

So you can go back in project history. So you can see your progress. Super cool and useful:

OK, we’ve made a few commits now. Saved a couple different stages of the project. Just on my computer. What can we do?
Here’s some stuff.


9. **“Hey, I want to see how many different moments in time in the project I’ve saved.”**
  1. `$ git log`
  2. What do you see?
  3. What does it mean?
  4. Why is it helpful?

10. **“Hey, I want to go back to the first version I had. I really liked that best.”**
  1. Are you sure? You’re going to rewrite history.
  2. (There are ways to avoid rewriting history, but we’re not going to go into the complexity *just yet*.)
  3. Are you really sure?
  4. Let’s check to be certain we’re sure.
    1. `$ git log`
    2. Hey, ok, what’s the commit where I said I had the initial version? This one!
          - (It’s represented by this long string of letters and numbers called a **sha1 hash**. Every one of these in one project is unique! They represent commits: snapshots, moments in project time.)
    3. *Let’s look at what’s different between now and then, the stuff I’m gonna get rid of if I go back to an old version.*
    4. `$ git diff <the commit hash here>`
    5. Hmm, looks like that’s what I added… yeah, I don’t like that. I want to go back to when I just had that very first bit. Definitely. I’m going to do this differently.
    6. `$ git reset --hard <the commit hash of that same very first commit here>`
        *(*`*--hard*` *means reset completely, but other options get into some more challenging complexities of git, so not yet. There ARE also ways to recover commits after reset —hard, but they’re kind of a pain & we’re not gonna talk about them today. If you’re curious, you can look up* `*git reflog*` *, which will make more sense soon)*

    7. `$ git status` — let’s check out the status of things, always a good idea
    8. `$ git log` — history now shows only the one commit version, because that’s what we came back to!

11. **“Hey, now I want to make some DIFFERENT changes to the file(s) and save a new version. I think I want to add a new file, too.”**
  1. So, what are we gonna do? What are your thoughts? Consider for a minute, talk w/ a neighbor.


It’s easy to get yourself into a bit of a mess with Git,  but it’s also possible to get yourself out of any mess with enough practice and calm. And it’s really useful to know the basics, because then you can collaborate with others using it. This is the first tool in the 507 collaboration toolkit.

I like the sticky net metaphor for GitHub because of that — what you want is always somewhere, saved in your history, even if you have to dive in to find it.

Any other metaphors you like? Please share on Piazza!


## **This was all just on our own computers. Now, GitHub!**
- Having this on your computer is useful, good.
- But, it’s nice to be able to put your project somewhere else.


1. **GitHub Account — yours**
  1. GitHub account holds *repositories* — like folders for projects
  2. You want one repository (or “repo”) per project
  3. The work I do for SI 364 is not explicitly related to the work I do for SI 507
  4. The work you do for Project 2 will not be explicitly related to the work you do for Project 3
2. Associate SSH keys so you can connect the stuff on your computer TO the stuff online — security!
  1. Take a look at the readings this week…
3. Create a new repository: *this is the place to save your project*
4. Let’s take a look at a GitHub repository: https://github.com/aerenchyma/madlib-generator
  1. Commits
  2. History
  3. Contributors
  4. How to look at this and understand it
5. Questions?


## **Connect a git repository to a GitHub repository**

(if time)


## **Nice thing about GitHub: collaborate with others**
- More about this next week, but for now…
- *Forking*!
  - “Her project is cool, I want to copy it… but do something a little different with it”
  - Press a “fork” button … this part is pretty OK once you know what to do.
- *Cloning!*
  - Now I want to work on this thing that I have in my GitHub account, on my own computer
  - `git clone` + the git URL of the project in YOUR account
    - For example…

Repository for another interactive textbook, somewhat similar to (but different from) the one we’re referencing/that you used if you took SI 506: https://github.com/RunestoneInteractive/thinkcspy

  - Fork it
  - Clone it
  - Make a change
  - Commit that change *to your copy*
# Section this week

You’ll be practicing:

- forking and cloning repositories
- creating virtual environments
- using `pip` and requirements files

Will be even easier if you get to the Virtual Environments reading before your section, but OK if you don’t — treat it as an experiment with these new concepts (new even if you’re pretty proficient with Python)

We’ll be getting back to Python soon.


# Next week

More git
Testing, testing, testing

Don’t forget about your readings!




----------

**Additional Notes**


    # IMP: Remember to activate your virtualenv. Make it a habit!
    # Once activated, you can use python and pip, instead of python3 and pip3

    # see installed packages
    # usually installed in your venv/lib/python3.6/site-packages
    pip freeze

    # save installed packages in requirements.txt
    pip freeze > requirements.txt

    # install packages from requirements.txt into your current environment
    pip install -r requirements.txt


> The sign # (aka octothorp, hash, pound, number sign) is used to start a comment in shell & gitignore files, just like in python


Anything you put in `.gitignore` is ignored / not tracked by `git`


    # .gitignore example file
    venv_test_project/ # ignore this folder and its sub-folders
    __pycache__/ # ignore this folder and its sub-folders
    *.pyc # ignore any file with extension .pyc
    somefile.py # ignore this specific file


> Preceding gitignore with a dot (.) makes it a hidden file. It is a convention followed by git. To see hidden files and folders, run `ls -al`
