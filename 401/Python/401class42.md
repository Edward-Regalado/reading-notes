# Dunder Methods

- special methods used to enrich your classes.
- start and end with double underscores __ini__ or __str__.
- pythonistas adopted the term "dunder methods" a short form of "double under".
- dunder methods let you emulate the behavior of built-in types.

## Object Representation: __str__,__repr__

- common practice in python to provide a string representation of your object for the consumer of your class.
1. __repr__: The "official" string representation of an object. 
2. __str__: the "informal" or nicely printable string representation of an object.
- if you're only going to use one string methods on a Python class, make sure it's __repr__.

## Iteration:__len__,__getitem__,__reversed__

- def __len__(self):
    return len(self._transactions)
- def __getitem__(self):
    return self._transactions[position]
- def __reversed__(self):
    return self[::-1]

## Operator Overloading for Comparing Accounts: __eq__,__lt__

- def __eq__(self, other):
    return self.balance == other.balance
- def __lt__(self, other):
    return self.balance < other.balance
- this allows you to compare class instances.

## Callable Python Objects:__call__

- you can make an object callable like a regular function by adding the __call__ dunder method.
- def __call__(self):
    print('start amount: {}'.format(self.amount))
    print('transactions: ')
    for x in self:
        print(x)
    print('\nBalance: {}'.format(self.balance))
- now you can call the instance of the class objecdt you just created. myObj().
- one downside of having a __call__ method on your objecs is that it can be hard to see what the purpose of calling the object is.


## Python Iterators

- objects that support the __iter__ and __next__ methods automatically work with for-in loops.
- just like decorators, iterators and their related techniques can appear arcane and complicated on first glance.

## A simple Iterator Class
 
- class Repeater:
    def __int__(self, value):
        self.value = value
    def __iter__(self):
        return self
    def __next__(self):
        return self.value
        
r = Repeater("hello")
for x in r:
    print(x)
- this will print "hello" in the console forever!
- iterators use exceptions to structure control flow, to signal the end of iterations, a Python iterator simply raises the built-in StopIteration exception.

- class BoundedRepeater:
    def __int__(self, value, max_repeats):
        self.value = value
        self.max_repeats = max_repeats
        self.count = 0
    def __iter__(self):
        return self
    def __next__(self:
        if self.count >= self.max_repeats:
            raise StopIteration
        self.count += 1
        return self.value
r = BoundedRepeater("hello", 3)
for x in r:
    print(x)
- this will print in the console 3 times.
- This gives us the desired result. Iteration stops after the number of reps defined in the max_repeats params:

## What are Python Generators?

- writing class-based iterators from scratch in Python requires writing quite a bit of code.
- Iterators allow you to write pretty for-in loops and help make your code more Pythonic and efficient
- Python Generators help with some sytactic sugar to amke writing iterators easier.
- def repeater(value):
    while True:
        yeild value
- Generators look like regular functions but instead of using the return statement, they use yield to pass data back to the caller.
- When yield is invoked, it also passes control back to the caller of the function- but it only does so temporarily.
- Whereas a return statement disposes of a function's local state, a yield statement suspends the function and retains its local state.
- re-implement the BoundedRepeater class as a generator function.
- def bounded_repeater(value, max_repeats):
    count = 0
    while True:
        if count >= max_repeats:
            return
        count += 1
        yield value
- def bounded_repeater(value, max_repeats):
    for i in range(max_repeats:
        yield value

## Python Generators - A Quick Summary

- Gen functions are syntatic  sugar for writing objects that supports the iterator protocol. Gens abstract away much of the boilplate code need when writing class-based iterators
- yield statements allow you to temporarily suspend execution of a gen funciton and to pass back values from it.
- Gens start raising StopIteration exceptions after control flow leaves the gen funciton by any means other than a yield statement.






