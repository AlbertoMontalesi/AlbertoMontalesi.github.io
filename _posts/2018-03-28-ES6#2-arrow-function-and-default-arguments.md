---
title: "ES6 #2: Arrow functions & default function arguments"
categories:
  - ES6
tags:
  - programming
  - guide
---

## What is an arrow function

ES6 introduced fat arrows (=>) as a way to declare functions. 
This is how we would normally declare a function in ES5:

```
const greeting = (function(name) {

return `hello ${name}`;
})
``` 

The new syntax with a fat arrow looks like this:

``` javascript
const greeting = (name) => {
return `hello ${name}`;
}

```

But we can go further, if we only have one parameter we can drop the parenthesis and write:

``` javascript
const greeting = name => {
return `hello ${name}`;
}
```

And if we have no parameter at all we need to write empty parenthesis like this:

``` javascript
const greeting = () => {
return "hello";
}

```


### Implicitly return

With arrow functions we can skip the explicit return and return like this:

``` javascript
const greeting = (name) => `hello ${name}` ;
}

```

Let's say we want to implicitly return an **object literal**, we would do like this:

``` javascript
const race = "100m dash";
const runners = [ "Usain Bolt", "Justin Gatlin", "Asada Powell" ] ;

const winner = runners.map(( runner, i) =>  ({ name: runner, race, place: I +1})));

```

To tell JavaScript that what's inside the curly braces is an object literal that we want to implicitly return we need to wrap everything inside parenthesis.

Writing race or race:race is the same.

### Arrow functions are anonymous

As you can see from the previous examples, arrow functions are **anonymous**.

If we want to have a name to reference them we can bind them to a variable:

``` javascript
const greeting = (name) => `hello ${name}`;

greeting("Tom");

```

## Arrow function and the **this** keyword

You need to be careful when using arrow functions in conjunction with the this keyword as they behave differently from normal functions.

When you use an arrow function, the this keyword is inherited from the parent scope.
