# Classes and Objects
- Objects are an encapsulation of variables and functions into a single entity. Objects get their varaibles and functions from classes.
- A very basic class would look something like this:
    class MyClass:
        variable = "blah"
        def function(self)
            print("message")
- How to assign a class to an object: myobjectx = MyClass()
- You can use dot notation to accesst the variable inside the class. print(myobjectx.variable) would display "blah"
- You can create multiple different objects that are of the same class with the same variables and functions defined. However, each object contains independent copies of the variables defined in the class.
- myobjectx = MyClass(), myobjecty = MyClass(), myobjecty.variable = "yackity"
- To access a funciton inside of an object you use dot notation. myobjectx.function().

# Thinking Recursively in Python
- Thinking recursively is essentially breaking down problems into smaller and smaller chunks.
- An iterative algorithm:
 houses = [1, 2, 3, 4, 5]
 def deliver_presents_iteratively():
    for house in houses:
        print("delivering presents to", house)
- The algorithm for recursive present delivery:
houses = ["Eric's house", "Kenny's house", "Kyle's house", "Stan's house"]
    # Each function call represents an elf doing his work 
def deliver_presents_recursively(houses):
    # Worker elf doing his work
    if len(houses) == 1:
        house = houses[0]
        print("Delivering presents to", house)

    # Manager elf doing his work
    else:
        mid = len(houses) // 2
        first_half = houses[:mid]
        second_half = houses[mid:]

        # Divides his work among two elves
        deliver_presents_recursively(first_half)
        deliver_presents_recursively(second_half)
## Recursive Functions in Python
- a recursive function is a function defined in terms of itself via self-referential expressions. This means that the function will continue to call itself and repeat its behavior until some condition is met to return a result.
-All recursive functions are made up of two parts: base case and recursive case.
## Maintaining State
- since all recursive functions has its own execution context, you hve to make sure to maintain state during the processs.
- Thread the state through each recursive call so that the current state is part of the current call's execution context
- Keep the state in global scope.
def sum_recursive(current_number, accumulated_sum):
    # Base case
    # Return the final state
    if current_number == 11:
        return accumulated_sum

    # Recursive case
    # Thread the state through the recursive call
    else:
        return sum_recursive(current_number + 1, accumulated_sum + current_number)
- Global scope:
## Global mutable state
current_number = 1
accumulated_sum = 0


def sum_recursive():
    global current_number
    global accumulated_sum
    # Base case
    if current_number == 11:
        return accumulated_sum
    # Recursive case
    else:
        accumulated_sum = accumulated_sum + current_number
        current_number = current_number + 1
        return sum_recursive()

## Recursive Data Structures in Python
- data structure is recursive if it can be defined in terms of a smaller version of itself. A list is an example of a recursive data structure.

## Navie Recursion is Naive
- Recursive function to cpmpute the nth Fibonacci number:
def fibonacci_recursive(n):
    print("Calculating F", "(", n, ")", sep="", end=", ")

    # Base case
    if n == 0:
        return 0
    elif n == 1:
        return 1

    # Recursive case
    else:
        return fibonacci_recursive(n-1) + fibonacci_recursive(n-2)
- Improved recursive Fibonacci function by caching the results of each Fibonacci computation.
- lru_cache is a decorator that caches the results, thus, we avoid recomputation by explicitly checking for the value before trying to compute it.
from functools import lru_cache

@lru_cache(maxsize=None)
def fibonacci_recursive(n):
    print("Calculating F", "(", n, ")", sep="", end=", ")

    # Base case
    if n == 0:
        return 0
    elif n == 1:
        return 1

    # Recursive case
    else:
        return fibonacci_recursive(n-1) + fibonacci_recursive(n-2)
## Python Testing with pytest: Fixtures and Coverage
- Fixtures: when writing test, you're most likely goign to be writing an entire "test suite", with each test aiming to check a different path through your code.
- You'll want to have some objects availalbe to all of your tests> Those objects might contain data you want to share across tests, or they might involve the network or filesytem.These are known as "fixtures."
- You define fixtures using a combination of the pytest.fixutre decorator, along with a function def.

## Coverage 
- There are ways in which a function could give a totally different result that the test didn't check. As software gets larger and more complex, it's not going to be so easy to eyeball it. That is where you want to have "code coverage", checking that your tests have run all of the code.
- 100% doesn't mean your code if perfect or that it lacks bugs.

