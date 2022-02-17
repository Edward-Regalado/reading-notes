# ES6 Syntax and Feature Overview

### Legend

- Varibale: `x`
- Object: `obj`
- Array: `arr`
- Function: `func`
- Parameter, method: `a, b, c`
- String: `str`

### Variable declaration

- ES6 introduced the `let` keyword, which allows for block-scoped variables which cannot be hoisted or redeclared.
- ES5: `var x = 0`
- ES6: `let x = 0`

### Constant declaration

- `const` keyword, which cannot be redeclared or reassigned, but it is not immutable
- constants are uppercase by convention
- `cont CONST_IDENTIFIER = 0`

### Arrow functions

- arrow functions expression syntax is a shorter way of creating a function expression.
- does not have their own `this` or prototypes
- cannot be used for constructors
- should not be used as objecvt methods
- ES5: `function func(a, b, c) {}` // function declaratoin `var func = function (a, b, c) {}` // function expression
- ES6: `let func = (a) => {}` // parentheses optional with one parameter `let func = (a, b, c) => {}`// requied with mult params

### Template literals

- expressions can be embedded in template literal strings
- ES5: `var str = 'Release date: ' + date`
- ES6: `let str = `Release Date: ${date}` // use backticks and curly for temp literals

### Multi-line strings

- Using temp literal syntax, JS string can span multiple lines without the need for concatenation
- let str = `This text is on multipel lines`

### Implicit returns

- the `return` keyword is implied and can be omitted if using arrow functions without a block body.
- ES5: `function func(a, b, c) {`
            `return a + b + c}`
- ES6: `let func = (a, b, c) => a + b + c` // curly brackets must be omitted

### Key/property shorthand

- ES6 introduces a shorter notation for assigning properties to variables of the same name.
- ES5: `var obj = {a: a, b: b}`
- ES6: `let obj = {a, b}`

### Method definition shorthand

- The `function` keyword can be omitted when assigning methods on an object
- ES5: var obj = {
    a: function (c, d) {},
    b: function (e, f) {},
}
- ES6: let obj = {
    a(c, d) {},
    b(e, f) {},
}

### Destructuring (objecdt matching)

- use curly brackets to assign properties of an objectd to their own variable.
- `var obj = {a: 1, b: 2, c: 3}`
- ES5: var a = obj.a
       var b = obj.b
       var c = obj.c
- ES6: `let {a, b, c} = obj`

### Array iteration (looping)

- A more concise syntax has been introduced for iteration through arrays and other iterable objects.
- `var arr = ['a', 'b', 'c']`
- ES5: `for(var i = 0; i < arr.length; i++) {`
    `console.log(arr[i])}`
- ES6: `for (let i of arr) {`
    `console.log(i)}`

### Default parameters 

- functions can be initialized with default parameters, which will be used only if an argument is not invoked through the function.
- ES5: `var func = function (a, b) {
    b = b == undefined ? 2 : b
    return a + b
}
- ES6: let func = (a, b = 2) => {
    return a + b
}
- func(10) // return 12
- func(10, 5) // return 15

### Spread syntax

- Spread syntax can be used to expend an array.
- `let arr1 = [1, 2, 3]`
- `let arr2 = ['a', 'b', 'c']`
- `let arr3 = [...arr1, ...arr2]`
Spead syntax can be used for function arguments
- `let arr1 = [1, 2, 3]`
- `let func = (a, b, c) => a + b + c`

### Classes/constructors functions


- `class` syntax on top of the prototype-based constructor function.
- ES5:
- function Func(a, b) {
    this.a = a
    this.b = b
}

Func.prototype.getSum = function () {
    return this.a + this.b
}

var x = new Func(3, 4)

- ES6: class Func {
    constructor(a, b) {
        this.a = a
        this.b =b
    }
    getSum() {
        return this.a + this.b
    }
}
let x = new Func(3, 4)
