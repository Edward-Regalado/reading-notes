### Javascript New Vocabulary 
* Javascript
* conditionals
* data types
* variable

### Creating a Basic Javascript
* JS is written in plain text, just like HTML and CSS, so you do not need any new tools to write a script.
* USE .js when creating a JS file
* Keep JS files organized by savin them in folders called scripts, javascript or js. 
### Link to a JS file from an HTML page
* when you want to use JS w/a web page, you use the HTML <script> element to tell the browser it is coming across a script. Its scr attributes tells people where the JS file is stored: <script src = " js/add-content.js"></script>

### Objects & Methods
* JS shows how to use objects and methods- programmers refeer to this as calling a method of an object
* document.write('good afternoon');  document is the object and .write('') is the method
* document object reps the entire webpage.. all browsers implement this object, and you can use it just by giving its name 
* Member operator (.) - the document object has serveral methods and properties known as members of that object.. call a **member operator** Access the members of an object using a dot between teh object name and the member you want to access
* The write () method of the document object allows new content to be written into the page where the <script> element sit.. 
* Parameteres- content inside parentheses. Each piece of information is called a parameter of the method.
* The browser uses a lot more code to make words appear on the screen... you only need to know how to call the object and method, and how to tell it the information it needs to do the job you want... 
* There are lots of objects like the **document** object and lots of methods like the **write()** methods that will help you write your own script

### JS run where it is found in the HTML
* when the browser comes across a //<script> element it stop to load the script and then checks if it needs to do anything
* the script element can be moved and it will affect where the <script> is diplayed on the screen... and it can also affect the load times
* Its best to keep JS code in its own JS file. 
* always make sure to you the script element for JS files and not (link) or any other element tags
* the JS will not chage the HTML when viewing the source code on a browser

### JS basic instructions: Statements
* learn the new syntax and grammar (just like any new language) 
* script is a series of insctructions that computers follow one-by-one and each step is known as a **statement** 
* statements end with a ; For example: var today = new Date(); var hourNow = today.getHours(); var greeting;
* the {} contains the code block and each code block can contain many, many statements
* JS is case sensitive so hourNow means something dif than HourNow and HOURNOW
* Each statement are instructions and each start on a new line (easier to read) and end with a ; 
* ; tells the interpreter when the step is over so it can move on to the next step 
* statements can be organized into code blocks aslo known as curly braces { } 
* Code blocks will often be used to group together many more statements (helps organize and read)

### Comments 
* write comments to explain what your code does.. helps make your code easier to read and understand for you and others
* /*This script displays a greeting to the user based upon the current time */
* var today = new Date();  // create a new date object
* var hourNow = today.getHours(); // find the current hour
* var greeting;
* //display the appropriate greeting based on the current time 
* if (hourNow > 18) {
*    greeting = 'Good evening';
* } else if (hourNow > 12) {
*   greeting = 'Good afternoon'; 
* } else if (hourNow > 0) {
*   greeting = 'Good morning'; 
* } else {
*   greeting = 'welcome'; 
* }
* document.write(greeting); 

* Mult-line comments stretch over more than one line use /*comments*/ and they will not be processed by the JS interpreter
* Single-line comments are often used for short descriptions of what the code if doing  //

### Variable
* Scripts will have to tempporary store bits of info it needs to do its job and can store data in **variabale**
* when writing JS, you have to be very specific with your instructions
* Data stored in variables does exactly that, changes (or vary) each time a script runs
* (var) is an example of what programmers call a keyword.. JS interpreter knows that this keyword is used to create a variable
* Variable name or indentifier is required when creating a new var (var quantity;)
* If variable name is more than one word, use camelCase
* Once you create a var, assing a value to it (quantity = 3;) or else its undefined

### DATA types 
* JS distinguishes between numbers, strings, and true or false values know as Booleans
* **Numeric data type** - for task that involve counting or calculating sums, you will use number 0-9. 
* numbers are also used for tasks such as the size of a screen, moving the positions of an element on page, or the amount of time an element should take to fade in
* **String Data type** - consist of letters and other characters 'Hi!' enclosed within a pair of '' or "" and can be used with any kind of text 
* **Boolean Data type** have two values: true or false. Helpful when determining which part of a script should run
* JS also has other (arrays, objects, undefined, and null) data types 

### Var to store a number
* var price; var quantity; var total; 
* price = 5; quantity = 14; total = price * quantity; 
### Var to store a string 
* var username; var message; 
* usermane = 'Molly' message = 'See our upcoming range'; 
* Use \"text here\" when using quotes within a 'string' or simply use the other quote variant (single vs double)

### Var to store a Boolean
* can only have a value of true or false (light an on/off switch)
* used when the value can only be T or F.. 1 or zero
* used when code can take more than one path 

### Shorthand for Var
* three var on the same line: var price, quantity, total; 
    * price = 5; 
    * quantity = 14; 
    * toatl = price * quantity
* two var declared on the same line 
    * var price = 5, quantity = 14; 
    * var total = price * quantity 
* will save time but might make your code harder to read

### Rules for Naming varibable
* name must begin with a letter, dollar sign, or an underscore. It must not start with a number
* must not use a dash (-) or period (.)
* cannot used keyword or reserved words such as VAR
* variable are case sensitive 
* Use a name that describes the kind of information that the var stores: var firstName; var lastName; var Age; 
* Use camelCase or underscore for every word after the first.. var lastName; var last_name; var 





### CSS 
* stand for Cascading Style Sheet
* It's a language used to give styling and desgin to webistes
* It is the standard for styling webites, used by most/all websites
* Usually goes hand-in-hand with HTML
* used for Styling, layout and design, animations, font changes,           organization and grid systems

### How computers work
* what makes a computer, a computer?
* computers are changing the world from pocket devices to desktop PCs
* Everyone uses it but most don't know how they work 
* Computers use circuits to do everything from simple math to VR worlds
* The 4 different parts of a Computer: CPU, Memory, Input and Output
* What exactly is Code and how does this software control Hardware?

### What makes a computer, a computer?
* how does it even work?
* Computers are tools that help us solve complex problems - it's a thinking machine
* it takes input, stores, process and outputs
* Early computers were made out of wood and metals with mech levers and gears
* Early PC were slow and very large
* PC started out as basic calculators 
* Input- the stuff that the outside world does that make computers do stuff- touch screen, mouse, cam, keyboard, watch. 
* Display- shows texts, games, VR, photos, videos and even signals to controls robots 

### How computers work - DATA & Binary 
* computers work on ones and zeroes on the insides
* wires and circuits carry all the information in a computer
* How do you store data/information with electricty?
* The binary number system- 0 and 1
* Any number can be respresented by 1 or 0
* More wires, more numbers 
* Text, images and sound are all represented with 1/0s in binary code
* Sound 32bit is better than 8bit audio... has more data points 


### Circuits and Logic 
* every input and output is information 
* computers modify multiple inputs 
* Simple ON/OFF circuits take an electrical signal and flips it
* Circuit with 2 bits is called an adder 0+0=00

### Memory, CPU, Input and Output
* Input devices converts physical inputs to binary information 
* Memory stores this information 
* Cpu processes this information 
* Outputs to screen display binary code into pixels, output devices can be lots of different things 

### Hardware and Software
* Hardware- circuits, wires, chips, speakers, plugs
* Software- is code/programs running on machine
* How does the software and hardware communicate?
* CPU - master chip that controls all the other parts of the computer
* CPU recieves simples commands that tells it which circuit to use to complete a job (add, store, output, etc)
* Binary code is the most basic form of software and it controls all hardware of computer
* Binary code is not used to create new programs
* All current coding languages are designed on top of the binary language
* OS - The master program that manages how software uses the hardware of a computer



