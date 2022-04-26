---
title: React - Do's and Dont's
description: 
published: true
date: 2022-04-06T09:56:17.438Z
tags: 
editor: markdown
dateCreated: 2022-04-06T09:06:16.262Z
---

# React Do's & Don'ts

Some good practises about react.

## Naming event handling

By convention, for Event Handler Functions & Props in React should be followed the same structure as in the HTML events handling: `onClick`, `onSubmit`, `onChange`, etc.

### Naming handler funtions

It follows the cause and effect flow, so that it proceeds the event by adopting the `handle` prefix. Therefor, the naming convention becomes `handleSubjectEvent` where `Subject` is the thing the handler is focused on and `Event` is the event taking place.

**Convention:** `handleEvent`, `handleSubjectEvent`

**Examples:** `handleNameChange`, `handleChange`, `handleFormReset`, `handleReset`

```js
const todoAddHandler = (text: string) => {
  setTodos(prevTodos => [...prevTodos, { id: Math.random().toString(), text: text }]);
};
```

### Naming the Props

When creating a React component which has a prop that handles something, simply follow the `onEvent` convention (adding a `Subject` if applicable).

**Convention:** `onEvent`, `onSubjectEvent`

**Examples:** `onNameChange`, `onChange`, `onFormReset`, `onReset`

Passing the props to a component:

```jsx
<NewTodo onAddTodo={todoAddHandler} />
```

Handling an HTML event in a component and calling the action from the props.

```jsx
const todoSubmitHandler = (event) => {
  // other actions...
  onAddTodo(enteredText);
};

// In JSX
<form onSubmit={todoSubmitHandler}>
```
