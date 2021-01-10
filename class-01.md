# Duckett HTML (HyperText Markup Language)

## **Structure (p 12-39)**
- HTML pages are text documents 
- heading and subheading represent a hierarchy of information 
- seperatre out text to give document structure and each topic might have a new paragraph with a sub-heading
- HTML elements are made up of two tags: opening and closing <>
- HTML uses element to describe the structure of pages
- Tags act like containers and describe the information between the tags
- <html></html> everything between is html code
- <body></body> main broswer window
- <title> displayed in URL or tab for that webpage 
- <h1></h1> main heading
- <p></p> paragraph tags
-<h2></h2> sub-heading 
- characters within brackets indicate the tag's purpose <p>
- "tag" and "element" are often used interchangeably
- Attributes provide additional information about the contents of an element and appear in the opening tag <p lang="en-us">Paragraph in English</p>
- Majority of attributes can only be used on certain elements 
- Atttributes require a name and a value
- Use source code to learn how web pages are made, as well as books and online tutorials 
- 


## **Extra Markup (p. 176-199)**
- Indentify different versions of HTML
- Every element needed a closing tag except for empty elements <img />
- Because there have been serveral versions of HTML, each webpage should begin with <!DOCTYPE html> 
- comments in HTML <!-- comment goes here --> 
- add comments to your code makes it easier to understand for you and someone else down the road
- Every HTML element can carry the id attribute.. it is used to uniquely identify that element from other elements on the page
- id attribute should state with a letter or an underscore (not a number or underscore)
- id attribute is known as a global attribute bc it can be used on any element 
- Every HTML element can also carry a class attribute and help to identify several elements in a document
- Class value should describe the class it belongs to
- Block elements always appear to start on a new line in the browser <h1>, <p>, <ul>, and <li>
- Inline elements always appear to continue on the same line as their neigbouring elements <a>, <b>, <em>, and <img>
- Grouping Text & Element in a block <div> allows you to group element together in one block-level box
- Using an id or class attribute on the <div> element means that you can create CSS style rules to change appearance of all elements contained within it
- Use <div> element to make it easier to follow code
- Grouping Text & Element Inline <span> elements acts like an inline equivalent fo the <div> element 
- <span> is used to differentiate it from surrounding text using CSS
- class and id attributes are often used with <span> elements to explain the purpose of the <span> and so CSS styles can be applied to elements
- <iframe> is like a little window on your web browser (embed a google map) and contains src/height/width/
- <meta> element lives inside the <head> element and contains information about the web page
- Most common attributes for <meta> are name (intention to specify) and content (description is specified) 
- Description is commonly used by search engines to understand what the page is about
- Keywords contains a list of comma-seperated words that a user might search on to find the page
- Escape Characters are used to includ special character in your pages such as <,>, and &copy; 
  9


## **HTML5 Layout (p. 428-451)**
- Web dev use <div> elements to group together related elements on the page and use class or id attributes to indicate the role of the <div> 
- Navigation is used to contain the major navigational blocks on the site such as the primary site navigation
- Artical element acts as the container for any section of a page that could stand alone and potentially be syndicated (blog entry, comment or forum post)
- Asides <aside> used as inside an article element (contains information related to article but not essential) It's also used outside of an <article> and acts like a containerthat is related to the entire page.
- Sections <section> group related content together and typically each section would have it's own headin. Also, can be used to split up a long article. 
- Heading Groups <hgroup> purpose is to group together a set of one or more <h1> through <h6> elements so that they're treated as one single heading
- Figures <figure> <figcaption> (text description) can be used to contain any contecnt that is referenced from the main flow of an article such as images, videos, graphs, diagrams and code samples
- Sectioning Element <div> remains an important way to group together related elements, esp when there is no suitable element
- Linking block-level element with <a> allows to turn an entire block into a link
- New elements provide clearer code (compared) to using multiple <div> elements
- Older browswers that don't understand HTML5 need to be told which elements are block-level
- Extra JS is needed for HTML5 to work in IE8 and older



## **Process & Design (p. 452-475)**
- Every website should be designed for the target audience and not just for yourself or site owner
- Content and design should be influenced by the goals of your users
- discover underlying motivations and specific goals of users
- Are they looking for entertainment or do they need to achieve a specific goal?
- know who is coming to your site adn why, so now you can work out what information they need in order to achieve their goals quickly and effectively
- Prioritize levels of information from key points down to non-essentials
- Once you know what needs to appear on your site, you can start to organize the information into sections or pages
- Aim is to create a diagram of the pages, also know as a site map and use card sorting to figure out what goes on which page
- Wireframe is a simple sketch of the key information that needs to go on each page of a site- show hierarchy of the information and how much space it might require
- Primary aim of any kind of visual design is to communicate- organize the information on a page so it help the user understand it's importance
- Designers create something known as a visual hierarcy to help users focus on the key messages that will draw people's attention, then guide them to subsequent messages
- Group content into blocks or chunks makes the page look simpler, thus users should be able to identify the purpose of each block without processing each individual item
- Organize and prioritize the information to communicate your message and help users find what they're looking for
- Use size, color and style to create visual hierarchy
- Navigation menu concise (less than 8 links), clear (single descriptive word) and selective 
- Good navigation provides context and lets the user know where they are in the website at that moment 
- Interactive links should be the proper size and should change appearance when the user hovers

## JS Chapter 1: "The ABC of Programming" (p. 11-52)
- use JS to select any element, attribute or text from an HTML page
- JS alows you to make web pages more interactive by accessing and modifying the content and markup used 
- specify a set a of steps for the browswer to follow (recipe) which allows it to access or change the content of a page
- JS makes the web page feel interactive by responding to what the user does 
- specify when a script should run when a specific event has occurred- button is pressed, link is clicked, cursor hovers over element, etc
- CSS uses rules to indicate how the contenct of one or more elements should be displayed in the browswer. Each rules have a selector and a declaration block. 
- A script is a series of instructions that a computer can follow to achieve a goal (step-by-step)
- Define the goal and task that you want to achieve
- Design the script to split the goal out into a series of tasks that are going to be involved in solving this puzzle (flowchart)
- Code each step into programming language that the computer understands (JS)
- Syntax: how you put those words together to create instructions computers can follow
- Computers solve problems programmactically; they follow series of instructions, one after another 

## How do computers fit in the world around them?
- Each physical thing in the world can be represented as an object
- An event is teh computer's way of sticking up its hand to say somethign happened
- Programmers choose which events they respond to... when a specific event happens, that event can be used to trigger a specific section of the code
- Scripts use different events to trigger different types of functionality
- Methods represent things people need to do with objects. They can retrieve or update the values of an object's properties
- Methods are like questions and instructions that tell you something about that object or change the value of one or more of that object's properties
- Computers use data to create models of things in the real world
- The events, methods, and properties of an object all relate to each other: events can trigger methods, and methods can retrieve or update an object's properties
- Web browswers are programs builts using objects
- All major browsers use a JS interpreter to translate your instructions into instructions the computer can follow

## How do I write a script for a web page?
- Web devs usually talk about 3 languages used to create web pages: HTML, CSS and JS
- HTML (content layer) gives the page structure and adds semantics 
- CSS (presentation layer) backgrounds, borders, box, dimensions, colors, fonts, etc
- JS (behavior layer) changes how the page behaves, adding interactivity (keep as much of our JS as possible in seperate files)
- JS is written in plain text, just like HTML and CSS, so you don't need any tools to write script
- When you want to use JS with a web page, you use the HTML <script> element to tell the brower it is coming across a script. Its src attribute tells people where the JS file is stored
  - You may see JS in the HTML between opening <script > and closing</script> tags but it's better to put scripts in their own files
 



