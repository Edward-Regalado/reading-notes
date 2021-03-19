## Daily Reading Notes 7 Duckett HTML 
## Chapter 6: Table (p. 126-145)
- There are several types of information that need to be displayed in a grid or table: sports results, stock reports, train timetables
- Think of a grdi made up of rows and columns (spreadsheet)
- Table represent information in a grid format
- <table> element used to create a table- contents are written out row by row.
- <tr> </tr> indicates the start of each row and <td> (table data) goes inside and represents each new cell in the row.
- <th> (table heading) element is used to represent the heading for either a column or row- use the scope attribute to indicate if its a column or row 
- use the colspan in a <th> or <td colspan="2"> to indicate how many columns that cell should run across.
- The rowspan attribute can be used on <th> and <td> to indicate how many rows a cell should span down the table <td rowspan="2">.
- There are threee elements that help distinguish between the main content of the tabel and the first and last rows- these element help people with e-readers. <thead></thead>, <tbody></tbody>, <tfoot></tfoot>. This is very similar to the stand HTML document model. 
- All old code/outdate attributes inside <tb>, <th> such as table width & spacing, border & background have been replaced by the use of CSS. 
- For long tables you can split the table into a <thead>,<tbody>, and <tfoot>.


## Ducket JS 
## Chapter 3: Functions, Methods, and Objects (p. 106-144)
- The new keywordand Object constructor create a black object that you can add properties and methods too. var hotel = new Object ();
- Each statement that add a property or method should end with a ; 
- To update the value of properties in an object, use dot notation or square brackets syntax. hotel.name = 'Park'; or hotel ['name'] = 'Park'; 
- delete hotel.name; or hotel.name = ''; to set property to blank
- Each statment that creates a new property or method for this object ends in a ; ( not a comma, which is used in the literal synatx).
- The name of the contructor function usually begins with a capital letter (unlike other functions).
- to access the properties or methods inside the obejct hotel, simply use dot notation. hotel.name or hotel.checkAvailability();
- Ways to create object: Literal notation var hotel = {} or Object contructor notation var hotel = new Object(); 
- Literal Notation: A colon separates teh key/value pairs and there is a comma between each key/value pair var hotel = {name: 'Quay', rooms: 40, booked: 25}; 
- Object Constructor Notation - this function can be used to create multiple objects. function Hotel (hame, rooms, booked) { this.name = name; this.room = rooms; this.booked = booked;};
- The keyword this is commonly used inside functions and objects. Where the function is declared alters what this means. It always refers to one object, usually the object in which the function operates.
- Method of an Object: when a function is defined inside an object, it becomes a method. 
- In JS, data is represented using name/value paris. To organize your data, you can use an array or object to group a set of related values. 
- Variable has just one key (the variable name). 
- Arrays can store multiple pieces of information, each piece of information is separated by a comma and are nested inside of [].
- Functions can take parameters (information required to do thier job) and may return a value.
-Web browsers implement object that represent both the browser window and the document loaded into the browser window. 
- An object is a series of variables and functions that represent soemthign from the world around you and variables are known as properties of that object; functions are known as methods of the object. 
