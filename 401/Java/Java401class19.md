# Purely Functional Programming

- In CS,. PFP usually designates a programming paradigm - a style of building the structure and elements of computer programs -- that treats all computation as the evaluation of mathematical functions.
- may also forbid state changes and mutable data.
- consist of ensuring that functions, inside the functional paradigm, will only depend on their arguments, regardless of any global or local state.

## Difference between pure and impure functional programming

- waters are still a bit murky
- a program is usually said to be functional when it uses some concepts of functional programming, such as first-class functions and high-order functions.
- first class function need not be purely functional -- may use techniques from the imperative paradigm, such as arrays or I/O methods that are not purely functional programs.

## Strict versus non-strict evaluation

- each evaluation strategy which ends on purely functional program returns the same result.
- ensures that the programmer does not have to consider in which order programs are evaluated, since eager evaluation will return the same result as lazy evaluation.
- still possible that that an eager evaluation may not terminate while the lazy evaluation of the same program halts.

## Parallel Computing

- Purely functional programming simplifies parallel computing since two purely functional parts of the evaluation never interact
 
## Data Structures

- purely functional DS are often represented in a different way than their imperative counterparts.
- array with constant-time access and update is a basic component of most imperative languages and many imperative DS, such as hash-table and binary heap, are based on arrays.
- arrays can be replaced by map or random access list, which admits purely functional implementation, but the access and update time is logarithmic.
- purely functional DS can be used in languages which are non-functional, but may not be the most efficient tool available.

## Sources

[Wikipedia](https://en.wikipedia.org/wiki/Purely_functional_programming)

