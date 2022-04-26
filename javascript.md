---
title: JavaScript
description: 
published: true
date: 2022-04-05T11:27:45.789Z
tags: 
editor: markdown
dateCreated: 2022-04-04T20:03:02.008Z
---

# JavaScript

## Timing Events

### setTimeout

Executes a function, after waiting a specified number of milliseconds.

```js
setTimeout(function, milliseconds)
```

### setInterval

Repeats the execution of the function continuously each time interval.

```js
setInterval(function, milliseconds)
```

## Spreading to update properties

Edit properties of an object with spreading.

```js
{ ...object, propertyToEdit: 'newValue' }
```

## Spreading to insert in Array 

The previous state can be inserted as needed.

```js
[...array, value1, value2] // beginning
[value1, ...array, value2] // middle
[value1, value2, ...array] // end
```

## Trigger function in events

When you pass a function with a parameter to an event the funciton is triggered in the load of the dom.

To use it correctly it needs to be an arrow function, if not the parameter goes empty.

```js
onClick={ () => todoDelete(id) } // CORRECT
onClick={ todoDelete(id) } // WRONG!!
```

## Stop event propagation

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

## Generate aleatory numbers

This example get a random number between two values.

The maximum is exclusive and the minimum is inclusive.

```js
function getRandomInt(min, max) {
  min = Math.ceil(min);
  max = Math.floor(max);
  return Math.floor(Math.random() * (max - min) + min); 
}
```

## Template literals ES6

Operators inside a string

```js
`Task ${ !todoEdit ? 'added' : 'edited' } successfuly`
```

Multiline

```js
`string text line 1
string text line 2`
```

- <https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Template_literals>

## Computed Property Names (ES6)

It is possible to assing a name of a property with the value of a variable using brackets.
Is also possible to change the name of a property using destructuring + computed property names

```js
const handleInputChange = (e) => setFormValues({
  ...formValues,
  [e.target.name]: e.target.value 
  // e.target.name is a string used as a property name.
});
```

- <https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Object_initializer#computed_property_names>
- <https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment#computed_object_property_names_and_destructuring>

## Callback function

This is an example of creation of a function with a callback function. The result is the same as the tool map on JavaScript.

```js
const myMap = (array, callback ) => {
  let newArray = [];
  for ( element of array ) newArray.push(callback(element))
  return newArray;
}

const myArray = [1,3,5,7];
console.log(myMap(myArray, element => element+1)); // (4) [2, 4, 6, 8]

```
