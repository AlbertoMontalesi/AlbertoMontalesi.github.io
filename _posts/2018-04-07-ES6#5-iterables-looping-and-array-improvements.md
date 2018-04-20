---
title: "JavaScript ES6 for Beginners #5: Iterables, Looping and Array improvements"
categories:
  - ES6
tags:
  - programming
  - guide
---



![ES6-card-5](https://albertomontalesi.github.io/assets/images/ES6/ES6-card-5.jpg)


ES6 introduced a new type of loop, the `for of` loop.

&nbsp;

## The `for of` loop

### Iterating over an array

Usually we would iterate using something like this:

``` js
var fruits = ['apple','banana','orange'];
for (var i = 0; i < fruits.length; i++){
  console.log(fruits[i]);
}
// apple
// banana
// orange
```

Look at how we can achieve the same with a `for of` loop:

``` js
const fruits = ['apple','banana','orange'];
for(const fruit of fruits){
  console.log(fruit);
}
// apple
// banana
// orange
```

### Iterating over an object

Objects are **non iterable** so how do we iterate over them?
We have to first grab all the values of the object using something like `Object.keys()` or the new ES6 `Object.entries()` (more on that in a later article).


```js
const car = {
  maker: "BMW",
  color: "red",
  year : "2010",
}
for (const prop of Object.keys(car)){
  const value = car[prop];
  console.log(value,prop);
}
// BMW maker
// red color
// 2010 year
```

&nbsp;


## The `for in` loop

Even though it is not a new ES6 loop, let's look at the `for in` loop to understand what differentiate it compared to the `for of. 

The `for in` loop is a bit different because it will iterate over all the [enumerable properties](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Enumerability_and_ownership_of_properties) of an object in no particular order.

It is therefore suggested not to add, modify or delete properties of the object during the iteration as there is no guarantee that they will be visited, or if they will be visited before or after being modified. 


```js
const car = {
  maker: "BMW",
  color: "red",
  year : "2010",
}
for (const prop in car){
  console.log(prop);
}
// maker
// color
//  year
```

&nbsp;

## Difference between `for of` and `for in`

The first difference we can see is by looking at this example:

```js
let list = [4, 5, 6];

// for...in returns a list of keys
for (let i in list) {
   console.log(i); // "0", "1", "2",
}


// for ...of returns the values 
for (let i of list) {
   console.log(i); // "4", "5", "6"
}

```

`for in` will return a list of keys whereas the `for of` will return a list of values of the numeric properties of the object being iterated.


Another differences is that we **can** stop a `for of` loop but we can't do the same with a `for in` loop.

```js
const digits = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9];

for (const digit of digits) {
  if (digit % 2 === 0) {
    continue;
  }
  console.log(digit);
}
// 1 3 5 7 9
```

The last important difference I want to talk is that the `for in` loop will iterate over new properties added to the object.

```js
const fruit = ["apple","banana", "orange"];

fruit.eat = "gnam gnam";

for (const prop of fruit){
  console.log(fruit);
}
// apple
// banana
// orange

for (const prop in fruit){
  console.log(fruit[prop]);
}

// apple
// banana
// orange
// gnam gnam

```

&nbsp;

## Array improvements

### `Array.from()`

`Array.from()` is the first of the many new array methods that ES6 introduced.

It will take something **arrayish**, meaning something that looks like an array but it isn't, and transform it into a real array.

``` js
<div class="fruits">
  <p> Apple </p>
  <p> Banana </p>
  <p> Orange <p>
</div>
```

``` js
const fruits = document.querySelectorAll(".fruits p");
const fruitArray = Array.from(fruits);

console.log(fruits);
//it will return us an array containing 3 p tags [p,p,p];

//since now we are dealing with an array we can use map
const fruitNames = fruitArray.map( fruit => fruit.textContent);

console.log(fruitNames);
// ["Apple", "Banana", "Orange"]
```

We can also simplify like this:

```js
const fruits = Array.from(document.querySelectorAll(".fruits p"));
const fruitNames = fruits.map(fruit => fruit.textContent);

console.log(fruitNames);
// ["Apple", "Banana", "Orange"]
```

Now we transformed **fruits** into a real array, meaning that we can use any sort of method such as `map` on it.

`Array.from()` also takes a second argument, a `map` function so we can write:

``` js
const fruits = document.querySelectorAll(".fruits p");
const fruitArray = Array.from(fruits, fruit => {
  console.log(fruit);
  // <p> Apple </p>
  // <p> Banana </p>
  // <p> Orange </p>
  return fruit.textContent;
  // we only want to grab the content not the whole tag
});
console.log(fruitArray);
// ["Apple", "Banana", "Orange"]
```

&nbsp;

### `Array.of()`

`Array.of()` will create an array with all the arguments we pass into it.


```js
const digits = Array.of(1,2,3,4,5);
console.log(digits);

// Array [ 1, 2, 3, 4, 5];
```


&nbsp;

### `Array.find()`

`Array.find()` returns the value of the first element in the array that satisfies the provided testing function. Otherwise `undefined` is returned.

It can be useful in instances where we have a json file, maybe coming from an API from instagram or something similar and we want to grab a specific post with a specific code that identifies it.

Let's looks at a simple example to see how `Array.find()` works.

``` js
const array = [1,2,3,4,5];

let found = array.find( e => e > 3 );
console.log(found);
// 4
```

As we mentioned, it will return the **first element** that matches our condition, that's why we only got **4** and not **5**.

&nbsp;

### `Array.findIndex()`

`Array.findIndex()` will return the *index* of the element that matches our condition.

``` js
const greetings = ["hello","hi","byebye","goodbye","hi"];

let foundIndex = greetings.findIndex(e => e === "hi");
console.log(foundIndex);
// 1
```

Again, only the index of the **first element** that matches our condition is returned.

&nbsp;

### `Array.some()` & `Array.every()`

I'm grouping these two together because their use is self-explanatory: `.some()` will search if there are some items matching the condition and
stop once it finds the first one, `.every()` will check that all items match the given condition.

```js
const array = [1,2,3,4,5,6,1,2,3,1];

let arraySome = array.some( e => e > 2);
console.log(arraySome);
// true

let arrayEvery = array.every(e => e > 2);
console.log(arrayEvery);
// false 
```

Simply put, the first condition is true, because there are **some** elements greater than 2, but the second is false because **not every element** is greater than 2.


---

&nbsp;

This was the fifth part of my ES6 for beginners course, check out the rest of them [here](https://albertomontalesi.github.io/courses/es6).

You can also read this articles on medium, on my [profile](https://medium.com/@labby92).

Thank you for reading.