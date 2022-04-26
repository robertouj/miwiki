---
title: React - Hooks
description: 
published: true
date: 2022-04-05T12:51:41.661Z
tags: 
editor: markdown
dateCreated: 2022-04-02T21:45:34.212Z
---

# Hooks API

Hooks let you use state and other React features without writing a class.

## Custom Hooks

Building your own Hooks lets you extract component logic into reusable functions.

It is similar to classes where you can create states (like properties) and functions (like methods) and import them into components.

Then it returns an array with the states and functions needed to use into a component.

```js
import { useState } from 'react';

const useCounter = () => {
  const [counter, setCounter] = useState(0);

  const increment = () => setCounter( counter + 1 );
  const reset = () => setCounter(0);

  return [counter, increment, reset];
}

export default useCounter
```

The hook is similar to a component, but most of the times we don't need to import the `import React from 'react'` because it doesn't need to return JSX.

## useState

This hook is used to manage the states of the variables that need to change in the app. 

The initial value passed as the first argument `initialState`.

It returns an array with two elements:

- The current `state` value.
- The `setState` updater function.

```js
const [someState, setState] = useState(initialState);
```

### Updater function (setState)

The `setState` updater is called to update the previous state. It is something that need to change in the DOM, accepts a new state value and re-render (DOM) the component only if the new stat fiffers.

```js
setState(state + 1);
```
 
This **udater is asynchronous**, so if the new state is computed using the previous state, you can pass a callback function to setState. The function will receive the previous value, and return an updated value.

```js
const [counter, setCounter] = setCount(initialCounter);
// ...
setCounter(prevCounter => prevCounter + 1);
```

Another example with an object.

```js
setProduct(prevProduct => { ...prevProduct, name: 'La Exportiva Solution 2' });
```

### Collection: Add, update, remove

A collection of states can be managed saving an array of states.

```js
const [states, setStates] = useState(initialStates);
```
Add

```js
const stateAdd = (newState) => setStates([...states, newState]);
```

Update

```js
const statesUpdate = (updatedState) =>
  setStates(
    states.map((state, index) => (state.id === index ? updatedState : state))
  );
```

Delete

```js
const stateDelete = (stateId) => {
  setTodos(states.filter((state, index) => index !== stateId));
};
```

## useEffect

With React is possible to do more than only show HTML (DOM manipulation)

- HTTP requests
- Interaction with browser API

The name is given because useEffect allow to do a secondary effect, other than rendering a DOM.

- All the effects are executed on the first load of the component.
- The first paramete is an arrow function with the actions of the secondary effect.
- The second parameter is used to control when the side-effect is executed.

### No dependency

The function will be executed every time there is a render of the component.
It means, eacht time the component is loaded or when there is a change in a state.

```js
useEffect(() => {
  console.log('useEffect no dependency');
  return () => {
      console.log('cleanup useEffect no dependency');
  }
});
```

### With an empty array

The function will be executed only with the first load of the component.

```js
useEffect(() => {
  console.log("useEffect []");
  return () => {
    console.log("cleanup useEffect []");
  };
}, []);
```

### With dependencies

The function will be executed on first load and whenever of the states in the dependency changes.

```js
useEffect(() => {
  console.log("useEffect [counter1, counter2]");
  return () => {
    console.log("cleanup useEffect [counter1, couter2]");
  };
}, [counter1, counter2]);
```

When the effect **has a function as a dependency**, it needs to include the function in the dependencies array.

It **also needs to use the hook useCallback** inside the function to prevent memory overload because each loading of the effect load the dependent function with its dependent variables.

```js
const updatePosts = useCallback(() => {
  getPosts(user.id).then((newPosts) => {
    setsPosts(newPosts);
  });
}, [user.id]);

useEffect(() => {
  if (user?.id) {
    updatePosts();
  }
}, [user, updatePosts]);
```

If the function is only called within the effect, it can be solved writing the function inside.

```js
useEffect(() => {
  const updatePosts = () => {
    getPosts(user.id).then((newPosts) => {
      setsPosts(newPosts);
    });
  };

  if (user?.id) {
    updatePosts();
  }
}, [user]);
```

### Managing unmount components: Clean up

When a component reloads by an effect, this component is unmounted and React creates a completely new component. Previously, React executes a cleanup of the component.

For instance, when an effect is adding something permanent to memory, such as a listener, it is important to clean it up to free memory when the component is unmounted. It prevents future errors and performance problems.

Returning a function inside an effect make it possible to do clean up actions when the component is unmounted.

```js
useEffect(() => {
  const handleResize = () => setWindowWidth(window.innerWidth);
  window.addEventListener('resize', handleResize);

  return () => { 
    // actions when the component is unmounted
    window.removeEventListener('resize', handleResize);
  }
}, []);
```

### Other

:exclamation: useEffect don't accept async functions. It needs to call a function outside.

```js
useEffect(() => {
  if (stateEdit) {
    setFormValues(stateEdit); // this would be an asyn function
  }
}, [stateEdit]);
```

## useContext

Within a `/contexts` folder can create all the **providers** needed (context files) in the app, like for example `UserContext.js`.

The `UserContext.Provider` share needed variables and functions in a object inside the value property and is returned as a provider component with a children.

```jsx
import React, { createContext } from "react";

const UserContext = createContext();
const initialUser = { id: 1, name: "Miguel" };

const UserProvider = ({ children }) => {
  const [user, setUser] = useState(initialUser);

  const login = () => setUser(initialUser);

  const logout = () => setUser(null);

  const data = { user, login, logout }

  return <UserContext.Provider value={data}>{children}</UserContext.Provider>;
};

export { UserProvider };
export default UserContext;
```

The `userProvider` component is used as a wrapper for the components that need the context.

```js
import { UserProvider } from "./contexts/UserContext";

function App() {
  return (
    <div>
      <UserProvider>
        <!-- here all the components that need to use the context -->
      </UserProvider>
    </div>
  );
}

export default App;
```

Then the files called **consumers** can use this context importing the context and using the `useContext` hook.

```js
import React, { useContext } from "react";
import UserContext from "../contexts/UserContext";

const Navbar = () => {
  // destructuring the data
  const { user, login, logout } = useContext(UserContext);

  return (
    <>
      <h2>`Hi ${user.name}`!</h2>
      { user ? <button onClick={logout}>Log out</button> : <button onClick={login}>Log in</button>}
    </>
  );
};

export default Navbar;

```
