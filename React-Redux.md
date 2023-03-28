---
marp: true
footer: "![width:200px](./header_logo.png)"
math: mathjax
---

![bg width:600px](./redux-logo.png)

---

# $~~~~~~~~~~~~~~~~~~~~~~~~~~~$ What is Redux?

- ## Redux is a pattern and library for managing and updating application state, using events called "actions".It serves as a centralized store for state that needs to be used across your entire application, with rules ensuring that the state can only be updated in a predictable fashion.

---

# $~~~~~~~~~~~~~~~~~~~$ Why Should I Use Redux?

- ## Redux helps you manage "global" state, state that is needed across many parts of your application.
- ## The patterns and tools provided by Redux make it easier to understand when, where, why, and how the state in your application is being updated, and how your application logic will behave when those changes occur.

---

# $~~~~~~~~~~~~~~~~~~~$ When Should I Use Redux?

- ## You have large amounts of application state that are needed in many places in the app
- ## The app state is updated frequently over time
- ## The logic to update that state may be complex
- ## The app has a medium or large-sized codebase, and might be worked on by many people

---

# $~~~~~$ How to add Redux to your React project?

- ## Redux is a small standalone JS library. However, it is commonly used with several other packages such as React-Redux, Redux Toolkit, Redux DevTools Extension

- ## Run the below given commands in the terminal from the root directory of the application.
- ## React-Redux is used for official React bindings for Redux.

- ## npm i redux react-redux

---

# $~~~~~~~~~~~~$ Redux Concepts to be Familiar With

- ## Actions - An action is a plain JavaScript object that has a type field. You can think of an action as an event that describes something that happened in the application.

- ## Reducers - A reducer is a function that receives the current state and an action object, decides how to update the state if necessary, and returns the new state: (state, action) => newState. You can think of a reducer as an event listener which handles events based on the received action (event) type.

---

- ## Store - The current Redux application state lives in an object called the store. The store is created by passing in a reducer, and has a method called getState that returns the current state value.
- ## Dispatch - The Redux store has a method called dispatch. The only way to update the state is to call store.dispatch() and pass in an action object. You can think of dispatching actions as triggering an event

---

# $~~~~~~~~~~~~~~~~~~~~~~~~~$ Redux Core Principles

- ## Single Source of Truth
- ## State is Read-Only
- ## Changes are Made with Pure Reducer Functions

---

# Creating Actions

- ## Create a folder by name actions inside src and create an index.js file and write the respective code.

```
export const increment = () => {
  return {
    type: "INCREMENT",
  };
};

export const decrement = () => {
  return {
    type: "DECREMENT",
  };
};
```

---

# Creating Reducer Functions

- ## Create a folder by name reducers inside src and create two js files by name index and counter.
- ## Write the reducer function inside counter file and then export it to index.js.
- ## Inside index.js we combine all our reducer functions using combineReducer.

---

# Example code for counter.js

```
const initialCount = 0;

const counterReducer = (state = initialCount, action) => {
  switch (action.type) {
    case "INCREMENT":
      return state + 1;
    case "DECREMENT":
      return state - 1;
    case "RESET":
      return (state = 0);
    default:
      return state;
  }
};

export default counterReducer;
```

---

# Example code for index.js

```

import counterReducer from "./counter";
import { combineReducers } from "redux";

const rootReducers = combineReducers({
  counterReducer,
});

export default rootReducers;

```

---

# Creating Store

- ## Create a file by name store.js inside src.

```
import { createStore } from "redux";
import rootReducers from "./reducers/index";

const store = createStore(
rootReducers,
);

export default store;
```

---

# We need to centralize our store

- ## Import provider function from react-redux and store in index.js

```
import store from "./store";
import { Provider } from "react-redux";

ReactDOM.render(
  <React.StrictMode>
    <Provider store={store}>
      <App />
    </Provider>
  </React.StrictMode>,
  document.getElementById("root")
);
```

---

# We need to use the state and perform actions in app.js.

- ## We will use useDispatch to dispatch actions and useSelector to access the state from our reducer.
- ## To dispatch actions we need to import the required action present in actions folder.

```

import { useSelector, useDispatch } from "react-redux";
import { increment, decrement } from "./actions/index";

```

---

```
function App() {
  const counterValue = useSelector((state) => state.counterReducer);
  const dispatch = useDispatch();

  return (
    <div>
      <h2>{counterValue}</h2>
      <button onClick={() => dispatch(increment())}>Increment</button>
      <button onClick={() => dispatch(decrement())}>Decrement</button>
    </div>
  );
}

export default App;
```

---

# You've implemented redux successfully in your React application. To explore more features of Redux visit - https://redux.js.org/
