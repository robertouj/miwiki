---
title: React - Codes (short)
description: 
published: true
date: 2022-04-06T16:11:22.464Z
tags: 
editor: markdown
dateCreated: 2022-04-02T21:50:02.257Z
---

# React - Codes (short)

Some useful codes to use with React.

## Fetch an API

The example shows the first calling to the API that retrieve the collection.

### With Axios

This library provide by default the results in JSON format. It only needs the first asynchronous call to get the array of results.

```js
import axios from "axios";

const getPosts = async (userId) => {
  const url = `https://jsonplaceholder.typicode.com/posts?userId=${userId}`;
  const response = await axios.get(url);
  const posts = response.data;

  return posts;
}
```

### With Fetch

Fetch needs a second async. call to get the array of results.

```js
const getPosts = async (userId) => {
  const url = `https://jsonplaceholder.typicode.com/posts?userId=${userId}`;
  const response = await fetch(url);
  const posts = await response.json();

  return posts;
}
```

## Managing a Form (basic)

```js
import React, { useEffect, useState } from "react";

// ...

const initialFormValues = {
  title: "",
  description: "",
};

const myForm = (props) => {
  const [formValues, setFormValues] = useState(initialFormValues);
  const { title, description } = formValues;
  // ...

  const handleInputChange = (e) =>
    setFormValues({
      ...formValues,
      [e.target.name]: e.target.value,
    });

  // Handle action functions ...

  return (
    <>
      <h2>Form Title</h2>
      <form>
        <input
          type="text"
          placeholder="Title"
          value={title}
          name="title"
          onChange={handleInputChange}
        />
        <textarea
          type="text"
          placeholder="Description"
          value={description}
          name="description"
          onChange={handleInputChange}
        />
        <button onClick={handleAnActionButton}>An Action</button>
      </form>
    </>
  );
};

export default myForm;
```

## Local Storage

Save data in the Local Storage.

```js
// hardcoded init values if needed
const initialStates = [/* here the hardcoded states if necessary */]
// load state from local storage
const localStates = JSON.parse(localStorage.getItem('states'));

const App = () => {
  const [states, setStates] = useState(localStates || initialStates);

  useEffect(() => {
    setLocalStorage();
  }, [states])

  const setLocalStorage = () => localStorage.setItem('states', JSON.stringify(states));

  // ...

  return (
    // ...
  )
}

export default App
```

### Helper component

Create a folder `/helpers` and inside a file with the helper file, for example `getUser.js`.

That file contain the helper functions to be exported.

```js
const getUser = async () => {
  // ...
};

export default getUser;
```

Or create a library like exporting more than one function like `helpers.js`.

```js
export const getUser = async () => {
	// ...
};

export const getPosts = async (userId) => {
  // ...
}
```

## Handle Input changes

Pass handle function to the onChange event.

```jsx
<input
  type="text"
  name="title"
  value={formValues.title}
  onChange={handleInputChange}
/>
```

This function set the new state and the event object contains the name of the needed property. Using Computed Property Names, it can change the value of the corresponding property.

```js
const handleInputChange = (e) => {
  setFormValues({
    ...formValues,
    [e.target.name]: e.target.value,
  });
};
```

## Add bootstrap

Install the library. 
```bash
npm install bootstrap
```

Additionally you can install an especific version.

```bash
npm install bootstrap@5.1.3
```

### Using a Custom Theme

Sometimes you might need to tweak the visual styles of Bootstrap (or equivalent package).

To enable `scss` in Create React App you will need to install `sass`.

To customize Bootstrap, create a file called `src/custom.scss` (or similar) and import the Bootstrap source stylesheet. Add any overrides before the imported file(s). You can reference [Bootstrap's documentation](https://getbootstrap.com/docs/4.6/getting-started/theming/#variable-defaults) for the names of the available variables.

```bash
npm install sass
```

### Using components with React Bootstrap

Other option is using one of the React bootstrap libraries.

- More info: [React Bootstrap getting started](https://react-bootstrap.github.io/getting-started/introduction/)

## Passing all props to a component

By destucturing the props variable, it can be sent as an attribute to the childs.

```jsx
<Modal {...props} title="New Gallery"> content...</Modal>
```
## Inline styles

Inside a component is possible to assign css styles or classes to an HTML element direct with a JS variable, or even to assign them dinamicaly with boolean states.

```jsx
<img style={{ height: "260px", objectFit: "cover" }} />
<div className={`modal ${ isOpen && 'modal-open' }`}>
```

## Show list elements

With the `map()` function on JS you can show the list of elements and format them as needed.

A list of elements in React needs the `key` attribute with a unique identificator.

```jsx
{
  todos.length === 0
    ? "There are no Tasks!"
    : todos.map((todo) =>
      <Todo
        key={index}
        title={title}
        description={description}
			/>
  )
}
```

## Transform API response

Sometimes is a good recomendation to adapt the response object of the API to our states requirements. It simplifies the work in the app using meaningful names, and also discarding the not needed properties.

```js
const response = await axios.get(url);
const [newQuote] = response.data;
const { quote: text, author } = newQuote; // change "text" for "quote"
```

## Events: call a function with parameters

When you pass a function with a parameter to an event the funciton is triggered in the load of the dom.

To use it correctly it needs to be an arrow function, if not the parameter goes empty.

```js
onClick={ () => todoDelete(id) } // CORRECT
onClick={ todoDelete(id) } // WRONG!!
```

## Stop event in an internal layer

The `stopPropagation()` method of the Event interface prevents propagation of the current event to an html element.

```js
const handleModalDialogClick = (e) => {
  e.stopPropagation();
};
```

```jsx
<div onClick={closeModal}>
  <div onClick={handleModalDialogClick}>
    <h1>Title</h1>
  </div>
</div>
```

## Updater function

Thanks to the new ES6 syntax is possible to change properties on a state passign the property name as a parameter.

```js
const updateProduct = (property, value) =>
  setProduct(prevProduct => {
    ...prevProduct,
    [property]: value // ES6 Computed property names
  });
}
```

## Show conditional elements

With the **AND operator** (`&&`) to show or hide elements:

```jsx
{ errorMessage && `Ops! There is an error: ${errorMessage}` }
```

With the **Ternary operator** to show diferent elements:

```jsx
{ elements.length === 0 ? <ElementsList /> : "no elements" }
```

Both operations are also possible to change properties or classes:

```jsx
<Button variant={state.completed ? "outline-secondary" : "success"} />
```

