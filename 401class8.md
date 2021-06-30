## List Comprehensions
- List compreshension always returns a result list.
- new_list = []
for i in old list:
    if filter(i):
        new_list.append(expressions(i))
new_list = [expression(i) for i in old_list if filter(i)]
- The list comprehension start with a [], square brackets.
- new_list: The new list (result)
- expression(i): Expression is based on the variable used for each element in the old list.
- for i in old_list: The word for followed by the variable name to use, followed by the work in the old list.
- if filter(i): Apply a filter with an if-statement.

## Create a simple list
- This is how you create a simple list: x = [i for i in range(10)]
print x [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
- squares = [] 
for x in range(10)
    squares.append(x**2)
    print squares
    [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
- Or you can use list compreshensions to get the same result: squares = [x**2 for x in range(10)]

## Multiplying parts of a list
- list = [3, 4, 5]
multipled = [item*3 for item in list]
print multiplied [9, 12, 15]
- Note how the item*3 multiplied each piece by 3

## First letter of each word
- listOfWords = ["this", "is", "a", "list", "of", "words"]
items = [word[0] for word in listOfWords]
print items

## Lower/Upper case 
- [x.lower() for x in ["A", "B", "C"]] [x.upper() for x in ["a", "b", "c"]]

## Print number only from string
- string = "Hellow 12345 World"
numbers = [x for x in string if x.isdigit()] (or x.isalpha for letters)
print numbers ['1', '2', '3', '4', '5']

## Using list comprehension in functions
- def double(x):
    return x*2
print double(10) 20
- [double(x) for x in range(10)]
print double [0, 2, 4, 6, 7, 10, 12, 14, 16, 18]
- you can put in conditions: [double(x) for x in range(10) if x%2==0] 
    prints [0, 4, 8, 12, 16]

## Primer on Python Decorators
- Functions returns a value based on the given arguments. 
- def add_one(number):
    return number + 1
add-one(2)
3
- In functional programming, you work (almost) only with pure functions without side effects.

## First-class Objects
- In Python, functions are fist-class objects, which means functions can be passed around and used as arguments, just like any other object (string, int, float, list, etc).
- def say_hello(name):
    return f"Hello {name}"

- def be_awesome(name):
    return f"Yo {name}, together we are the awesomest!"

- def greet_bob(greeter_func):
    return greeter_func("Bob")

## Inner Functions 
- It's possible to define functions inside other functions, also known as inner functions
- def parent():
    print("Printing from the parent() function")

    def first_child():
        print("Printing from the first_child() function")

    def second_child():
        print("Printing from the second_child() function")

    second_child()
    first_child()
- The order in which the innner functions are defined does not matter and the innner functions are not defined until the parent function is called. They are locally scoped to parent(): they only exist inside the parent() function as local variables. You'll get an error if you try to call the child functions of parent. 

## Simple Decorators
- def my_decorator(func):
    def wrapper():
        print("Something is happening before the function is called.")
        func()
        print("Something is happening after the function is called.")
    return wrapper

def say_whee():
    print("Whee!")

say_whee = my_decorator(say_whee)
- When you call say_whee(), it gets passed through the my_decorator(func): and gets executed inside the wrapper(): The name say_whee now points to the wrapper() function. 
- Decorator wrap a function, modifying its behavior.