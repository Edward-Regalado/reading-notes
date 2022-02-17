## ES6 Classes

https://replit.com/@TonyRegalado/ES6-Classes

## Defining Classes
- classes are template for creating objects. They encapsulate data with code to work on that data. 
- Classes in JS are built on prototypes, but also have some syntax and semantics that are not shared with ES5 class-like semantics.
- Classes are basically special functions.
- Class syntax has two components: class expressions and class declarations.

## Hoisting
- an important difference between function declarations and class declarations is that function declarations are hoisted. 
- You need to declare you class and then access it.

## Class Expressions 
- class expressoins is another way to define a class. 
- can be named or unnamed.
- the name given to the named class expression is local to the class's body.

## Class body and method def
- the body of a class is that part that's inside {} and is where you define class members, such as methods and constructors.
- the body of a class is executed in strict mode.
- the constructor method is a special method for creating and initializing an object created with a class. There can only be one special method with the name constructor.
- a constructor can use the super keyword to call the constructor of the super class.

## Static Methods and properties
- the static keyword define a static method or property for a class.
- static methods are often used to create utility functions for an app, whereas static properties are useful for caches, fixed-configuration, or any other data you don't need to be replicated across instances. 

## Sub classing with extends 
- the extends keyword is used in class declarations or expressions to create a class as a child of another class.
- if there's a constructor present in the subclass, it needs to first call super() before using "this".
- the super keyword is used to call corresponding methods of super class.
