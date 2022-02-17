## Concepts of Functional Programming in JS
- FP is a programming paradigm- a style of building the structure and elements of computer programs- that treats computation as the evaluation of mathematical functions and avoids changing-state and mutable data.
## Pure Functions
- returns the same result if given the same arguments (deterministic).
- does not cause any observable side effects.
- if your function reads external files, it's not a pure function- the file contents can change.
- any function that relies on a random number generator cannot be pure.
- Pure functions are stable, consisten, and predictable.
## Pure Functions benefits
- code is easier to test.
- Given a parameter A => expect the function to return value B.
- let list = [1, 2, 3, 4, 5]; const incrementNumbers = (list) => list.map(number => number + 1);
## Immutability
- state cannot change after it's created.
- If you want to change an immutable obeject, you can't. Instead you create a new object with the new value.
- Use recursion, we keep our variable immutable.
## Referential transparency
- const square = (n) => n * n; this function will always have the same output, given the same input.
- a function consistently yields the same result for the same input, it is referentially transparent.
- pure functions + immutable data = referential transparency.
## Functions as first-class entities
- functions are also treated as values and used as data.
- can refer to it from constants and variables, pass it as a parameter to other functions, return it as result from other functions.
- the idea is to treat functions as values and pass functions like data- we can combine functions to create new functions with new behavior.
## Higher-order functions
- HOF akes one or more functions as arguments.
- HOF returns a function as its result
- Filter functions expects a true or false value to determine if the element should or should not be included in teh results collection.
## Map
- the map method transforms a collection by appying a function to all of its element and building a new collection from the returned values.
- transform a given array into a new array
## Reduce 
- reduce is to receive a function and a collection, and return a value created by combining the items.
- use map to transform the shppingCart into a collecttion of amount values, then just use the reduce function with sumAmount function.

## Refactoring JS for Performance and Readability
// Unrefactored code

const URLstore = [];

function makeShort(URL) {
  const rndName = Math.random().toString(36).substring(2);
  URLstore.push({[rndName]: URL});
  return rndName;
}

function getLong(shortURL) {
  for (let i = 0; i < URLstore.length; i++) {
    if (URLstore[i].hasOwnProperty(shortURL) !== false) {
      return URLstore[i][shortURL];
    }
  }
}

// Refactored code

const URLstore = new Map(); // Change this to a Map

function makeShort(URL) {
  const rndName = Math.random().toString(36).substring(2);
  // Place the short URL into the Map as the key with the long URL as the value
  URLstore.set(rndName, URL);
  return rndName;
}

function getLong(shortURL) {
  // Leave the function early to avoid an unnecessary else statement
  if (URLstore.has(shortURL) === false) {
    throw 'Not in URLstore!';
  }
  return URLstore.get(shortURL); // Get the long URL out of the Map
}
