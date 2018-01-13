# SI 507 | Lecture 4 | September 27, 2017 | Class inheritance, object design

# Admin

- New office hours announcement

# Review from last week
- Defining classes (user-defined types)
- Instance variables and class variables
- Class methods
- Instance of a class
- Defining a class using data, and brief data investigation review
  - Which you practiced in section this past week

# Making decisions about defining a class

Looking at the `Card` and `Deck` classes from your HW1 for an example…

What might be a thought process for designing this? How would you use it? How would you write more functions to play games — e.g one like this: https://www.pagat.com/invented/slap.html

Try some code that would do something fun with cards and decks in a function, using the code — creating instances and invoking methods on them. A good goal — write code that does the following:

- Shuffle a deck
- Deal 2 hands of 8 cards each
- Play one card at a time from each hand
- If the cards are the same suit OR the same rank/number, add a point to a score tally

How can you write code to do that, looking at the code you have?

(Worth spending time here: what does this code really do? Does it make sense? What questions do you have about it? Are there changes you could make that you might want to make and if so, why? What code will allow you to write code that does the things listed above?)

You can use your Project 1 code or download the `cards.py` file again from the Project 1 files folder on Canvas. You could write this code inside `cards.py` where the play game  functions are defined, or import the file into a file in the same directory…

Code…



# Introduction: class Inheritance

class `Student`
class `UMichStudent`
class `HighSchoolStudent`
class `GraduateStudent`

Let’s consider this “Python object family tree”, and then try a couple examples.

## From your reading…
- **Why would you define a class that inherits from another class? What are some reasons you can imagine to use class inheritance? (Hint: have you seen class inheritance before?)**
  - Employee - different types (salary, rank, title)
  - UI components
  - Memberships, subscription services — more expensive memberships, etc get all the basics, plus extras
  - Inheritance from unittest


- **What are some different forms of inheritance you might see or use in your code?**
  - Overriding methods
  - Making additions to methods that exist in the parent
  - Removing some functionality from methods that exist in the parent (overriding a method)
  - …what else?


Say you have the following code, which uses class inheritance.


    class Vehicle(object):
      def __init__(self, brand, color):
          self.brand = brand
          self.color = color
          self.miles_moved = 0

      def __str__(self):
          return "A {} vehicle, color {}, which has moved {} miles.".format(self.brand, self.color, self.miles_moved)

      def forward_amount(self, miles_num):
          self.miles_moved += miles_num
          #return "This vehicle moved forward {} miles.".format(miles_num)
    # class LuxuryTransport

    class Limousine(Vehicle):
      def __init__(self, brand="Porsche",color="black",rental_co="Happy Limos"):
          #super(Limousine,self).__init__(brand, color)
          #super(Limousine).__init__(self, brand, color)
          super().__init__(brand,color) # even better!
          self.clean = True
          self.rental_co = rental_co
          self.excited_brand = brand + "!!!!!!!!"

      def forward_amount(self, miles_num):
          return super().forward_amount() # this returns a string I don't care about
          #self.miles_moved += miles_num
          #return "This limo moved forward {} miles.".format(miles_num)

      def spill_drink(self):
          self.clean = False

      def clean_up(self):
          self.clean = True



# Exercise

Here’s some code that uses those class definitions above, includes instances of those classes, and some questions — try to answer them, predict the answers, run the code, figure out what’s going on, see if there’s anything you find confusing you’d like to clarify.


    car = Vehicle("Ford","red")
    gala_limo = Limousine()
    party_limo = Limousine(color="silver")

    # What will the following code print?
    print(car)
    print(gala_limo)



    gala_limo.forward_amount(15)
    gala_limo.spill_drink()

    print(party_limo)
    print(gala_limo)

    if gala_limo.clean:
        print("The limo I took to this celebration is so lovely!")
    else:
        print("I should take this vehicle to a car wash or something.")

    # Will the following code work?
    #car.spill_drink()  
    party_limo.spill_drink()
    car.forward_amount(32)
    print(car)
    print(party_limo)
    if party_limo.clean:
        print("Whoa, shiny!")
    else:
        print("Oops.")


    print("The car and party limo have together moved {} miles.".format(car.miles_moved + party_limo.miles_moved)


Before you try running that code, try figuring out what it will do, making predictions, i**n order to answer the following questions:**

You’ll notice that line 14 of the code, `print(party_limo)` includes that the `party_limo` instance has moved 30 miles.  And line 7 of the code, `print(gala_limo)` for the first time, includes that the `gala_limo` instance has moved 0 miles.


- Why is that? I don’t see any `self.miles_moved` instance variable in the definition of the `Limousine` class…

Also,

- Why, when we defined the classes above, did we need to redefine the whole `forward_amount` method for the `Limousine` class? Why not just use the parent class’s method? What’s different?


- What’s going on in the constructor (`__init__`) method for the `Limousine` class? Try explaining that in English.


- Will the lines of code line 23 - 30 in the code above run properly? Which will? Why or why not? Which won’t run and should be commented out?


- What will line 34 of that code print (assuming all code that won’t run has been commented out)? How do you know?


- What will print when lines 18-21 are done executing?


- What will print when lines 27-32 are done executing?


- What will print when line 34 is executed?
# Exercise

Define the class `GraduateStudent`, as follows:

class `GraduateStudent` inherits from `Student`, but there are a few differences:


- each instance of class GraduateStudent should have an instance variable class_limit that == 4
  - **HINT:** checking out the Tamagotchi code in the book and how the bored and hunger constants are used may be a good hint for how to do this…

- `GraduateStudent` should have the same input to the constructor as Student, but
  - an additional input — `degree_program`, which gets assigned to an instance variable `self.degree`. (e.g. “MSI”, “MHI”… or any string)
  - an additional instance variable that, for every GraduateStudent instance, begins as the empty list, called `self.internships`

- `GraduateStudent` should have an additional class method `do_internship`, which should take one additional input, and should append the input to the empty `self.internships` list.

Copying the Student definition here so it’s easier to see:

    class Student(object):
      class_limit = 4
      def __init__(self, name, school_name):
        self.name = name
        self.school_name = school_name
        self.classes = []

      def __str__(self):
        return "A student named {} who goes to {}".format(self.name,self.school_name)

      def take_class(self, class_name):
        if len(self.classes) < self.class_limit:
          self.classes.append(class_name)

      def add_to_limit(self):
        self.class_limit = self.class_limit + 1


**The following code should definitely work once these definitions as specified exist:**


    gs = GraduateStudent("Isabel","UMich","MSI")
    gs.take_class("SI 501")
    print(gs.classes) # should print: ['SI 501']
    print(len(gs.internships)) # should print: 0
    print(gs.degree) # should print: MSI
    gs.do_internship("UMich Library")
    print(gs.internships) # should print: ["UMich Library"]
    print(gs) # should print: A student named Isabel who goes to UMich


# Using class inheritance to make design decisions

Want to define a class `HighSchoolStudent`, and include an instance variable `self.extracurriculars`.

But then!


# (if time) More on Git & GitHub


- fetch
- pull
- merge & resolving conflicts (more on this later)


## Review

**Which involve GitHub only? which involve Git only? which (could) involve both?**

fork - GitHub
clone - involves both — GitHub → your computer
push - involves both — your computer → GitHub
commit - Git
add - Git
init - Git
remote add - involves both — building a connection between Git and GitHub
status - Git
log - Git
reset - Git (dangerous!)

**Analogies…**


## **One possible situation**

e.g. you create a git repo on your computer,
and you create a GitHub repository in your GitHub account,
and you add that GitHub repository as the remote location for your git repo (build the `origin` bridge…),
and in the *GitHub repo* you use the *GUI on the website* to create a new file! but you don’t do anything on your own computer,
and then you build the `remote add` bridge between this git repo and this github repo.

OK.

You want to push your files, committed in a git repo, to the GitHub location.

But you get an error:

![](https://www.dropbox.com/s/hymb07sp3fb5fgy/Screenshot%202017-09-26%2018.31.08.png?raw=1)


[https://www.dropbox.com/s/hymb07sp3fb5fgy/Screenshot%202017-09-26%2018.31.08.png?dl=0](https://www.dropbox.com/s/hymb07sp3fb5fgy/Screenshot%202017-09-26%2018.31.08.png?dl=0)


What to do? What does that mean?

“There’s some stuff in that remote location that you don’t have! I can’t push to that, it might not be right! Is this really the remote location for this repository??”

Here’s what you can do:


1. `git pull`
  1. *“Hey, git, pull down everything from across the bridge in the online remote onto my computer’s attached copy, and make sure any differences between the two are reconciled as best you can”*
2. Maybe everything’s fine! Then you have everything from online on your copy, and you can make changes, add, commit, and push, to maintain the equilibrium.
  1. If you have a clone of a repository on your computer, ideally, if there are *new* changes that *you* made, you want them on your computer first, and THEN on GitHub.
  2. Otherwise you have to make sure the GitHub version and the your-computer version are at that equilibrium before you can back up more changes on GitHub.
3. Occasionally you encounter a **merge conflict**.
  1. `git pull` is secretly doing 2 things:
    1. `git fetch` (get all the stuff from online that I have attached to this git repo with metaphorical bridges — there are other ways of doing so you haven’t learned yet — and pull it onto the computer, to sit around till I decide what to do with it)
    2. `git merge` (try to combine the version of the repository online you referred to, the GitHub repository, with the version of the files you have on the computer)
4. So, **example of resolving a merge conflict…**
  1. Here are some notes on it and other possible git problems, as one reference (not your only reference, but potentially useful): https://docs.google.com/document/d/1LcdVse69CKcwEgA4lrqg_Gr6YqpcqmmH81DgodR1BHU/edit?usp=sharing
  2. Live example… (if time)

We’ll look at this even more later on in the course. However, even with what you know now, you almost have the power to help yourself out of a lot of git troubles. It’s pretty much always fixable — you just have to be careful about what you are doing so you know how to retrace your steps.

Any commit you make in a repo can be retrieved, as long as you do not do a `reset` (which changes history. You can’t get back history that never happened!)
