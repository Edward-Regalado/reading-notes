## List and Keys
- map() function to take an array of numbers and double their values. 
- const numbers = [1, 2, 3]; const doubled = numbers.map((number) => number * 2); console.log(doubled);

## Rendering Multiple Components
- you can build a collection of elements and include them in JSX using {}.
-loops through the numbers array using map() function and return a <li> element for each item, assign results to listItems.
- const numbers = [1, 2, 3]; const listItems = number.map((number) => <li>{number}</li>);
- ReactDOM.render (<ul>{listItems}</ul>, document.getElementById('root'));

## Keys 
- keys help React identify which items have changed, are added, or removed.
- keys should be given to the elements insdie the array to give the elements a stable identity.
- best way to pick a key is to use a string that uniquely identifies a list item among its siblings- most often you would use IDs from your data as keys.
- <li key={number.toString()}>{number}</li>
- when you don't have stable IDs for rendered items, you may use the item index as a key as a last resort.
- using indexes for keys can negatively impact performance and may cause issues with components state.
- React will default to using indexes as keys if not assigned.

## Extracting Component with Keys
- keys only make sense in the context of the surrounding array

## What is React?
- React is a declarative, efficient, and flexible JS library for building user interfaces. 
- It let you compose complex UIs from small and isolated pieces of code called "components".
- It uses components to tell React what we want to see on the screen.
- A component takes in parameters, call props, and returns a hierarchy of views to display via the render method.
- The render method returns a description of what you want to see on the screen. React takes the description and displays the result.
- Devs use a special syntax called JSX, whihc makes these structures easier to write.
- You can put any JS expression within braces inside JSX {}.
- Each React element is a JS object that you can store in a variabel or pass around in your program.

## Function Components
- function components are a simpler way to write components that only contain a render method and don't have thier own state. 
- Instead of defining a class which extends React.Component, we can write a function that takes props as input and returns what should be rendered.
- FC are less tedious to write than classes, and many components can be expressed this way.
