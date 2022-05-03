---
title: Basics TypeScript
description: 
published: true
date: 2022-05-03T17:42:27.431Z
tags: 
editor: markdown
dateCreated: 2022-05-03T17:42:27.431Z
---

# Basics TypeScript

## Core Types

These are the basic types accepted by TypeScript:

- `number`: 1, 5.3, -10
- `string`: 'Hi', "Hi", \`Hi\`
- `boolean`: true, false
- `object` : {age: 30}
- `Array`: [1, 2, 3]
- `Tuple`: [1, 2]
- `Enum`: enum { NEW, OLD }
- `Any`: *
- And any other JavaScript types: `undefined`, `null`, etc.

## Assign of types

### Explicit assignment

The assignment can be **explicit** when whe defin the type in a declaration.

```TypeScript
// with a variable
const age: number:

// in the parameters of a function
function add(person: { n1: number, n2: number, showResult: boolean }) {
  // ...
}

// even in the properties of an object
function greet(person: { name: string, age: number }) {
  return "Hello " + person.name;
}

// or with objects
const person: {
  name: string;
  age: number;
} = {
  name: 'Maximilian',
  age: 30
};
```

### Type Inference

Or can be implicit by **inference** when js assign directly the type depending of the values.

```TypeScript
let x = 3; // let x: number
let x = [0, 1, null]; // let x: (number | null)[]
let zoo = [new Rhino(), new Elephant(), new Snake()]; // let zoo: (Rhino | Elephant | Snake)[]

let number; // let x: any
number = '5'; // ts allows any type here
```

When there is a mix of numbers and strings it is converted to a string.

```TypeScript
let x = 3; // let x: number
let y = 5// let y: number

let text = 'The number is: ' + x + y; // let text: string
// resulting the string "The number is 35"
```

## Object Types

```TypeScript
const person: { name: string, age: number } = { name: "Mathew", age: 36 };
```

ref: <https://www.typescriptlang.org/docs/handbook/2/objects.html>

## Array Types

This type can be **flexible** or **strict**, regarding the element types. The type string is asigned with `[]` at the end.

```TypeScript
// strict
const hobbies: string[] = ['Music', 'Films'];

// flexible with any
const myArray: any[] = ['Music', 4];
```

### Tuple Types

A tuple type is another sort of Array type that knows exactly how many elements it contains, and exactly which types it contains at specific positions.

```TypeScript
const stringNumberPair: [string, number] = ['High', 5];
```

## Enum Types

A enum type give an enumerated list of flobal constant identifiers. The constants in the enums are assigned to number consecutively or you can assign them as needed to numbers, strings, etc.

```TypeScript
enum Role { ADMIN, READ_ONLY, AUTHOR };
const role: Role = Role.AUTHOR; // it receives the number 0

enum Role { ADMIN = 10, READ_ONLY = 20, AUTHOR = 30 };
const role: Role = Role.AUTHOR; // it receives the number 10
```

## Any Type

It is a no specific type assignment, can be any kind of value.

| :warning: WARNING          |
|:---------------------------|
| Any takes away all advantages of TypeScript, because of that better to avoid it whenever possible.

So you can use any as a fallback if you have some value or some kind of data where you really can't know which kind of data will be stored in there and where you then maybe are using some runtime checks.

```TypeScript
let favoriteActivities: any[] =  [null, 'Hi', 3.5];
```

## Union Types

It combines different kind of types and the variable can be each of them.

That results in a needed runtime check to avoid TS errors when it is assigned. It is possible combinations with the `typeof` operator.

```TypeScript
function combine(
  input1: number | string,
  input2: number | string,
) {
  let result;
  if (typeof input1 === 'number' && typeof input2 === 'number') {
    result = input1 + input2;
  } else {
    result = `${input1.toString()} ${input2.toString()}`;
  }
  return result;
}
```

## Literal Types

In addition to the general types string and number, we can refer to specific strings and numbers in type positions.

It only make sense when combines with Union Types, it can express a much more useful concept.

```TypeScript
const resultConversion: "as-number" | "as-string":
```

## Type Aliases or Custom Types (feature)

It’s common to want to use the same type more than once and refer to it by a single name.

A type **alias** or **custom type** is a name for any type. Start with `Type` and continue with the `Name` And also it can be combine with unions or define objects.

```TypeScript
//  name a union type
type ID = number | string;

// or an object type
type Point = {
  x: number | string;
  y: number | string;
};
 
// the type is assigned
function printCoord(pt: Point) {
  console.log("The coordinate's x value is " + pt.x);
  console.log("The coordinate's y value is " + pt.y);
}
```

## Function Return Types & "void"

### Return: Types

The returned value of the function can be defined or infered. It is possible with the `:` sign and the type between the parameters and the curly braces.

```TypeScript
function add(n1: number, n2: number): number { // return: number
  return  n1 + n2;
}
```

### Return: void

It means that the function returns nothing. But JavaScript actually returns undefined.

`undefined` is not allowed as returned type in TS, instead of that it uses `void`.

```TypeScript
function printResult(num: number) { // return: void (inferred)
  console.log(`Result:  ${num}`);
}

console.log(printResult(add(5, 12))); // void return: undefined
```

## Function Types

Function types allow to describe which type of function will be used somewhere. It match the number of arguments and their types, also what it returns.

Type Funtions has the `Function` type and can be assigned with an arrow function with the parameters in the left and the returned value right to the arrow.

```TypeScript
const combinedValues: (a: number, b: number) => number; 
// Function Types: 2 arguments type number and return a number
```

### Callbacks

Define a callback function that receive the result of the previous operation

```TypeScript
// 
function addAndHandle(n1: number, n2: number, cb: (a: number) => void) { 
  let result = n1 + n2;
  cb(result); // callback function will handle the result
}
```

## The "unknown" Type

This admit any kind of type, but that need to be ckecked before assign.

```TypeScript
let userInput: unknown;
let userName: string;

userInput = 5;
userInput = 'Roberto';

userName = userInput; // ERROR: because it need to be validated
```

## The "never" Type

Advice that the fucntion never return. The script ends.

```TypeScript
function generateError(message: string, code: number): never { // indication of never return
  throw { message, errorCode: code }; // most common use
  // while (true) {} // another case that never return
}

generateError('An error occurred!', 500); // never return
console.log('This message never will neve be displayed!'); // never executed
```