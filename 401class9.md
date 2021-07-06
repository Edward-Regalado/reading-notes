# Dunder Magic Methods
- Dunder Methods are special methods that are predeined which you can use to enrich your classes.
- They start and end with doulbe underscores, for example __init__ or __str__.
- Pythonistas adopted the term "dunder methods", a short form of "double under."
- Dunder methods let you emulate the behavior of built-in types like len("string"), empty class definitions don't support this behavior out of the box.

# Special Methods and the Python Data Model
- Python data model lets devs tap into rich features like sequenes, iteration, operator overloading, attribute access, etc.
- Python's data model is like a powerful API that you can interface with by implementing one or more dunder methods.

# Enriching a Simple Account Class

## Object Initialization: 
- to construct account objects from the account class you need a constructor which in Python is the __init__ dunder.
- The constructor takes care of setting up the object.
- class Account:
    """A simple account class"""

    def __init__(self, owner, amount=0):
        """
        This is the constructor that lets us create
        objects from this class
        """
        self.owner = owner
        self.amount = amount
        self._transactions = []
- create new accounts like this:
acc = Account('bob')  # default amount = 0
acc = Account('bob', 10)

## Object Representation: __str__, __repr__
- __repr__: the "official" string rep of an object. This is how you would ake an object of teh class. The goal of __repr__ is to be unambiguous.
- __str__: the "informal" or nicely printable string rep of an object. This is the enduser.
class Account:

    def __repr__(self):
        return 'Account({!r}, {!r})'.format(self.owner, self.amount)

    def __str__(self):
        return 'Account of {} with starting amount: {}'.format(
            self.owner, self.amount)

## Basic Statistics in Python -- Probability
- What is probability? seeks to answer the question, "what is teh chance of an event happening?. An event is some outcome of interest. 
- by looking at the events that can occur, probabiity gies us a framework for maing predictions about how often events will happen.
- use stats to calculate probabilities based on observations from the real world and check how it compares to the ideal.

## From stats to probability
fimport random
def coin_trial():
heads = 0
for i in range(100):
    if random.random() <= 0.5:
        heads +=1
    return heads
def simulate(n):
    trials = []
    for i in range(n):
        trials.append(coin_trial())
    return(sum(trials)/n)
simulate(10)
>>> 5.4
simulate(100)
>>> 4.83
simulate(1000)
>>> 5.055
simulate(1000000)
>>> 4.999781

