## Thinking in React
- React is a premier way to build big, fast Web apps with JS. 

## Step 1: Break The UI ino a Component Hierarchy
- Break the UI Into a Component Hiearchy and draw boxes around every component
- Use the single responsibility principle - a component should ideally only do one thing, and if it ends up growing, it should be decomposed into smaller subcomponents.
- Using the JSON data model and if your model was built correctly, your UI and component structure will map nicely. 
- UI and data mdoels tend to adhere to the same information achitecture.
- Once you identified the components, arrange into a hierarchy: FiterableProductTable, SearchBar, ProductTable- ProductCategoryRow, ProductRow

## Step 2: Build a Static Version in React
- Easiest way is to build a version that takes your data model and renders the UI but has no interactivity.
- It's best to decouple these processes because building a static version requires a lot of typing and no thinking, and adding interactivity requires a lot of thinking and not much typing.
- Static Version - build components that reuse other components and pass data using props.
- Props are a way of passing data from parent to child.
- State is reserved only for interactivity, meaning data changes over time.

## Step 3: Identify the Minimal Representation of UI State
- to make your UI interactive, you need to be able to trigger changes to your underlying data model via state.
- DRY: Dont Repeat Yourself.
- Think of all the pieces of data in your application, then figure out which one is state. 
- Ask 3 questions about each piece of data: is it pass in from parent via props? Does it remain unchanged over time? Can you compute it based on any other state or props in your component?

## Step 4: Identify Where your State should live
- identify which component mutates, or owns, this state.
- React is all about one-way data flow down the component hierarchy.
- Identify every component in your application
- Find a common owner component (a single component above all teh components that need the state in the hiearchy)
- Either the common owner or another component higher up in the hierarchy should own the state.
- If you can't find a component where it makes sense to own the state, create a new component soley for holding the state and add it somewhere in the hierarchy  above the commmon owner compoenent

## Step 5: Add inverse Data flow
- React makes data flow explicit to help you understand how your program works, but does require more typing than traditional two-way data binding.
- Components should only update their own state
- Use onChange events on the inputs

