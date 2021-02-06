## Daily Reading Notes 9
## Ducket HTML 
## Chapter 7: Forms (p. 144-175)
- HTML borrows the concepts of a form to refer to different elements that allow you to collet information from visitors to your site. 
- There are several types of form controls that you can use to collet information: Text input, Password input, Text area, Radio buttons, Checkboxes, Drop-down boxes, submitting forms, image buttons, uploading files
- Information is sent from the browser to the serving using name/value pairs.
- Form controls live inside a <form> element. This element should always carry the action attribute and will usually have a method and id attribute too.
- Forms can be sent using one of two methods: get or post
- Get method should be used for short forms, when you are just retrieving data from the web server.
- post method should be use because allows users to upload files, is very long, contains sensitive data, add information to, or deletes info from a database
- <input type"text"> element is useed to create several different form controls and value of the type attribute determines what kind of input they will be creating
- <input type="password" name="password goes here"> when the type attribute has a value of passowrd it creates a text box that acts just like a single-line text input, except the characters are blacked out.
- <textarea></textarea> element is used to creat mult-line text input - use CCS to control the width and height of textarea
- <input type="radio"> allows users to pick just one of a number of options.
- <input type="checkbox"> allows users to select and unselect one or more options
- <button> elements was introduced to allow users more control over how their buttons appear, and to allows other element to appear inside the button
- <label> used to wrap around both the text description and the form input or kept seperate from the form control and use the "for" attribute to indicate which form control it is a label for via classes and ids.
- <fieldset> used to group related form controls together inside.
- <legend> used to title the fieldset box

## Chapter 14: List, Tables & Forms (p. 330-357)
- the list-style-type property allows you to control the shape or style of a bullet point
- list-style-image use an immage as a bullet point
- CSS is used to control the appearance of form element. This is both to make them more attractive adn to make them more consistent across different browsers
- forms are easier to use if the form controls are vertically aligned using CSS
- forms benefit from styles that make them fell more interactive
- use <div> element in forms to ensure that each question appears on a new line.

## Ducket JS
## Chapter 6: Events (p. 243-292)
- events occur when users click or tap on a link, hover or swipe ovver an element, type on a keyboard, resize the window, or when the page they requested has loaded.
- When an event occurs, or fires, it can be used to trigger a particular function. Different doce can be triggered when users interact with different parts of the page.
- when an event has occured, it is often described as having fired or been raised and they trigger a function or script.
- Event listeners are a more recent approach to handling events since they can deal with more than one function at a time (not supported my older browsers) element.addEventListerner(event', funcionName [ Boolean]);
- HTML elements nest insdie other elements. If you hover or click on a link, you will also be hovering or clicking on its paretn elements.
- Binding is the process of stating which event you are waiting to happen, and which element you are wiating for that event to happen upon.
- event delegation monitors for events to happen on all of the children of an element.
