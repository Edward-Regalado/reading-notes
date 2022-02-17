## Itroduction JSX
- JSX is a sytax exstension to Javascript
- JSX produces React "elements"
- React doesn't require using JSX, but most people find it helpful as a visual aid when working with UI inside JS code
- allows React to show more useful error and warning messages
- const name = 'Josh Perez'; const element = <h1>Hello, {name}</h1>;
- JSX expressions become regular JS function calls and evaluate to JS objects. Can be used inside of if statements and for loops.
- React DOM uses camelCase property naming convention instead of HTML attribute names.

## Rendering Elements
- elements are the smallest building blocks of React apps.
- React elements are plain objects and the React DOM takes care of updating the DOM to match the React elements.
- <div id="root"></div> - this is the "root" DOM node because everything insdie it will be managed by React DOM. 
- const element = <h1>Hello, world</h1>; 
ReactDOM.render(element, document.getElementById('root'))
- Applications built with just React usually have a signle root DOM node. 
- React elements are immutable. An element is like a single frame in a movie: it represents the UI at a certain point in time.
- React DOM compares the element and its children to the previous one, and only applies the DOM updates necessary to bring the DOM to the desired state.

## Components and Props
- components let you split the UI into independent, reusable pieces, and think about each in isolation.
- components are like JS functions: they accept arbitrary inputs(called "props") and return React elements describing what should appear on the screen.

## Function and Class Components
- simplest way to define a component is to write a JS function.
- function welcome(props) {return <h1>hello, {props.name}</h1>};
- You can also use ES6 class to define a component: class Welcome extends React.Component { render() {
  return <h1>Hello, {this.props.name}</h1>;
}
- When React see an element representing a user-defined component, it passed JSX attributes and children to this comp as a single object. 
- React treats components starting with lowercase as DOM tags. 

## Composing Components
- components cn refer to other components in their output. This lets us use the same component abstraction for any level of detail.
- typically, new React apps have a single App component at the very top. 
- name props from the component's own point of view rather than the context in which it is being used.
- Props are Read-only- when you declare a component as a function or a class, it must never modify its own props.
- All React components must act like pure functions with respect to their props.

## Handling Events 
- React events ar named using camelCase.
- With JSX you pass a function as the event handler, rather than a string.
- When using React, you generally don't need to call addEventListener to add listeners to a DOM element, just provide a listener when the element is initially rendered.
- If you aren't using class fields syntax, you can use an arrow function in the callback.

