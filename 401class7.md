# Python Scope & the LEGB Rule: Resolving Names in Your Code
- The concept of scope rules how variable and names are looked up in your code. It determines the visibility of a variable within the code.
- LEGB - stands for Local, Enclosing, Global and Built-in
- Scope of a name defines the area of a program in which you can unambiguously acces that name, such as vars, funcs, objects etc.
- Global scope: The names that you define in this scope are available to all your code.
- Local scope: names that you define are only available or visible to the code within the scope.

## Names and Scopes in Python
- Assignments: x = value
- Import operations: import module OR from module import name
- Function definitions: def my_func():
- Argument defs in the context of funcs: def my_func(arg1, arg2, arg3):
- Class definitions: class MyClass: ...

## Python Scope vs Namespace
- Python scopes are implemented as dictionaries that map names to objects. These dictionaries are commonly called namespaces and are concrete mechanisms that Python uses to store names. They're stored in a special attribute called .__dict__
- import sys sys.__dict__.keys() to return a list with all the names defined at the top level of the module.
- You can reference the name by using the dot notation  module.name or subscription operation module.__dict__['name']
- Whenever you use a name (var or func name), Python searches through different scope levels (or namespaces) to determine if that name exists or not.

## LEGB Rule for Python Scope
- Local (or function) scope: contains the names that you define inside the function. These names will only be visible for the code inside the function. Names are created in memory at function call, not a function definition.
- Enclosing (or nonlocal) scope: is a special scope that only exist for nested functions. If the local scope is an inner or nested function, then the enclosing scope is the scope of teh outer or enclosing function. The names in the enclosing scope are visible from the code of the innner and enclosing functions.
- Global (or module) scope: is the top-most scope in Python program, script, or module. Names are visible everywhere in your code.
- Built-in scope: is a special Python scope that's created or loaded whenever you run a script or open an interactive session. This scope contains names such as keywords, functions, exceptions and other attributes that are built into Python. Names in this Python scopes are also available from everywhere in your code.

## Functions: The local scope
- The local scope or function scope is a Python scope created at function calls. Every time you call a function, you're also creating a new local scope. By default, the params and names that you assign inside a function only exist inside that scope, and when the function returns, the local scope is destroyed and names are forgotten.
- The idea is to avoid name collisions in your programs by properly using the local Python scope. This also makes functions more self-contained and created maintainable program units.
- programs will be easier to debug, read and modify.

## Nested Functions: The Enclosing Scope
- Enclosing or nonlocal scope is observed when you nest functions inside other functions. 
- Names that you define in the enclosing Python scope are known as nonlocal names.
- When you call outer_func(), you’re also creating a local scope. The local scope of outer_func() is, at the same time, the enclosing scope of inner_func(). From inside inner_func(), this scope is neither the global scope nor the local scope. It’s a special scope that lies in between those two scopes and is known as the enclosing scope.


## Modules: The Global Scope
- From the moment you start a Python program, you're in the global scope. Internally, Python turns your program's main script into a module called __main__ to hold the main program's execution. 
- Module Scope and global scope are the same since global scope/names are tightly associated with modules files and top-level names in any Python module.
- Whenever you run a Python program, the interpreter exectuest the code in the module or script that serves as an entry point to your program. This module is loaded with the specail name, __main__. Fromt this point on, you can say that your main global scope is the scope of __main__.
- when you call dir() with no arguments, you get the list of names available in your main global scope.
- There's only one global Python scope per program execution and this scope remain in existence until the program terminates and all its names are forgotten.


## The Built-in Scope
- is a special Python scope that's implemented as a standard library module name builtins. All of Python's built-in objects live in this module. 
- len(dir(__builtins__)) = 152
- You don't need to import these builtin objects.
- you can use dot notation to access the names on the __builtin__ object: builtins.sum([1, 2, 3]), builtins.max([1, 2, 3]), builtins.sorted([4, 5, 2, 1])

