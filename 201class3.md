# Duckett HTML Book

## Chapter 3: List (p. 62-73)
## Ordered Lists 
- ordered list is created with the <ol> element 
- each item in the list is placed between an opening and closing <li>
- browsers indent list by default

## Unordered List
- unordered list is created with the <ul> element 
- each item in the list is placed between an opening and closing <li> element 
- broswers indent by default
- bullet pionts such as circles, squares, diamonds and so on

# Definition Lists 
- def list is created with <dl> element and usually consit of a series of terms and their definitions
- inside the <dl> element you will usually see a pair of <dt> and <dd> elements
- <dt> is used to contain the term being defined
- <dd> is used to contain the definition 

## Nested Lists 

- you can put a second list inside the <li> element to created a sub-list or nested list
- browsers display nested lists indented further than the parent list


## Chapter 13: Boxes (p. 300-329)
- by default a box is sized just big enough to hold its contents
- to set your own dimensions, used the height and width properties
- most popular ways to specify the size of a box are to use pixels, percentages or ems
- pixels are the most popular bc they allows designers to accurately control their size
- percentages are based on the size of the broswer window or the box encased within another box
- ems are based on the size of the text within it

## Limiting Width 
- min-width property specifies the smallest size a box can be displayed at when the browser window is narrow
- max-width indicats the max width when the browser is wide
- helps make sure the content of the pages are legible (text doesn't become too wide or narrow)

## Limiting Height
- min-hegiht and max-height work similar
- when contents of box take up more space than the box
- overflow property tells the browser what to do if the content within box is later than the box
- overflow: hidden; hides any extra content p.one {
  overflow: hidden:}
- overflow: scroll adds a scrollbar to the box so that user can scroll to see the missing content  p.two {
  overflow: scroll;}
- overflow is handy because some browsers allow users to adjust the size of the text to appear as large or small as they want 

## Border, Margin & Padding 

- the border separates the edge of one box from another 
- margin sits on the outside edge of the border 
- padding is the space between the border of box and content contained within it

## White Space & Vertical Margin 

- Space between items on a page is known as white space
- makes text easier to read 
- add space between various items on a page 

## Border Width 

- used to control the width of a border and value of this property can either be given in pixels or using (thin, med, thick)
- you cannot use percentages
- you can control the individual size of borders using border-top-width, border-right-width, etc
- border-width : 2px, 1px, etc

## Border Style and Color 
- solid, dotted, dashes, double, groove, ridge, inset, outset, hidden/none
- border-top-color, border-right color: blue; etc
- values appear in clockwise: top, right, bottom, left (trbl)
- Shorthad9 border allows you to specify the width, style and colors of a border in one property a9d values should be coded in that specific order 
p {
  width: 290px;
  border: 9px dotted color:}

## Padding9

- padding 9llows you to specify how much space should appear between teh content of an element an9 its border
- usually 9pecified in pixels but can use ems or %
- Pecentag9 is % of browser window or box its contained 

## Margin 

- margin property controls the gap between boxes
- value is commonly given in pixels, can use ems or % too
- if boxes sit on top of another, margins are collasped, which mean larger of the two margins will be used and the smaller will be disregarded
- value of the margin property is not inherited by child elements in the same way that the color value of the font-family so you need to specify the margin for every element

## Centering Content 

- use left-margin or right-margin to center a box on the page (or center it inside the element that it sits in)
- need to set width for the box or else it will take up the full width of page
- text-align property is inherited by child elements 

## Change Inline/Block
- display property allows you to turn an inline element into a block-level element or vise versa
- inline causes a block-level element to act like an inline element 
- block causes an inline-block to act like a block-level element 
- inline-block causes a block-level element to flow like an inline element 
- none hides an element from the page 
- inline means they will sit next to each other rather than appearing on new lines

 ## Hiding Boxes Visibility  
- allows you to hide boxes from users but it leaves a space where the element would have been  
- visibility: hidden; shows the element but its  a blank space  
- visibility: none; hides the element with no blank space
- this will appear in the source in the browser

## CSS3: Box Borders 
- the border-image property applies an image to the border of any box
- takes a backgroud image and cuts it into 9 pieces
- box must have a border width for image to be shown
- box shadow property allows you to add a drop shadow around a box
- border-radius: 2px; creates rounded corners

# Duckett JS Book 

## Chapter 2: Basic JS Instructions (p. 70-73)

## Arrays 
- an array is a special type of variable. It doesn't just store one value, it stores a list of values
- consider using an array whenever you are working with a list or a set of values that are related to each other
- create an array and give it a name just like any other variable 
- var colors;
- colors = ['white', 'black', 'blue'];
- values inside an array using [ ] and each value separated by a , 
- values inside do not need to be the same data type
- technique for creating an array is known as an array literal 
## Values in Arrays
- each item in an array is automatically given a number called an index [0, 1, 2, etc]
- var itemThree; itemThree = colors[2]; 
- each array has a property called lenght, which holds the number of items in the array
- var numColors; numColors = colors.lenght; 

## Accessing & Changing Values in an Array 
- to access a value from an array, after the array name you specify the index number colors[2] = 'beige'; 
- you can change the value of an item in an array by selecting it and assigning it a new value just like any other variable 


## Chapter 4: Decisions and Loops from switch statements (p. 162-182)
- The if...else statement checks a condition
- If it resolves to ture the first code block is executed, if false the second code block is run instead 
- if (score >= pass){                               var pass = 50;
  msg = 'congratulations, you passed!';             var score = 75; 
} else {                                            var msg; 
  msg = 'Have another go!';  
}
## Switch Statments 
- starts with a variable called the switch value 
- each case inidcates a possible value for this variable and the code that should run if the variable matches that value
- you have a default option that is run if none of the cases match
- if a match is found, that code is run; then the break statment stops the rest of the switch statement from running 
- purpose of switch statments is to present the user with a differnt message depending on which level they are at
- var msg; var level = 2; 
- switch (level){
  case 1: msg = 'Good luck on the first test'; 
  break;
  defaul: 
  msg = 'Good luck!'; 
  break;  
}
## Type Coercion & Weak Typing
- JS can convert data types behind the screnes to complete an operation called type coercion
- JS is said to use weak typing becuase the data type for a value can change- other languages require that you specify what data type each variable will be (strong typing)
- === !== checks that the value and data types match 

## Truthy & Falsy Values 
- Falsy values are treated as if they are false or 0 
- Truthy values are treated as if they are true or 1 
- var highScore = false; var highScore = 0; var highScore = ''; var highScore = 10/'score'; var highScore; 


## Checking Equality & Existence 
- the presence of an object or array can be considered truthy, it is often used to check for the existence of an element within a page
- A unary operator returns a result with just one operand

## Short Circuit Values 
- logical operators are process left to right. They short-circuit (stop) as soon as they have a result- but they return the value that stopped the processing 

## Loops 
- For loops are used to run code a specific number of times and is the most common loop.In a For loop, the condition is usually a counter which is used to tell how many times the loop should run 
- While loop is used when you don't know how many times the code should run. The condition can be something other than a counter, and the code will continue to loop for as long as teh condition is true
- Do While loop is very similar to the while loop, but will always run statement inside the {} at least once, even if condition if false
- for (var i = 0; i < 10; i++){
  document.write(i); 
}
- Initialiazion - create a var and set it to 0, this var is commonly called i. var i = 0; 
- Condition - loop should continue to run until the couner reaches a specified number i <10;
- Update - every time the loop has run teh statements in the curly braces, it adds one to the counter 

## While Loops 
- this loop continues to run for as long as the condition in the parenthesis is true
- That condition is a counter indicating that as long as (i < 10), the code block will run 
- key difference between a while loop and a do while loop is that the statements in the code block come before the conditions. 


















