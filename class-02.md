## CHAPTER 2: "Text" (p. 40-61)
<br />
## Headings 
- HTML has six "levels" of headings 
- H1 is used for main headings and H2 is used for subheadings 
## Paragraphs
- <p> A paragraph consist of one or more sentences that form a self-contained unit of discourse. The start of a paragraph is indicated by a new line.
- <p> Test is easier to udnerstand when it's slipt up into units of text. 
- by default, a browser will show each paragraph on a new line with some space between it and any subsequent paragraphs
## Bold & Italic 
- <b> BOLD </b> to make words bold
- <i> ITALIC </i> to make words italic - used to represent a section of text that would be said in a different way from surround content- technical terms, foreign words, etc
## Superscript & subscrip 
- <sup> element is used to contain characters that shoudl be superscript such as the suffixes of dates or mathematical concepts like raising a nubmer to a power such as 2<sup>2</sup>
- <sub> element is used to contian characters that should be subscripts such as chemical formulas H<sub>2</sub>0
## White Space 
- In order to make code easier to read, web dev often add extra spaces or start some elements on new line
- when the browswer comes across two or more spaces/line break next to each other, it only displays one space (white space collapsing)
- ## Line Breaks & Horizontal Rules
- <br /> adds a line break inside the middle of a paragraph
- <hr /> add horizontal line break between paragraphs or sections 
## Visual Editors & Their Code Views 
- Visual editors oftern resemble word procesors, although each editor will differ slightly, there are some featurese that are common to most editors 
- Code views show you the code created by the visual editor so you can manually edit it, or so you can just enter new code yourself
## Semantic Markup 
- text elements that are not intenderd to affect the structure of your web pages, but they do add extra information to the pages
-<em> element allows you to indicate where emphasis should be placed on selected words and the <blockquote> element which indicates that a block of text is a quotation (similar to italic)
## Strong & Emphasis 
- <strong>Beware:</strong> element indicates that its content has strong importance and browsers will show the content in bold 
- <em> indicates emphasis that subtly changes the meaning of a sentence 
- <blockquotes> element is used for loger quotes that take up an entire paragraph. Browsers tends to indent the contenct of the <blockquote> element, however you should not use this element just to inent a piece of text
- <q> element is used for shorter quotes that sit within a paragraph 
## Abbreviations & Acronyms 
- <abbr> element can be used for an abbreviation or an acronym 
- <abbr title="Professor">Prof</abbr> 
## Citations & Definitions 
- <cite> should be used when referencing a piece of work such as a book, film or research patper. In HTML5, <cite> should not be used for a person's name- but was allowed in HTML4, so most people are likely to continue to use it
- <dfn> element is used to indicate the defining instance of a new term <p> <dfn>black hole</den> is a region of space... 
## Author Details
- <address> element has quite a specific use: to contain contact dtails for the autheor of the page and can contain a physical address, email or phone number
## Changes to Content
- <ins>insert</ins> element can be used to show content that has been inserted into a document, while the <del>delete</del> element can show text that has been deleted from it
- <s> element indicates somethign that is no logner accurate or relevant (advertisement/price change) show a lines through the information 
## CHAPTER 10: "Introducing CS" (p. 226-245)
<br /
## Introducing CSS 
- CSS allows you to create rules that specify how the content of an element should appear (text and backgroud color)
- The key to understanding how CSS works is to imagine that there is an invisible box around every HTML element 
## Block & Inline elements 
- Block level elements look like they start on a new line. Examples include the <h1>-<h6>, <p> and <div> elements 
- Inline elements flow within the text and do not start on a new line. Examples include <b>, <i>, <img>, <em> and <span> 
- CSS allows you to create rules that control the way that each individual box (and content within that box) is presented
- Using CSS, you can add a border around anyt of teh boxes, specify its width and height, or add a backgroud colors. You could also control text insides a box- its colors, size, and tyeface used.
- CSS works by associating rules with HTML elements. These rules govern how the content of a specified elements should be displayed <bold>A CSS rule contains two parts: a selector adn a declaration</blod>
- p {font-family: Arial;} This rule indicates that all <p> elements should be shown in the Arial typeface
- Selectors indicate which element the rule applies to. The same rule can apply to more than one element if you separate the element anems with commas
- Declarations indicate how the elements referred to in the selector should be styled. Declarations are split into two parts (a property and a value), and are separated by a colon. 
## CSS Properties How Elements are Displayed
- CSS declarations sit inside curly brackets adn each is made up of two parts: a property adn a value, separated by a colon. h1, h2, h3 {font-family(property): Arial(value); color (property): yellow(value);}
- Properties indicate the aspects of the element you want to change- color, font, width, height, and border
- Value specify the settings you want to use for the chosen properties, which color, font, etc
## Using External CSS 
- <link> element can be used in an HTML document to tell the browswer where to find the CSS file used to style the page. Its an empty element and doesn't need a closing tag <link hreg="css/styles.css" type="text/css" rel="stylesheet" />
- href specifies the path to the CSS file (which is often placed in a folder called CSS or Styles)
- type attribute specifies the type of document beiing linked. The value should be text/css.
- rel specifies the relationship between the HTML page and teh file it is linked to. The value should be stylesheet when linking to a CSS file. 
- An HTML page can have more than one CSS style sheet. 
## Using Internal CSS
- You can use internal CSS by placing them inside a <style> element, which usually sits inside the <head> element of the page
- The <style> element should use the type attribute to indicate that the styles are specified in CSS. The value should be text/css
- When building a site with more than one page, you should always use an external CSS style sheet
## CSS Selectors
- there are many different types of CSS selectors that allow you to target rules to specific element in an HTML document
- CSS selectors are case sensitive, so they must match element names and attributes values exactly 
- Universal Selector - applies to all elements in the document *{}
- Type Selector - matches element names h1, h2, h3 {}
- Class Selector - matches an element whose class attribute has a value that matches the one specified after the period symbol .note{}
- ID Selector - matches an element whose id attribute has a value that matches the one specified after the pound or has symbol #introduction {}
- Child Selector - matches an element that is a direct child of another li>a {}
Descendant Selector - matches an element that is a descendant of another specified element (not just a direct child of that element) p a{}
- Adjacent Sibling Selector - matches an element that is the next sibling of another - h1+p {} tagets first <p> element after any <h1> element but none other 
- General Sibling Selector - matches an element that is a sibling of another, although it does not have to be the directly preceding element h1~p {} if you have two <p> elements that are siblings of an <h1> element 
## Inheritance 
- if you specify the font-family or color properties on the <body> element, they will apply to most child elements. This is because the value of the font-family property is inherited by child elements (does not work for backgroud-color or border properties)
## Why use External Style Sheets?
- All web pages can share the same style sheet by using the <link> element on each HTML page of your site to link to the same CSS document. This means that the same code does not need to be repeated = less code and smaller HTML page
- Page loads faster and it's easier to make changes to web page
- Single web pages can have CSS within the HTML file <head> of document, it's still not good practice 
<br /> 
## Duckett JS book Chapter 2: "Basic JS instructions" (p. 53-84)
## Basci JS Insctructions 
- Syntaxx and Grammer: like any new language, there are new words to learn and rules for how these can be put together 
## Statements 
- A script is a series of instructions that a computer can follow one-by-one. Each individual instruction or step is knonw as a statment. Statements should end with a SEMICOLON. 
- Javascript is case sensitive so hourNow means somethign different that HourNow or HOURNOW
- The semicolon also tells the JS interpreter when a step is over, indication that it should move to the next step. 
- Statements can be organized into code blocks - some statements are surrounded by curly braces; these are known as code blocks. The closing curly brace is not foloowed by a semicolon
- Code blocks will often be used to group together many nmore statments 
## Comments 
- you should write comments to explain what your code does. They help make your code easier to read and understand 
- Multi-line comments - to write a comment that strecthes over more than one line, you use a mult-line comment, starting with the /* characters and ending with the */
- Single-line comments is anything that follows the two froward slash characters // on that line will not be processed by the JS interpreter. Used for short descriptions of what the code is doing 
## What is a Variable?
- a script will have to temporarily store the bits of information it needs to do its job inside variables
- the data stored inside variables can change (or vary) each time a script runs 
- declaring a varibable: var (variable keyword) quantity (variable name/identifier); 
- Use camelCase is a variable name is more than one word  
- Once you create a variable, you can tell it what information you would like to store for you. Programmers say that you assign a value to the variable:  quantity (name) = (assignment operator) 3 (variable value);
- Variable name should describe the kind of data the variable holds 
- Until you have assigned a value to a variable, programmers say the value is undefined
## DATA Types 
- JS distinguishes between numbers, strings, and true or false values knowns as Booleans
- Numberic Data Type  handles numbers  0.75
- String Data Type consist of letters and other characters 'Hi, Tony!'
- Boolean Data Type can have one of two values; true of false 
- JS also has other data types such as arrays, objects, undefined and null 
## Shorthand for Creatting Variables
- programmers sometimes use shorthand to create var. There are 3 variations 
- 1. Variables are declared and values assigned in the same statement: var price = 5; 
- 2. Three vars are declared on the same line, then values assigned to each: var price, quantity, totat; price = 5; quantity = 14; total = price * quantitity 
- 3. Two vars are declared and assigned values on the same line. Then one is declared and assigned a value on the next line: var price = 5, quantity  = 14; var total = price * quantity 
## Changing the value of a Variable 
- once a variable has been created, you do not need to use the var keyword to assign it a new value. You just use the variable name, the equals sign (also known as the assignment operator), and the new value for that attribute 
## Rules for Naming Variables 
- 1. the name must begin with a letter, dollar sign($), or an underscore(_). It must not start with a number 
- 2. The name can contain letters, nubmes, dolalr sign, or an underscore. Note that you must not use a dash or a period in a var name 
- 3. You cannot use keyworkd or reserved words. Keyword are special words that tell the interpreter to do something. 
- 4. All variable are case sensitive, so score and Score would be different names, but it is bad practice to create two variables that have the same name using different cases
- 5. Use a name that describes the kind of information that the variable stores. (firstName) might be used to store a persons firt name 
- 6. If you variable name is made up of two or more words, use capital letter for the first letter of every word after the frist word
## Arrays 
- an array is a special type of variable. It doesn't just store one value; it stores a list of values 
- consider using an array whenever you are working with a list or a set of values that are related to each other 
- You create an array and give it a name just like you would any other variable (using the var keyword) var colors; color = ['white', 'black', 'custom']; 
- The values are assigned to the array inside a pair of square [], and each values is separated by a comma. 
- Values in an array do not need to be the same type, so you can store a string, number and a Boolean all in the same array 
- Values in an array are accessed as if they are in a numbered list. It is important to know that the numbering of this list starts at zero, these numbers are called an index 
## Expressions
- an expression evaluates into (results in) a signle value. Brodaly speaking there are two types of expressions 
- 1. Expressions that just assign a value to a variable: var color = 'beige'; 
- 2. Expressions that use two or more values to return a single value: var area = 3 * 2; The value of area is now 6. 
## Operators 
- expressions rely on things called operators; they allow programmers to create a single value from one or more values color = 'beige'; area = 3 * 2; greeting = 'Hi ' + 'Molly'; 
- Comparison Operators: buy = 3 > 5; the value of buy is false
- Logical Operators: buy (5 > 3) && (2 < 4); the value of buy is now true
## Arithmetic Operators 
- JS contains the following mathematical operators, which you can use with numbers. 
- addition +, subtraction -, division /, multiplication *, increment ++, decrement --, modulus %
- Order of Execution applies to arithmetic operations. Multiplication and division are performed before addition or subtraction 
## String Operator
- joining two or more strings together. Programmers call this string concatenation. var firstName = 'Ivy'; var lastName = 'Stone'; var fullName = firstName + lastName; 
<br />
## Chapter 4: "Decisions and Loops" (p. 145-162)
- Scripts often need to behave differently depending upoon how the user interacts with the web page and/or the brower windwo itself. 
- Evaluations- can analyze values in your scripts to determine whether or not they match expected results 
- Decisions- using the results of evaluations, you can decide which path your script should go down 
- Loops- there are also many occasions where you will want to perform the same set of steps repeatedly 
- Flowcharts can help to determine which lines of code should be run next 
- In the same way that there are operators to do basic math or add strings, there are comparison operators that allow you to compare values and test whether a condition is met or not. Examples include the greater than or less than symbols, and double (==) which checks wheter two values are the same 
- Evaluation of a condition is comparing two values using a comparision operator which returns a value of true or false 
// if (score > 50){
    document.write('You passed!'); 
} else {
    document.write('Try again...'); 
}
- Conditional Statements are based on a concept of if/then/else; if a condition is met, then your code executes one or more statements, else your code does something different (or just skips a step)
- == is equal to 'Hello' == 'Goodbye' returns false because they are not the same
- != is not equal to 'Hello' == 'Hello' return true 
- === strict equal to: this operator compares two values to check that both the data type and value are the same 
- !=== strict not equal to: this operator compares two values to check that both the data type and value are not the same  
- > great than: checks if the number on the left is greater than the number on the right 
- < less than: check if the number on the left is greater than the number on the right
- >= greater than or equal to 
- <= less than or equal to 
## Structuring Comparison Operatros 
- In any condition, there is usually one operator and two operands. The operands are placed on each side of the operator. They can be values or vairables. (score >= pass) 
- You can evalute two variables using the comparision operator to return a true or false value 
- The operand does not have to be a single value or variable name. An operand can be an expression (score1 + score2) > (highScore1 + highScore2)
## Logical Operators 
- allow you to compare the results of more than one comparison operator ((5 < 2) && (2 >= 3)) returns true 
- && logical and 
- ||  logical or 
- ! logical not 
## If Statements 
- the if statement evalutes (or checks) a condition. If the condition evaluates to true, any statement in the subsequest code block are executed
- If.. Esle statments check a condition. If it resolves to true the first code block is executed. If the condition resolvee to fales, the second code block is run instead 

