### New Vocabulary 
* script
* programmatic problem solving
* expression 
* operator
* function 

### Java Introduction 
* you can use Javascript to select any element, attribute, or text from an HTML page. For example:
    * select the text insdie all fo the <h1> elements on a page
    * select any elements that have a class attribute w/a value of note
    * find out hwat was entered into a text input whose id attributes has a value of email
* Javascript allows you to make web pages more interactive by accessing and modifiying the content and markup used in a web page
* You can use JS to add elements, attributes, and text to the page or remove them. For example:
    * add a paragraph of text after the first <h1> element
    * change the balue of class attributes to trigger new CSS rules for those elements
    * change the size or position of an <img> element 
* specify a set of steps for the browser to follow (like recipe) which allows it to access or change the content of a page. For example: 
    * a gallery script could check which image a user clicked on and display a larger version of that image
    * mortgage calculator could collect values from a form, perform a calculation, and display elements
    * animation could check the dimension of the browser window and move an image to the bottom of the viewable area (viewpoint)
* JS encompasses many of the traditional rules of programming- makes web pages feel more interactive and responsive
* React to Event- specify that a script should run when a specific event has occurred. For example: 
    * a button is pressed
    * link is clicked
    * cursor hovers over an element 
    * information is added to a form 
    * time has passed
    * webpage has finised loading

### The ABC of programming 
*  A- what is a script and how do i create one?
*  B- how do computers fit in with the world around them?
*  C- How do  i write a script for a web page?

### 1/a What is a script and how to create
* a series of instructions that a computer can follow to achieve a goal- similar to recipes, manuals or handbooks
* scripts are made up of instructions a computer can follow step-by-step
* browers may use differnt parts of the script depending on how th user interacts with the web page
* can run different sections of the code in response to the situation around them 
* to write a script, you need to first state your goal and then list the tasks that need to be completed in order to achieve it
* Define the goal- the task you want to achieve
* Design the script- split goal out into a series of tasks that are going to solve this puzzle
* Code each step- each step need to be written in a programming language that the computer understands
* helps to plan/design script before you start coding it 
* use correct vocab and syntax

### Expressions + Operators pg 74-79
* expression evalutates into (result in) a single value. Broadly speaking there are two types of expressions
* Expressions that just assign a value to a varialbe
    * in order for a variable (var) to be useful, it needs to be given a value
    * var color = 'blue'; 
    * when you first declare a variable using the var keyword, it is given a special value of undefined- this  will change when you assign a value to it

* Expression that use **2** or more values to return a signle value
    * you can perform operations on any number of indiviual values to detemine a single value
    * var area = 3 * 2;   The value area is now 6 
    *  

### Operators 
* expressions rely on things called operators; they allow programmers to create a single value from one or more values
    * assignment operators color = 'blue'  
    * artihmetic operators: area = 3 * 2; 
    * string operators(combine two strings): greeting = 'Hi' + 'Molly'; .. the value of greeating is now Hi Molly
    * comparison operators (compare two values and return true of false): buy = 3 >  5; 
    * Logical operators (combine expressions adn return T or F): buy = (5 > 3) && (2 < 4);
### Arithmetic Operators
* addition +, sub -, divison /, multiplication *, increment ++, decrement --, modulus % 
### STring Operator 
* there is just one operator: the + symbol. It's used to join the strings on either side of it
* Concatenation- joining two or more string together 
    * var firstName = 'Ivy '; var lastName = 'Stone '; var fullName = firstName + lastName;
* When '' are added around a number, it becomes a string. If you add numeric data to a string, it becomes a 

### Using String Operators JS                      
* var greeting = 'Howdy ';                          
* var name = 'Molly'; 
* var welcomeMessage = greeting + name + '!'; 

### Summary 
* scripts are made up of a series of statements- like a recipe 
* scripts contain very precise instructions
* Var are used to temp store pieces of information used in the script
* Arrays are speacial types of varibale that store more than one pieve of related information 
* JS distinguishes between number (0-9), strings(text),, and Boolean values (T or F)
* Expressions evaluate into a single value
* Expressions rely on operators to calculate a value


### Functions 88-94

### What is a Function?
* lets you group a series of statements together to perform a specific task... different parts of a script repeat the same task, you can reuse the function rather than repeating the same set of statements
* group together statements that are required to answer a question or perform a task helps organize your code
* statements within functions are not always executed when the page loads; functions store steps needed to achieve a task when required- like clicking on a button
* All functions need a name, so you can call the function when needed
* Some functions need to be provided w/information call parameters
* when you write a function and you expect it to provide you wiht an answer, its called return value

### Declaring a Function 
* to create a function, you give it a name and then write the statements need to achieve its task inside the curly braces. Declare function using the function keyword, give function a name/identifier, {code goes inside}
        * function sayHllow() {
            document.write('Hello!');
        }
* functions store the code required to perform a specific task

### Calling a Function 
* after delaring a function, you can execute all of the statements between its curly braces with just one line of code... this is **calling the function**

