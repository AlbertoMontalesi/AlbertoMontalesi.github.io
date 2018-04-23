---
title: "JavaScript ES6 for Beginners #12: Sets, WeakSets, Maps and WeakMaps"
categories:
  - ES6
tags:
  - programming
  - guide
---

![ES6-card-12](https://albertomontalesi.github.io/assets/images/ES6/ES6-card-12.jpg)


## What is a `Set`?

A `Set` is an object where we can store **unique values** of any type.

```js
// create our set
const family = new Set();

// add values to it
family.add("Dad");
console.log(family);
// Set [ "Dad" ]

family.add("Mom");
console.log(family);
// Set [ "Dad", "Mom" ]

family.add("Son");
console.log(family);
// Set [ "Dad", "Mom", "Son" ]

family.add("Dad");
console.log(family);
// Set [ "Dad", "Mom", "Son" ]
```

As you can see, at the end we tried to add "Dad" again but the `Set` still remained the same because a `Set` can only take **unique values**.

Let's continue using the same `Set` and see what methd we can use.

``` js
family.size;
// 3
family.keys();
// SetIterator {"Dad", "Mom", "Son"}
family.entries();
// SetIterator {"Dad", "Mom", "Son"}
family.values();
// SetIterator {"Dad", "Mom", "Son"}
family.delete("Dad");
// true
family;
// Set [ "Mom", "Son" ]
family.clear;
family;
// Set []
```

As you can see a `Set` has a `size` property and we can `delete` an item from it or use `clear` to delete all the items from it.

We can also notice that a `Set` does not have keys so when we call `.keys()` we get the same as calling `.values()` or `.entries()`.


### Loop over a `Set`

We have two ways of iterating over a `Set`: using `.next()` or using a `for of` loop.

``` js
// using `.next()`
const iterator = family.values();
iterator.next();
// Object { value: "Dad", done: false }
iterator.next();
// Object { value: "Mom", done: false }


// using a `for of` loop
for(const person of family) {
  console.log(person);
}
// Dad
// Mom
// Son
```

&nbsp;

## What is a `WeakSet`?

A `WeakSet` is similar to a `Set` but it can **only** contain Objects.

``` js
let dad = {name: "Daddy", age: 50};
let mom = {name: "Mummy", age: 45};

const family = new WeakSet([dad,mom]);

for(const person of family){
  console.log(person);
}
// TypeError: family is not iterable
```

We created our new `WeakSet` but when we tried to use a `for of` loop it did not work, we can't iterate over a `WeakSet`.

Another big difference that we can see is by trying to use `.clear` on a `WeakSet`: nothing will happen because a `WeakSet` cleans itself up after we delete an element from it.

```js
dad = null;

// wait a few seconds


//example of garbage collectionnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnn

```

&nbsp;

## What is a `Map`?


&nbsp;

## What is a `WeakMap`?


---
&nbsp;

This was the tenth part of my ES6 for beginners course, check out the rest of them [here](https://albertomontalesi.github.io/courses/es6).

You can also read this articles on medium, on my [profile](https://medium.com/@labby92).

Thank you for reading.