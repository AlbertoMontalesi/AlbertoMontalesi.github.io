---
title: "JavaScript ES6 for Beginners #1: Var vs Let vs Const & the temporal dead zone"
categories:
  - ES6
tags:
  - programming
  - guide
---

![ES6-card-1](https://albertomontalesi.github.io/assets/images/ES6/ES6-card-1.jpg)

With the introduction of **Let** and **Const** in **ES6** we can know better define our variable depending on our needs. Let's have a look at the major differences between them.

&nbsp;

## Var

**Var** are **function scoped**, which means that if we declare them inside a **for loop** (which is a **block** scope) they will be available globally.

``` javascript 
for (var i = 0; i < 10; i++) {
  var global = "I am available globally";
}

console.log(global);

// expected output: I am available globally
```
&nbsp;
## Let 

**Let** (and **const**) are **block scoped** meaning that they will be available only inside of the block where they are declared and its sub-blocks.

``` javascript
let x = "global";

if (x === "global") {
  let x = "block-scoped";

  console.log(x);
  // expected output: block-scoped
}

console.log(x);
// expected output: global
```

&nbsp;
## Const

Similarly to **let**, **const** are **block-scoped** but they differ in the fact that their value **can't change through re-assignment or can't be  redeclared**.


``` javascript
const constant = 'I am a constant';

constant = " I can't be reassigned";

// it will raise: Uncaught TypeError: Assignment
// to constant variable
```


**Important** 
This **does not** mean that **const are immutable**.

###  The content of a Const is an Object

``` javascript
const person = {
  name: 'Alberto',
  age: 25,
}

person.age = 26;

// in this case no error will be raised, we are not
// re-assigning the variable but just 
// one of its properties.
``` 

---
&nbsp;
## The temporal dead zone

According to **MDN** the definition of the temporal dead zone is:

> In ECMAScript 2015, let bindings are not subject to **Variable Hoisting**, which means that let declarations do not move to the top of the current execution context. Referencing the variable in the block before the initialization results in a ReferenceError (contrary to a variable declared with var, which will just have the undefined value). The variable is in a “temporal dead zone” from the start of the block until the initialization is processed.

Let's look at an example:

```javascript
console.log(i);
var i = "I am a variable";

//  expected output: undefined

console.log(j);
let j = "I am a let";

// expected output: ReferenceError: can't access 
// lexical declaration `j' before initialization
```

**Var** can be accessed **before** they are defined, but we can't access their **value**.
**Let** and **Const** can't be accessed **before we define them**.

This happens because **var** are subject to **hoisting** which means that they are processed before any code is executed. Declaring a **var** anywhere is equivalent to **declaring it at the top**. This is why we can still access the **var** but we can't yet see its content, hence the **undefined** result.


---
&nbsp;

## When to use Var, Let and Const

There is no rule stating where to use each of them and people have different opinions. Here I am going to present to you two opinions from popular developers in the JavaScript community.

The first opinion comes from [Mathias Bynes:](https://mathiasbynens.be/notes/es6-const)


- use **const** by default
- use **let** only if rebinding is needed.
- **var** should never be used in ES6.


The second opinion comes from [Kyle Simpson:]( blog.getify.com/constantly-confusing-const/)

- Use **var** for top-level variables that are shared across many (especially larger) scopes.
- Use **let** for localized variables in smaller scopes.
- Refactor **let** to **const** only after some code has to be written, and you're reasonably sure that you've got a case where there shouldn't be variable reassignment.

Which opinion to follow is entirely up to you. As always, do your own research and figure out which one you think is the best.

You may want to [read this article](https://medium.com/@sbakkila/javascript-es-6-let-and-the-dreaded-temporal-dead-zone-85b89314d168) to understand how **let** affects your performances compared to **var** before you choose to follow either [Mathias Bynes](https://mathiasbynens.be/notes/es6-const) or [Kyle Simpson]( blog.getify.com/constantly-confusing-const/).



---

&nbsp;

This was the first part of my ES6 for beginners course, check out the rest of them [here](https://albertomontalesi.github.io/courses/es6).

You can also read this articles on medium, on my [profile](https://medium.com/@labby92).

Thank you for reading.