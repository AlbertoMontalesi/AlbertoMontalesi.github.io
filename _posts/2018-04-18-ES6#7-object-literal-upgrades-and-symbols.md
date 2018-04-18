---
title: "JavaScript ES6 for Beginners #7: Object literal upgrades & symbols"
categories:
  - ES6
tags:
  - programming
  - guide
---

![ES6-card-7](https://albertomontalesi.github.io/assets/images/ES6/ES6-card-7.jpg)

In this article we will look at the many upgrades brought by ES6 to the Object literal notation.

## Deconstructing variables into keys and values

This is our initial situation:

``` js
const name = "Alberto";
const surname = "Montalesi";
const age = 25;
const nationality = "Italian";
```

Now if we wanted to create an object literal this is what we would usually do:

```js
const person = {
  name: name,
  surname: surname,
  age: age,
  nationality: nationality,
}
```

In ES6 we can simplify like this:

```js
const person = {
  name,
  surname,
  age,
  nationality,
}
```
As our constant is named the same way as the value we are using we can reduce our typing by a lot.


&nbsp;
## Add functions to our Objects

Let's looks at an example from ES5:

``` js
const person = {
  name: "Alberto",
  greet: function(){
    console.log("Hello");
  },
}

```
If we wanted to add a function to our Object we had to use the the *function* keyword. In ES6 it got easier, look here:

``` js
const person = {
  name: "Alberto",
  greet(){
    console.log("Hello");
  },
}
```

No more *function*, it's shorter and it does the same.

**Remember** that **arrow functions**, look at this example:

``` js
// arrow functions are anonymous, in this case you need to have a key
const person = {
  ()=> console.log("Hello"),
}

const person = {
  greet: ()=> console.log("Hello"),
}
```

&nbsp;
##  Dynamically define properties of an Object

This is how we would dynamically define properties of an Object in ES5:

``` js
var name = "name";
// create empty object
var person = {}
// update the object
person[name] = "Alberto";
console.log(person.name);
// Alberto
``` 

First we created the Object and then we modified it.

In ES6 we can do both things at the same time, look here:

``` js
const name = "name";
const person = {
  [name]:"Alberto",
};
console.log(person.name);

```

&nbsp;

## Symbols

ES6 added a new type of primitive called *Symbols*. What are they? And what do they do?

Symbols are **always unique** and we can use them as identifiers for object properties.

Let's create a Symbol together:

``` js
const me = Symbol("Alberto");
console.log(me);
// Symbol(Alberto)
```

We said that they are always unique, let's try to create a new symbol with the same value and see what happens:

``` js
const me = Symbol("Alberto");
console.log(me);
// Symbol(Alberto)

const clone = Symbol("Alberto");
console.log(clone);
// Symbol(Alberto)

console.log(me == clone);
// false
console.log(me === clone);
// false
```

They both have the same value but we will never have naming collisions with Symbols as they are always unique.

As we mentioned earlier we can use them to create as identifiers for object properties, so let's see an example:

``` js 
const office = {
  "Tom" : "CEO",
  "Mark": "CTO",
  "Mark": "CIO",
}

for (person in office){
  console.log(person);
}
// Tom
// Mark
```
Here we have our office object with 3 people, two of which share the same name, a common situation.
To avoid naming collisions we can use symbols.

``` js
const office = {
  [Symbol("Tom")] : "CEO",
  [Symbol("Mark")] : "CTO",
  [Symbol("Mark")] : "CIO",
}

for(person in office) {
  console.log(person);
}
// undefined
```

We got undefined when we tried to loop over the symbols because they are **not enumerable** so we can't loop over them with a **for...in**.

If we want to retrieve their object properties we can use **Object.getOwnPropertySymbols()**.

``` js
const office = {
  [Symbol("Tom")] : "CEO",
  [Symbol("Mark")] : "CTO",
  [Symbol("Mark")] : "CIO",
}

const symbols = Object.getOwnPropertySymbols(office);
console.log(symbols);
// 0: Symbol(Tom)
​// 1: Symbol(Mark)
​// 2: Symbol(Mark)
​// length: 3
​// __proto__: Array []
```

We retrieved the array but to be able to access the properties we to use **map**.

```js
const symbols = Object.getOwnPropertySymbols(office);
const value = symbols.map(symbol => office[symbol]);
console.log(value);
// 0: "CEO"
​// 1: "CTO"
​// 2: "CIO"
​// length: 3
​// __proto__: Array []
```

Now we finally got the array containing all the values of our symbols.


---
&nbsp;

This was the seventh part of my ES6 for beginners course, check out the rest of them [here](https://albertomontalesi.github.io/courses/es6).

You can also read this articles on medium, on my [profile](https://medium.com/@labby92).

Thank you for reading.