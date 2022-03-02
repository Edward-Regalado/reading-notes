# Obejct-Oriented Programming Concepts

## Objects

- an object is a software bundle of related state or behavior.
- often used to model the real-world objects that you find in everyday life.
- all objects have state and behavior. Dogs state (name, color, bread, hungry) and behavior (barking, running, fetching).
- Fields (state) and Methods (behavior).
- Objects stores its state in fields (variables in some programming languages) and exposes its behavior through methods.
- Methods operate on an object's internal state and serve as the primary mechanism for object-to-object communication.
- Data encapsulation: requires all interaction from an object via its methods.
- An object's method(s) control how outside world is allowed to use it.
- Benefits: Modularity, Information-hiding, Code re-use, Pluggability and debugging ease.


## Classes

- A blueprint prototype from which objects are created.
- Bicycles are instances of the class of object known as Bicycles.
- cadence, speed and gear represent the object's state, and the methods (changeCadence, changeGear, speedUp) define its interaction with the outside world.
- `Bicycle` class does not contain a `main` method because it's not a complete application; just a blueprint for creating bicyles that might be used in an application. Creating the new `Bicycle` objects belongs some other class in your application.
- Classes contains fields, constructor and methods.

class Bicycle {

    int cadence = 0;
    int speed = 0;
    int gear = 1;

    void changeCadence(int newValue) {
         cadence = newValue;
    }

    void changeGear(int newValue) {
         gear = newValue;
    }

    void speedUp(int increment) {
         speed = speed + increment;   
    }

    void applyBrakes(int decrement) {
         speed = speed - decrement;
    }

    void printStates() {
         System.out.println("cadence:" +
             cadence + " speed:" + 
             speed + " gear:" + gear);
    }
}

- Demo below shows the main function creating instances on the Bicycle class:

class BicycleDemo {
    public static void main(String[] args) {

        // Create two different 
        // Bicycle objects
        Bicycle bike1 = new Bicycle();
        Bicycle bike2 = new Bicycle();

        // Invoke methods on 
        // those objects
        bike1.changeCadence(50);
        bike1.speedUp(10);
        bike1.changeGear(2);
        bike1.printStates();

        bike2.changeCadence(50);
        bike2.speedUp(10);
        bike2.changeGear(2);
        bike2.changeCadence(40);
        bike2.speedUp(10);
        bike2.changeGear(3);
        bike2.printStates();
    }
}

## Inheritance

- provides a powerful and natural mechanism for organizing and structuring your software.
- Different objects often share certain characteristics.
- Much like different types of bike
- OOP allows classes to inherit commonly used state and behavior from other classes.
- Each class in Java is allowed to have one direct superclass, while superclasses can have unlimited numbers of subclasses.
- Bicyle(Superclass): Mountain Bike(sub-class), Road Bike(sub-class), Tandem Bike(sub-class)
- syntax for creating a subclass: use the `extends` keyword followed by the class to inherit from.
- know the superclass state and behavior when accessing with a subclass.

class MountainBike extends Bicycle {

    // can access all of Bicycle methods and fields
    // create new fields and methods for a mountain bike that make it unique

}

## Interface

- an interface is a group of related methods with empty bodies.
- Methods form the object's interface with the outside world.
- Buttons on a calculator or TV remote form the interface.
- Implementing an interface allow a class to become more formal about the behavior it promies.
- Interfaces form a contract between the class and outside world, and this gets enfored at build time by compiler.
- all methods defined by an interface must be in source code before the class will successfully compile.

interface Bicycle {

    //  wheel revolutions per minute
    void changeCadence(int newValue);

    void changeGear(int newValue);

    void speedUp(int increment);

    void applyBrakes(int decrement);
}

## Package

- a namespace for organizing classes and interfaces in a logical manner.
- placing code into packages makes large software projects easier to manage (think folders on your computer).
- Java provides an enormous class library (set of packages) for use in your applications called "Application Programming Interface" or "API".
- packages represent tasks most commonly used in general-purpose programming.
- `File` object allows a dev to easily create, delete, inspect, compare or modify the filesystem.
- `String` object contains state and behavior for character strings.
- allows the programmer to focus on the design of your application, rather than having to build the infrastructure to make it work.

## Review

- Real-world objects contain **state** and **behavior**.
- A software object's state is stored in **fields**.
- A software object's behavior is exposed through **methods**.
- Hiding internal data from the outside world, and accessing it only through publicly exposed methods is known as data **encapsulation**.
- A blueprint for a software object is called a **class**.
- Common behavior can be defined in a **superclass** and **inherited** into a **subclass** using the **extends** keyword.
- A collection of methods with no implementation is called an **interface**.
- A namespace that organizes classes and interfaces by functionality is called a **package**.
The term API stands for **Application Programming Interface**.


## Declaring Classes

- The class body {everything between the curly braces} contains all the code that provides life to all instances created from the classs.
- **Constructors** for initializing new objects.
- **Declarations** for the fields that provide state of the class and its objects
- **Methods** to implement behavior of that class and its objects.

- class MyClass {
    //field, constructor and method declartions
}

### class declarations include:

- public and private modifiers determine what other classes can access your class.
- the class name with first letter capitalized.
- name of parent superclass (if needed) followed by `extends` keyword.
- comma-separated list of interface implemented by the class.
- class body {}.

## Declaring Member Variables

- Member variables in a class (fields).
- variables in a method or code block (local variables).
- variables in method declorations (parameters).

## Variable names

- first letter of a class name capitalized
- first word in a method name should be a verb.

## Defining Methods

- only required elements of a method declaration are return type, name, () and {}.
- void data type is method doesn't return anything.
- Method overloading: methods within a class can have the same name if they have different parameter lists- method parameters create the method signature. Use sparingly (makes code harder to read).

## Providing Construtors for you Classes

- constructors are invoke to create object from the class blueprint.
- use the same name of the class and have no return type.
- classes can have more than one constructor (no-arg constructor) as Java differntiates constructors based on teh number of arguments in the list and their types.

## Passing Information to a Method or a Constructor

Work-in-progress
