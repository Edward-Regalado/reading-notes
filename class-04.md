## Daily Reading Notes 4
## Chapter 4: Links (p. 74-93)

- links allow you to move from one web page to another 
- links are created using the <a> link </a>
- use href attribute to specify which page you want to link <a href="link">hyperlink</a>
- use word for link that people might use when searching
- when linking to other pages within the same site, you don't need to specify the domain name in the URL
- use target attribute to open link in new window <a href="link.com" target="_blank">
- you can use the id attribute to target elemetn within a page that can be linked to

## Chapter 15: Layout (p. 358-404)

- CSS treats each HTML element like it's own box, either block-level or an inline box 
- Block-level start on a new line and act as the main building blocks of any layout
- Inline boxes flow between surrounding text
- Its common to group a number of elements inside a <div>
- CSS has positioning schemes that allow you to control the layout of a page
- Normal flow: every block-level element appears on a new line 
- Relative Positioning: This moves an element from the position it would be in normal flow, shifting it to the 
top, right, bottom or left. 
- Absolute Positioning: positions elements in relation to its containing element 
- Fixed position: a form of absolute positioning that positions the element in relation to the browser window
- Floating element- allows you to take that element out of normal flow and position it to the far left or right 
of a containing box
- use z-index proptery to control which elements sits on top of other elements
- When using the float element, use the width proptery to indicate how wide the float element should be
- Clear property allows you to say that no element should touch the left and right-hand sides of a box 
- Use the <div> element to represent each column when building a web page with columns width, float, margin. 
- because screen sizes vary so much, web designers often try to create pages of around 960-1000 pixels wide 
- Fixed width layouts do not change size as teh user increases or decreases the size fo their browser window
- Liquid layouts stretch and contract and use percentages to specify the width of each box
- CSS frameworks aim to make life easier by providing the code for common tasks like creating lyaout grids, 
styling forms
- 960a.gs provides a style sheet that you can include in your HTML pages
- You can include multipel CSS files in one page
