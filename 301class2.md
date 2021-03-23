## Converting a Function to a Class
- Create an ES6 class (same name), that extends React.Component.
- Add a single empty method to it called render().
- Move body of function into the render() method.
- Replace props with this.props in the render() body.
- Delete the remaining empty function declaration.
- The render method will be called each time an update happens, but as long as we render <Clock /> into the same DOM node, only a single instance of the Clock class will be used. 

## Handling Events 
- React events are named using camelCase
- with JSX you pass a function as the event handler, rather than a string
- <button onclick="activateLasers()">Activate Lasers</button> vs <button onClick={activateLasers}>Activate Lasers</button>
- You cannot return false to prevent default behavior in React and you must call preventDefault explicitly.
- when using React, you generally don't need to call addEventListener to add listeners to a DOM element after it is created.
- When you define a component using an ES6 class, a common pattern is for an event halder to be a method on the class.

## Conditional Rendering
- In React, you can create distinct components that encapsulate behavior you need. Then, you can render only some of them, depending on the state of you application.
- conditional rendering in React works teh same way conditions work in JS. Use JS operators like if or teh conditional operator to create elements representing the current state, and let React update teh UI to match them.

## Element Variables
- you can use variables to store elements. This can help you conditionally render part of the component while the rest of the output doesn't change.

## Inline If with Logical && Operator
- you may embed experssions in JSX by wrapping them in curly braces
- JS true && expression always evaluates to expression, and false && expression always evaluates to false.
- If the condition is true, the element right after && will appear in the output. If false, React will ignore and skip it.

## Inline If-Else with Conditional Operator
- another method for conditionally rendering elements inline is to use the JS conditional operator condition ? true : false
- <div> The user is <b>{isLoggedIn ? 'currently' : 'not'}</b> logged in. </div>
