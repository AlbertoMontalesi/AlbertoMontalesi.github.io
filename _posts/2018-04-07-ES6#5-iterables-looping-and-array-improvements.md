---
title: "ES6 for Beginners #5: Iterables, Looping and Array improvements"
categories:
  - ES6
tags:
  - programming
  - guide
---

ES6 introduced new ways to create loops. We will start by looking at the **for of** loop.

&nbsp;

### The **for of** loop

#### Iterating over an array

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

Look at how we can achieve the same with a **for of** loop:

``` js
const fruits = ['apple','banana','orange'];
for(const fruit of fruits){
  console.log(fruit);
}
// apple
// banana
// orange
```

#### Iterating over an object

Objects are **non interable** so how do we iterate over them?
We have to first grab all the values of the object using something like **Object.keys()** or the new ES6 **Object.entries()** (more on that in a later article).


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





### The for in loop

remember to talk about how it loops over the prototype's properties


```js

example goes here
```


### Difference between for...of and for...in




## Array improvements

### Array.from()

Array.from() is the first of the many new array methods that ES6 introuced.

