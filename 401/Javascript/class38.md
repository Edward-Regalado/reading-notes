async actions

1. Why use Redux middleware? Allows you to intercept every action sent to the reducer so you can make changes to the action or cancel the action. Helps you with logging, error reporting, making asynchronous requests, and much more.
2. Consider the Redux Async Data Flow Diagram. Describe the flow in your own words.
    - Something happens in your application (clicking a button). 
    - the app code dispatches an action to the Redux store.
    - store runs the reducer function again with teh previous state and the current action, and saves the return values as the new state. - The store notifies all parts of the UI that are subscribed that the store has been updated.
    - each  UI component that needs data from the store check to see if the parts of the state they need have changed
    - each component that sees its data has changed forces a re-render with the new data.
3. How are we accommodating async in our Redux app? "Thunk" functions let us write async logic ahead of time, without knowing what Redux store is being used. A Redux thunk function receives dispatch and getState as arguments, and can dispatch actions like 'this data was received from an API response'

thunk middleware

1. Why would you need redux-thunk middleware? With a plain basic Redux store, you can only do simple synchronous updates by dispatching an action. Middleware extends the store's abilities, and lets you write async logic that interacts with the store.
2. Redux Thunk middleware allows you to write action creators that return a ____ instead of an action. A Function
3. Describe how any return value from the inner thunk function will be made available. Any return value from the inner function will be available as the return value of dispatch itself.



Redux Toolkit (RTK)

1. What concerns are addressed by Redux Toolkit? 
2. What does configureStore() do?
3. How would I use createSlice()?

MobX

1. What is Mobx?
2. How does MobX make it “impossible” to produce an inconsistent state?
3. How would we build a reactive user interface?

Tutorial

1. What take-away(s) did this tutorial provide?

# Readings

## Class 37 Redux Thunk Async logic - done
## Class 38 Learn Modern Redux: learn with Jason - done
## Class 39 React native - done