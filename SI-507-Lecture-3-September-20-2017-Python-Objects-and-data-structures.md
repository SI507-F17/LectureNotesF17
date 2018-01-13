# SI 507 | Lecture 3 | September 20, 2017 | Python Objects and data structures

# Admin

A few administrative announcements… this time, in more detail.


## This course

Is a different structure than other programming courses you may have taken at UMSI in the past, focused heavily on preparing you to *learn more about programming*, even more than teaching very specific skills.

Programming can only be learned with a *lot* of practice and stretching mental boundaries, new ‘mental muscles’ you may not even have known you had.

So for every assignment in this class, in order to get the most out of the lecture session, there are a few things I strongly recommend:

- Take a look at the projects as soon as you can after they are released
- Reminder: syllabus allowances & your own priorities
- How to do readings  



# Some examination of testing and side-effect tests
- Taking a look at Project 1
- And how you can use it moving forward

# Objects in Python, Review

Everything in Python is an object.

A string. A list. Objects!

There are methods you can call on each. There are special things about all of them.

You can also define your own classes, as you read about. You saw class `Point`. You saw class `Pet`. You’ve seen other classes — `Photo`, `Song`…


## Why define a class?
- You want to write a text-based interactive game where animals interact — it’s easier to create an “animal” type than it is to write a bunch of complicated code referring to this idea of an “animal”
- What other reasons?
- If you have a bunch of methods but you want a programmer / user not to have to be concerned with method implementation
- For stuff you use all the time
- You want to make a bunch of instances but you don’t want to write a lot of code
- You can pass nested data into a class and get instances/one instance (depending) where the data is easily organized
- Data that’s the same categories for every e.g. animal, but has different values for each “animal”
- Organizing your code


# Defining a class in Python
## What is a user-defined class?
- A factory
- An outline
- Produces instances that all have the same attributes -- little pieces of data or methods (special functions) that can be invoked, but whose attributes may have different data values
## What to think about when you think about defining a class?
- What the class represents overall (general outline)
- What one instance of that class represents overall (same idea, different data values)
- What data each instance has
- What each instance can *do* in your program
- What syntax to use
    class ClassNameInCaps(object):
        def __init__(self, ... ): # constructor -- invoked when an instance is created
            pass # stuff here

        def othermethodname(self):
            pass #stuff here
- What does **self** mean? Why is it always there?
- How do you invoke a method on an instance of the class?
- How do you access attributes (instance variables) of each instance?

My class will be called _____. (Should be a singular noun!)
One instance of this class will represent one _______.
Each instance of this class will have instance variables that represent _____, ______, ______.
Each instance of this class will have methods that can do things: _____, _____, _____.

## An example (class `Student`)
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
        self.class_limit = self.class_limit + 1 # creating an instance variable from a class variable -- how does this look up work?


    new_student = Student("Jackie","UMSI")  
    print(new_student.class_limit)
    print(new_student.name) # Jackie
    new_student.take_class("SI 507")

**NOTE: this code is now in a file on Canvas > Lecture Files > Lecture 3 >** `**student.py**`

- How many instance variables could there be, max, in an instance of Student?
- What is the input to the constructor?
- How many class methods are there?
- How many class variables are there?
- How many of the class methods return a value? How many do not?

Class variables link: https://www.programsinformationpeople.org/runestone/static/publicpy3/Classes/ClassVariablesInstanceVariables.html

## The constructor
  `__init__` — most important part of the factory, always called when an instance created (“instantiated”)
## Instance variables
- Attributes that belong to that particular instance
## Class variables
- Attributes that belong to the class — and, by definition, every instance that comes from that class “factory”
## Class methods
- Attribute functions (methods) that can be run ON any instance of a class
- Belong to the *class* not the instance
- But get run on the instance


## Special methods: `__str__`, `__repr__`, `__contains__` …

**String method and Representation method (in general)**
`__repr__` goal is to be unambiguous, clear re: data, often — obviously unique per instance
`__str__` goal is to be readable


    inst_var_rep.__repr__()
    str(inst_var_rep)


`__contains__` — what does it mean for something to be *in* an instance of `Student`?
If it means, “is this string one of the strings in the `classes` list, you have to define that

- takes one input, always (additional to `self`)
- defines what it means for something to be “in” it with the `in` operator, various examples:
  - e.g. `"``he``"` `in` `"``hello``"` eval to `True`
  - `"``hi``"` `in` `"``hello``"` eval to `False`
  - `"``hi``"` `in [``"``hello``"``,``"``goodbye``"``,``"``wow``"``,``"``hihihi``"``]` eval to `False`
  - `"``hi``"` `in [``"``hi``"``,``"``hello``"``]` eval to `True`
  - `3 in {3:``"``quarters``"``, 5:``"``nickels``"``}` eval to `True`
  -

__contains__ method could be used for allowing code like this:

    if "SI 507" in new_student:
      print("This student is taking 507!")

Let’s add a `__contains__` method to our `Student` class definition…


## Class instances, creating instances of a class
- One *particular* house
- One *particular* card
- One *particular* Deck
# Making decisions about defining a class

Looking at the `Card` and `Deck` classes from your HW1 for an example…

What might be a thought process for designing this? How would you use it? How would you write more functions to play games — e.g one like this: https://www.pagat.com/invented/slap.html

Try some code that would do something fun with cards and decks in a function, using the code — creating instances and invoking methods on them. A good goal — write code that does the following:

- Shuffle a deck
- Deal 2 hands of 8 cards each
- Play one card at a time from each hand
- If the cards are the same suit OR the same rank/number, add a point to a score tally

How can you write code to do that, looking at the code you have?

You can use your Project 1 code or download the `cards.py` file again from the Project 1 files folder on Canvas. You could write this code inside `cards.py` where the play game  functions are defined, or import the file into a file in the same directory, like so…





## A walk-through exercise:

Define a class that represents a photo, using data from Flickr.
Useful: https://www.programsinformationpeople.org/runestone/static/publicpy3/Classes/ClassesHoldingData.html
You can download sample data representing 1 photo from Flickr on Canvas: `Files > Code Samples > Lecture 3 > sample_diction.json`

Investigation of the nested data…

  - Review of how to do this? Straw poll.

“What data do you have to represent?” — always an important question when defining classes
What do you need to use the object instances for?

**A note on using data from APIs** — more on this can be found in the textbook material! If you took SI 506, you might want to look back at a couple of your problem sets. If you are a UMSI student and completed the SI 506 waiver, you might want to look at that (it’s a lot like this example here, and the information in the **Using REST APIs** chapter of the reference Python textbook).

(Walk through the thought process in English, almost always. Then start writing code.)

Try this yourself, either as review, refresher, etc. If you have ideas for making the






    import unittest

    class TestingDeck(unittest.TestCase):

# Introduction: class Inheritance

class `Student`
class `UMichStudent`
class `HighSchoolStudent`
class `GraduateStudent`

Let’s consider this “Python object family tree”, and then try a couple examples.

## From your reading…
- **Why would you define a class that inherits from another class? What are some reasons you can imagine to use class inheritance? (Hint: have you seen class inheritance before?)**


- **What are some different forms of inheritance you might see or use in your code?**
  - Overriding methods
  - Making additions to methods that exist in the parent
  - Removing some function from methods that exist in the parent
  - …what else?


- (If we don’t have time for this during lecture, this is a good set of things to review and ask questions about later on.)

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
          return "This vehicle moved forward {} miles.".format(miles_num)

    class Limousine(Vehicle):
      def __init__(self, brand="Porsche",color="black"):
          super(Limousine).__init__(self, brand, color)
          self.clean = True

      def forward_amount(self, miles_num):
          self.miles_moved += miles_num
          return "This limo moved forward {} miles.".format(miles_num)

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

    party_limo.forward_amount(20)
    party_limo.forward_amount(10)

    gala_limo.forward_amount(15)
    gala_limo.spill_drink()

    print(party_limo)
    print(gala_limo)

    if gala_limo.clean:
        print("The limo I took to this celebration is so lovely!")
    else:
        print("I should take this vehicle to a car wash or something.")

    # Will the following code work?
    car.spill_drink()  
    party_limo.spill_drink()
    car.forward_amount(32)
    print(car)
    print(party_limo)
    if party_limo.clean:
        print("Whoa, shiny!")
    else:
        print("Oops.")

    print("The car and party limo have together moved {} miles.".format(car.miles_moved + party_limo.miles_moved)


Try running that code yourself if you like! But first, try analyzing it.

You’ll notice that line 14 of the code, `print(party_limo)` includes that the `party_limo` instance has moved 30 miles.
And line 7 of the code, `print(gala_limo)` for the first time, includes that the `gala_limo` instance has moved 0 miles.
Why is that? I don’t see any `self.miles_moved` instance variable in the definition of the `Limousine` class…


Also,

- Why, when we defined the classes above, did we need to redefine the whole `forward_amount` method for the `Limousine` class? Why not just use the parent class’s method? What’s different?


- What’s going on in the constructor (`__init__`) method for the `Limousine` class? Try explaining that in English.


- Will the lines of code line 23 - 30 in the code above run properly? Which will? Why or why not? Which won’t run and should be commented out?


- What will line 34 of that code print (assuming all code that won’t run has been commented out)? How do you know?



# (if time) Exercise

class `GraduateStudent` inherits from `Student`, but there are a few differences:

- each instance of class GraduateStudent should have an instance variable class_limit that == 4
  - HINT: checking out the Tamagotchi code in the book and how the bored and hunger constants are used may be a good hint for how to do this…
- GraduateStudent should have the same input to the constructor as Student, but
  - an additional input — `degree_program`, which gets assigned to an instance variable `self.degree`. (e.g. “MSI”, “MHI”… or any string)
  - an additional instance variable that, for every GraduateStudent instance, begins as the empty list, called `self.internships`
- GraduateStudent should have an additional class method `do_internship`, which should take one additional input, and should append the input to the empty `self.internships` list.



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
        if len(self.classes) < self.class_limit
          self.classes.append(class_name)

      def add_to_limit(self):
        self.class_limit = self.class_limit + 1


The following code should definitely work once these definitions as specified exist:


    gs = GraduateStudent("Isabel","UMich","MSI")
    gs.take_class("SI 501")
    print(gs.classes) # should print: ['SI 501']
    print(len(gs.internships)) # should print: 0
    print(gs.degree) # should print: MSI
    gs.do_internship("UMich Library")
    print(gs.internships) # should print: ["UMich Library"]
    print(gs) # should print: A student named Isabel who goes to UMich
