---
title: Advanced Types
description: 
published: true
date: 2022-05-03T17:44:30.917Z
tags: 
editor: markdown
dateCreated: 2022-05-03T17:44:30.917Z
---

# Advanced Types

## Intersection Types

```TypeScript
type Admin = {
  name: string;
  privilieges: string[];
};

type Employee = {
  name: string;
  startDate: Date;
};

type ElevatedEmployee = Admin & Employee;
```

## Type Guards

Sometimes the union types modeling can overlap in the types they can take on.

Here is needed to diferenciate with some technics.

- in operator
  This check if the property exist in an object.
  if ("somePropertie" in someUnionType) { // do something ... }

- instanceof operator
  With classes exist this operator to check the type of the instantiated bject.

```TypeScript
type Admin = {
  name: string;
  privilieges: string[];
};

type Employee = {
  name: string;
  startDate: Date;
};

type ElevatedEmployee = Admin & Employee;

const e1: ElevatedEmployee = {
  name: 'Max',
  privileges: ['create-server'],
  startDate: new Date()
}
```

## Discriminated Unions

It is a pattern that can be used with union tpes that makes implementing type guards easier. The form is creating a literal type property referencing the interface.

```TypeScript
interface Bird {
  type: 'bird';
  flyingSpeed: number;
}

interface Horse {
  type: 'horse';
  runningSpeed: number;
}

type Animal = Bird | Horse;

function moveAnimal(animal: Animal) {
  let kindOfSpeed;
  switch (animal.type) {
    case 'bird':
      kindOfSpeed = animal.flyingSpeed;
      break;
    case 'horse':
      kindOfSpeed = animal.runningSpeed;
      break;
  }
  console.log(`Moving at speed: ${kindOfSpeed}`);
}
```

## Type Casting

Help to tell TypeScript that some value is of a specific type where TypeScript is not able to detect it on its own.

- Syntax 1: with `<someType>`
  `<someType>sombeObject;`

- Syntax 2: with `as` and `someType`
  `sombeObject as someType;`

with the `!` prevent that the object could be null and the subsequent ts error.

It is another form in which is no necessary to validate.

```TypeScript
let userInputElement = <HTMLInputElement>document.getElementById('user-input')!;
// or
let userInputElement = 
  document.getElementById('user-input')! as HTMLInputElement;
}

userInputElement.value = 'Hi there!';
```

## Index Properties

It is a feature that allows to create objects with more flexible properties.

```TypeScript
interface errorContainer {
  [prop: string]: string; // is possible to create undefined number of properties                          
}                         // with the key matching with a string and string values

const errorBag: errorContainer = {
  email: 'Not a valid email',
  username: 'Name can\'t be empty'
}
```

## Generic Type

Is a type which is kind of connected with some other type and is flexible regarding which exact type that other type is.

- Syntasx: `Array<T>` / `Array<T, U>` // returns the intersection T&U

```TypeScript
function merge<T, U>(objA: T, objB: U) {
  return Object.assign(objA, objB);
}

const mergedObj = merge({ name: 'Max', hobbies: ['Sports'] }, {age: 38});
console.log(`Name: ${mergedObj.name} - Age: ${mergedObj.age}`);
```

## Generic Constraints

Is possible to restrict the types of the generic types (`<T>`) can be based on, with the "extends" keyword.

- Syntax: `<T extends object>`

```TypeScript
function merge<T extends object, U extends object>(objA: T, objB: U) {
  return Object.assign(objA, objB);
}

// here we have a silent error, because 30 is not an object
// const mergedObj = merge({ name: 'Max', hobbies: ['Sports'] }, 30); 
const mergedObj = merge({ name: 'Max', hobbies: ['Sports'] }, { Age: 30 });
console.log(mergedObj); 
```

### Other Generic Type Functions

Is possible to create more specific generics to accept different types with specific properties.

```TypeScript
interface Lengthy {
  length: number;
}

// with that is no necessary to create overloads or large union types
function countAndPrint<T extends Lengthy>(element: T): [T, string] {
  let descriptionText = 'Got no value.';
  if (element.length === 1) {
    descriptionText = `Got 1 elements.`;
  } else if (element.length > 1) {
    descriptionText = `Got ${element.length} elements.`;
  }
  return [element, descriptionText]
}
```

## The "keyof" Constraint

Create a reference to a key of an object.

```TypeScript
function extractAndConvert<T extends object, U extends keyof T>(
  obj: T,
  key: U
) {
  return `Value: ${obj[key]}`;
}

console.log(extractAndConvert({name: 'Max'}, 'name'));
}
```

## Utilities

- Partial, Readonly...

More: <https://www.typescriptlang.org/docs/handbook/utility-types.html>

```TypeScript
const names: Readonly<string[]> = ['Max', 'Anna'];
// names.push('Manu'); // ERROR
// names.pop();

 interface CourseGoal {
  title: string;
  description: string;
  completeUntil: Date;
}

function createCourseGoal(
  title: string,
  description: string,
  date: Date
): CourseGoal {
  let courseGoal: Partial<CourseGoal> = {}; // it's empty and doesn't complain
  courseGoal.title = title;
  courseGoal.description = description;
  courseGoal.completeUntil = date;
  return courseGoal as CourseGoal;
}
```
