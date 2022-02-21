# A Guide to Java Loops

## Overview

- looping is a feature which facilitates the execution of a set of instructions util the controlling Boolean-expression evals to `false`

### For Loop

- A `for loop` is a control structure that allows us to repeat certain operations by incrementing an devaluating a loop counter.

### While Loop

- A `while loop` is Java's most fundamental loop statement. It repeats a statement or block of statements `while` its controlling boolean-expression is true.

### Do-While Loop

- A `do-while` loop works just like the while loop except for the fact that the first condition evaluation happens after the first iteration of the loop.

## Packages and Import

- Package = directory
- Java classes can be grouped together in packages.
- A package name is the same as the directory (folder) name which contains the .java files.
- You declare packages when you define your Java program, and you name the packages you want to use from other libraries in an `import` statement.

### Package declaration

- The first statement in a Java source file must be the package declaration.
- Example: import javax.swing.*; The (*) specifies that all classes from that package are available to your program.

### Common imports

- `import java.awt.*;` Common GUI elements.
- `import java.awt.event.*;` The most common GUI event listeners.
- `import javax.swing.*;` More common GUI elements. Note "javax".
- `import java.util.*;` Data structures (Collections), time, Scanner, etc. classes.
- `import java.io.*;` input-output classes.
- `import java.text.*;` formatting classes.
- `import java.util.regex.*;` regular expression classes.