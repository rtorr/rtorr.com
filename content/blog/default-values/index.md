---
title: "Default values in JavaScript"
date: "2019-12-29"
description: "How I think about default values in JavaScript"
---

# How I think about default values in JavaScript

First of all, all these things can fall under the Opinion and Concern
umbrella. The most important thing is just giving thought to the things
you have opinions about and always reserve the right to be corrected.

My simple rule of thumb is to try to set initial state to whatever the
eventual state will be for Objects and Arrays.

Strings and numbers default to undefined.

## Describing usage

### Problems defaulting to undefined:

A lot of times I am just trying to describe how state will be used,
so setting values that will be used later as `undefined` will give
future users some understanding of what state might exist

```javascript
// bad
const initialState = {
  // type string
  name: undefined,
  // type number
  age: undefined,
  // type array of strings
  cars: undefined,
  // type deep object {height: string, shoe_size: number}
  metaData: undefined,
}
// initialState.cars.map()
// > TypeError: initialState.cars is undefined
// console.log(initialState.metaData.test)
// > TypeError: initialState.metaData is undefined
```

Defaulting to `undefined` has been a safer choice overall in my experience,
because other authors tend to not set object properties befefore usage, or
they might just not exist on some JSON you get back from a server

### Problems defaulting to null:

any time you want to use `typeof` you will need to check for two values.
This is super error prone.
`typeof initialState.name !== "object" && typeof initialState.name === "string"`

```javascript
// Bad
const initialState = {
  name: null,
  age: null,
  cars: null,
  metaData: null,
}
// typeof initialState.name
// > "object"
// initialState.cars.map()
// > TypeError: initialState.cars is null
// console.log(initialState.metaData.test)
// > TypeError: initialState.metaData is null
```

### Problems defaulting to the values type

```javascript
const initialState = {
  age: 0, // is 0 a valid age?,
  name: "", // will someone typeof === 'string' and also have to check length?
}
```

### Preference

My preference, which has in my experience been less error prone.
The only time I will use null as a default is if some API I am using uses null.

```javascript
const initialState = {
  age: undefined,
  name: undefined,
  cars: [],
  metaData: { height: undefined, shoe_size: undefined },
}
```
