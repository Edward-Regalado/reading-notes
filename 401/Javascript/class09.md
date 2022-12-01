1. Explain the different between a query string parameter and a path parameter. A path parameter defines the resource location, while the query paramter defines sort, pagination, or filter operations.
2. What would our API URL with a path id parameter be given the following information: http://out-site.com/v3/stuff/things
    1. Domain: http://our-site.com
    2. v3
    3. model name: stuff
    4. id: things

3. We have created a dynamic API with an “interface”. Describe how that interface works to a non-technical friend.

Review Auth Server Build
1. Describe how you would use middleware to implement basic and bearer auth. 
    - The Basic Authentication processes is initiated by invoking a POST on your /oauth route with a basic authentication header. The Basic Authentication Middleware should at this point validate the user account in our database, and return an object with the re-authentication/bearer token and the user object or an error object.
    - Re-Authentication can be achieved on any route in the express server, not just the authentication routes. 
        1. The tokenAuthentication middleware will re-authenticate the user.
        2. If the token is valid, the route handler will execute as it normally would
        3. If the token is invalid or the capability is not present for the users, the system should respond with a standard error.
2. Describe the handshake necessary to implement OAuth. The handshake involves the Authorization request and the access token request. The access token is the end goal because it allows the app to finally access the user's information.
3. Describe how Role Based Access Control works to a non-technical friend. Think of the Role Based Access Control as key cards in a hotel. Guests are only allowed to have access to their specific room, whereas the front desk can access all rooms in the building. RBAC simple restricts network access (routes and information) on the roles of individual users within a company.

Reflection
1. What are your learning goals after reading and reviewing the class README?


Saturday Notes:

- The interview process today is around can you code and not as obscure as the late 90s and early 2000s.
- Sometimes the process today will find false negatives.
- Phone screen: at least 3 out of 5 engineers agree to move forward. It will be a combination of technical and behavior questions. Must do research to prepare for these.
- Phone screen questions are supposed to be easy.
- A Good github favors a certain type of candidate - more green commits (turn on public and private contributions)
- Be professional but be yourself.
- Once you get the phone screen, start doing research about the company and their interview process (what tools can I use, etc). Check out glass door reviews.
- Behavior questions will have something to do with company philosophy.


- speaker Brian Nations - non-traditional candidate. Principle instructor at CF and currently working at AWS.
- Topic of Talk: Css position relative and absolute
- relative position parent allows you to position elements within it to position absolute
- transitions slide bar
- vh and vw size: as the screen gets smaller (left to right), we start stacking elements on the page
- code daily, checkout when you need, but check in
- be okay with learning new things and making mistakes

# Redux Reading

1. What is the first principle of Redux? Whether your application is simple or complex with a large amount of UI and data state. Everything that changes in your  application is contained in a single object called state or the state tree.
2. what is a store and what do we use our reducers for within that store? It binds together the 3 principles of Redux. It holds the current application state object and allows you to dispatch actions. The reducer tells how state is updated with actions and you need to specify the reducer when creating the store.
3. Name three Redux store methods given to us by createStore and describe their use.
    1. getState()- returns the current state of the redux store.
    2. dispatch()- allows you to dispatch actions to change the state of your application.
    3. subscribe()- lets you register a callback that the redux store will call anytime an action has been dispatched.
4. Explain to a non-technical recruiter what combineReducers() does and why it is useful. It's a helper function that turns an object whose values are different reducing function into a single reducing function hta twe can pass to createStore().


- The state tree is redundant - every time you need to change the state, you need to dispatch an action... this is the only way to change state.
- pure function - the return value solely depends the their arguments. They're predictable and don't any observable side effects form network or database calls.
- Some functions in Redux need to be pure.
- UI in applications is most predictable when it is described as pure function of the application state.
- The state mutations in your application need to be described as a pure functions - the function takes the previous state, the action being dispatched, and returns the new state.
- If the reducer receives undefined as the state argument, it must return what it considers to be the initial state of the application



1. Why create multiple reducers? It helps maintain the application state.
2. How would you combine multiple reducers? Import combineReducers from redux, create individual reducers with their own state and action, then use the combineReducers() function.
3. How will you manage state as an immutable object? why? You never want to return the original state object. Instead use object destructuring on the original state object and return a new state object.

Redux Docs: Using Combined Reducers

1. combineReducers is a utility function to simplify the most common use case when writing Redux reducers.
2. Explain how combineReducers assembles the new state tree. combineReducers will call each slice reducer with its current slice of state and the current action, giving the slice reducer a chance to respond and update its slice of state if needed.
3. How would you define initial state in an app using combineReducers? 
    - take preloadedState as its second argument in the createStore function
    - have the root reducer return the initial state value when the state argument is undefined.

Redux Docs: Combined Reducer Syntax

1. Why will you want to split your reducing functions as your app becomes more complex? helps you organize your reducers to manage their own slice of state.
2. The combinedReducer() helper function turns an object whose values are different reducing functions into a single reducing function you can pass to createStore().
3. What is a popular convention when naming reducers? Name reducers after the state slice they manage.