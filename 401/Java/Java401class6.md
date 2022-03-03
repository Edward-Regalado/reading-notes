# Inheritance and Interfaces


## Objects

- An object is a software bundle of related state and behavior.
- Software objects are of used to model real-world objects that you find in everyday life.
- All real-world objects share two characteristics: they all have state and behavior.
- Software objects store its state in fields (variable in some programming languages).
- Methods operate on an object’s internal state and serve as the primary mechanism for object-to-object communication.
- Data encapsulation: hiding internal state and requiring all interaction to be performed through an object’s method.- Benefit: Modularity, Information hiding, Code re-use, Plug-ability and debugging ease.

## Classes

- A class is a blueprint or prototype from which objects instances are created.
the main method in your application is responsible for creating new class instances.

## Inheritance

- provides a powerful and natural mechanism for organizing and structuring your software.
- classes inherit state and behavior from their super classes.
- use inheritance for closely related objects.
- use the extends keyword after your class name followed by the superclass’s name.

## Interface

- An interface is a contract between classes and the outside world.
- when a class implements an interface, it has to implement the behavior (methods) that live inside of the interface class.
- an interface is a group of related methods with empty bodies.
- use the implements keyword after your class name followed by the interface’s name.
- allows a class to become more formal about the behavior it promise to provide.
- enforced at build time by the compiler.
- methods must appear in source code before the class will successfully compile.

## Packages

- A package is namespace for organizing classes and interfaces in a logical manner.
- packages are similar to folders on your computer.
- makes large software projects much easier to manage.
- Java platform has an enormous class library (set a packages). This library is known as the “Application Programming Interface”, or “API”.
- Its packages represent the tasks most commonly associated with general-purpose programming.
- A File object allows a programmer to easily create, delete, inspect, compare or modify a file on the filesystem.
- packages allows a programmer to focus on the design of your project, rather than the infrastructure required to make it work.

## Interfaces and Inheritance

- Work in progress...

### Sources

[Object-Oriented Programming Concepts](https://docs.oracle.com/javase/tutorial/java/concepts/index.html)  
[Interfaces and Inheritance](https://docs.oracle.com/javase/tutorial/java/IandI/index.html)