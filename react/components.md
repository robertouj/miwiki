---
title: React - Components
description: 
published: true
date: 2022-04-04T17:17:55.515Z
tags: 
editor: markdown
dateCreated: 2022-04-04T17:17:54.296Z
---

# Componets

All related with components in React.

## Creating a Component

This is a basic Functional Arrow Component

```js
import React from 'react'

const App = () => {
  return (
    <div>
      
    </div>
  )
}

export default App
```

The **prerender section** is all the code that precedes the component function and is executed when the file loads, even if the component has not loaded.

Inside the function are the actions that load the render of the DOM with the return.

Using effects it is possible to manage actions after DOM loading or when states change.

## Props Children

`props.children` is available on every component. It contains the content between the opening and closing tags of a component. For example:

```jsx
const Modal = ({ children }) => {
  return (
    <>
      <h1>Title</h1>
      {children}
    </>
  );
};
```

JSX:

```jsx
<Modal>
  <h2>Subtitle<h2>
  <p>Hello world!</p>
</Modal>
```

And it is an array containing all the html elements.

```jsx
const Modal = ({ children }) => {
  return (
    <>
      <h1>Title</h1>
      {children[0]} <!--show Subtitle -->

      <p>Here another element in between.</p>

      {children[1]} <!--show text -->
    </>
  );
};
```

## Fragments

In a render you need to return only one element. A common pattern in React is to return multiple elements. Fragments let you group a list of children without adding extra nodes to the DOM.

```js
return (
  <React.Fragment>
    <ChildA />
    <ChildB />
    <ChildC />
  </React.Fragment>
);

// in a short form
return (
  <>
    <ChildA />
    <ChildB />
    <ChildC />
  </>
);
```