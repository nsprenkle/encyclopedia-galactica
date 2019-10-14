# React

[NodeJS Introduction (Tutorials Point)](https://www.tutorialspoint.com/nodejs/nodejs_introduction.htm)

[React.js: Getting Started (Pluralsight)](https://app.pluralsight.com/library/courses/react-js-getting-started/table-of-contents)

## What is it?
- JavaScript framework for building UI components
- Build modular components, each has a state and passes data and functions to child components with properties
- Written with JSX

Argument for combining JS and HTML, the two are inextricably linked and doesn't make sense to separate "concerns" since it's more like separation of technologies.

2 technologies: react & react-dom
Separated because, for example, you can run React in Node for server-side rendering and never actually touch the DOM, React = engine, react-dom = interface to DOM.

Virtual DOM - memory representation of DOM for smarter refreshing of page, limiting unnecessary refresh by grouping updates and not refreshing unless changes are identified.

Container - responsible for doing out-of-app communication (e.g. AJAX) and maintain state as well as "side effects" (error handling.) That way components don't have as much error handling and can be dumb displays.


# Redux

## But first, flux
 architecture of unidirectional data flow, action calls the dispatcher which updates state in the store which updates the view
	- Action: someone does something on the page (view)
	- Dispatcher: receives action to be handled by reducer
	- Reducer: logic to update state accordingly
	- Store: shared data updates the view
	- View: page

a library which enables a flux-like architecture. Not react specific so you also need a binding library to bind state to react components.

Basically - you have one finite state machine (FSM) which the app then is built around updating and displaying.

Allows for time travel. Since there's a centralized source of truth, you can replay user actions and should get the same app state.

May have to rethink app architecture since there's one centralized state, e.g. don't save derived state in centralized state, calculate when needed in the tree.

Testing - allows separate testing of components and state engine. For engine, can test every permutation of the app. For components, can test each relevant state. 

Connect - way to specify which state changes to re-render on go over this more…

Idea: make managing state easy

  - There's a model for the app state…
  - … but no getters/setters on the model
  - Instead you dispatch an action (JS object) which describes an intent change to the state…
  - This gets put on the stack and is handled by a reducer which takes state and action to return new state objects
  - Changes to state occur in the order they appear on the stack so we remove race conditions
  - Make this modular

Redux - React data flow
	1. Setup
		a. Associate certain actions with the dispatcher (Map dispatch to props)…
		b. … which are accessed through this.props.actions in the container and passed to child elements
		c. Associate state changes with re-rendering (Map state to props)
	2. Data Flow
		a. User does something to a child container
		b. Child container change triggers a callback function passed in as a property.
		c. The callback function (in the parent) passes through to dispatcher…
		d. … which updates application state…
… which triggers a re-render of the component