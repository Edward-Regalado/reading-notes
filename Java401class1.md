# The Java Tutorials

## Variables

### Primitive Data Types

- Java is statically-type, which means that all variable must first be declared before they can be used. Declare the variable type and name `int myVar = 1;`
- Java supports 8 prmitive data type
- **byte**: `byte` data type is an 8-bit signed two's complement integer. Min value of -128 and max value of 127 (inclusive). Useful for saving memory in large `arrays`. Can also be used to help clearify your code; small variable range can serve as a form of documentaion.
- **short**: `short` data type is a 16-bit signed two's complement integer. Min value of -32,768 and max value of 32,767 (inclusive). Can be used to save memory in large  `arrays`.
- **int**: `int` data type is a 32-bit. Use the Integer class to use int data type as an unsigned integer.
- **long**: `long` data type is a 64-bit two's complement integer. Min value of -2^63 and max value of 2^63 -1. Use this data type when you need a range of values wider than those provided by `int`. The `Long` class contains methods like `compareUnsigned, divideUnsigned` to support arithmetic operations.
- **float**: `float` data type is a single-precision 32-bit 754 floating point. Use float instead of a `double` if you need to save memory in large `arrays` of floating point numbers. Should never be used for precise values like currency.
- **double**: `double` data type is a doulbe-precision 64-bit floating point. Generally the default choice for decimal values.
- **boolean**: `boolean` data type has only two possible values: `true` and `false`. Use this for simple flags that track true/false conditions.
- **char**: `char` data type is a single 16-bit Unicode character.

- Java also provides special support of string via the `String` class. Enclosing chars string within doulbe quotes will automatically create a new `String` object. String objects are immutable. String classes are not primitve data types.

### Default Values

- It's not always necessary to assign a value when a field is declared. Compiler will set to default(zero or zull) depending on data type.

### Literals

- primitive data types are speical data types built into Java; they're not objects created from a class. A literal si the source code representation of a fixed value. Literals are represented directly in your code without requiring computation.

#### Integer Literals

- An integer literal is a type `long` if it ends with the letter `L` or `l`; otherwise it is type `int`.
- Use uppercase letter L because its easier to read.

#### Floating-Point Literals

- floating-point literal is a type `float` if it ends with the letter `F` or `f`; otherwise its type is `double` and it can optionally end with the letter `D` or`d`.
- `floats` and `doubles` can also be expressed use `E` (scientific notation).

#### Character and String Literals

- Java supports special escape sequences for `char` and `String` literal: `\b` (backspace), `\t`(tab), `\n`(line feed), `\f`(form feed), `r`(carriage return), `\"`(double quote), `\'`(single quote), and `\\`(backslash).
- specail kind of class literal, used by taking the type name and appending ".class". `String.class`. Refers to the object (of type `Class`).

#### Uderscore Characters in Numeric Literals

- underscore character (_) can appear between digits in a numerical literal. Imporves readability of your code.
- Can place underscores only between digits and are not allow at: beggining or end of a number, adjacent to a decimal/float point, prior to an F or L suffix, in positions where a string of digits is expected.

## Arrays

- an `array` is a container object that holds a fixed number of values of a single type.
- lenght of `array` is established when the array is created and it's fixed.
- each item in `array` is called an element and each element has an index starting from 0.

### Declaring a Variable to Refer to an Array

- `int[] anArray;` declares an array of integers.
- an array declaration has two componenets: the array's type and name.
- `[]` a special symbols indicating that a variable holds an array.
- `byte[] anArrayOfBytes;` or `byte anArrayOfBytes[];` (can also place brackets at after array's name but convention disourages this form).

#### Creating, Initializing, and Accessing an Array

- create an array with the `new` operator.
- `anArray = new int[10]` create an array of ints with enough memory for 10 integers.
- `anArray[0] = 1`; initialize first element
- `anArray[1] = 2`; initialize second element
- use shortcut syntax to create and initialize an array: `int[] anArray = {1, 2, 3, 4, 5, 6};`
- length of array is determined by the element within the {} brackets.
- use two or more sets of brackets to declare a multidimensional array, `String[][] names`
- Use built-in `length` property to determine the size of any array. `Sytem.out.println(anArray.length);`

#### Copying Arrays

- `System` class has an `arraycopy` method that you can use to efficiently copy data from one array into another.
- `System.arraycopy(sourceArray, start pos, destArray, start pos, how many elemnts);`

#### Array Manipulations

- Java provides several methods for performing array manipulations (copying, sorting, searching) in the `java.util.Arrays` class.
- Some useful operation provide by methods in the `java.util.Arrays` class are:
- searchign an array for a specific value to get its index (`binarySearch` method)
- comparing two arrays to determine if they're equal or not(`equals` method)
- Filling an array to palce a specific value at each index (`fill` method)
- Sorting an array into ascending order (`sort` method) or using the `parallelSort` method.
- converting an array to a string using (`toString` method)

#### Summary of Variables

- Java used both "fields" and "variables" as part of its terminology.
- Instance variable (non-static fields) are unique to each instance of a class.
- Class variables (static fields) are fields declared with the `static` modifier; there is exactly one copy of a class variable, regardless of how many times the class has been instantiated. 
- Local variables store temporary state inside a method.
- Params are variables that provide extra information to a method; both local vars and params are always classified as "variables".
- Follow rules and conventions when naming variables.

### Operators

- operators are special symbols that perform specific operations on one, two or three operands, and then return a result.
- operators with high precedence are evaluated before operators with lower precedence.
- when operators have equal precedencd, a rule must govern which is evaluated first.
- all binary operators except for the asignment operators are evaluated from left to right; assignment operators are evaluated from right to left.

### Assignment, Arithmetic, and Unary Operators

#### Assignment Operator

- one of the most common operators is the assignment operator "=". `int speed = 120;`
- can be used on objects to assign object references.

#### Arithmetic Operators

# Work in Progress