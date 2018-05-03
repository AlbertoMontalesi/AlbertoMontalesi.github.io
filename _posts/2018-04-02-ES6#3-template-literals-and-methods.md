---
title: "JavaScript ES6 for Beginners #3: Template literals & additional string methods"
categories:
  - JavaScript
tags:
  - ES6
  - programming
  - guide
---


![ES6-card-3](https://albertomontalesi.github.io/assets/images/ES6/ES6-card-3.jpg)

Prior to ES6 they were called *template strings*, now we call them  *template literals*. Let's have a look at what changed in the way we interpolate strings in ES6.

&nbsp;

## Interpolating strings

In ES5 we used to write this, in order to interpolate strings:

``` javascript
var name = "Alberto";
var greeting = 'Hello my name is ' + name;

console.log(greeting);
// Hello my name is Alberto
```

In ES6 we can use backticks to make our life easier.

``` javascript
let name  = "Alberto";
const greeting = `Hello my name is ${name}`;

console.log(greeting);
// Hello my name is Alberto
```

&nbsp;

## Expression interpolations

In ES5 we used to write this:

``` javascript
var a = 1;
var b = 10;
console.log('1 * 10 is ' + ( a * b));
// 1 * 10 is 10

```

In ES6 we can use backticks to reduce our typing:

``` javascript
var a = 1;
var b = 10;
console.log(`1 * 10 is ${a * b}`);
// 1 * 10 is 10
```

&nbsp;

## Create HTML fragments

In ES5 we used to do this to write multi-line strings:

``` javascript
// We have to include a backslash on each line
var text = "hello, \
my name is Alberto \
how are you?\ "
```

In ES6 we simply have to wrap everything inside backticks, no more backslashes on each line.

``` javascript 
const content = `hello,
my name is Alberto
how are you?`;
```

&nbsp;

## Nesting templates

It's very easy to nest a template inside another one, like this:

``` js
const markup = `
<ul>
  ${people.map(person => `<li>  ${person.name}</li>`)}
</ul>
`;
```

&nbsp;

## Add a ternary operator

We can easily add some logic inside our template string by using a ternary operator:

``` js
// create an artist with name and age
const artist = {
  name: "Bon Jovi",
  age: 56,
};

// only if the artist object has a song property we then add it to our paragraph, otherwise we return nothing
const text = `
  <div>
    <p>  ${artist.name} is ${artist.age} years old ${artist.song ? `and wrote the song ${artist.song}` : '' }
    </p>
  </div>
`
```

&nbsp;

## Pass a function inside a template literal

Similarly to the example above, if we want to, we can pass a function inside a template literal.

``` js
const groceries = {
  meat: "pork chop",
  veggie: "salad",
  fruit: "apple",
  others: ['mushrooms', 'instant noodles', 'instant soup'],
}

// this function will map each individual value of our groceries
function groceryList(others) {
  return `
    <p> 
      ${others.map( other => ` <span> ${other}</span>`).join(' ')}
    </p>
  `;
}

// display all our groceries in a p tag, the last one will include all the one from the array **others**
const markup = `
  <div>
    <p> ${groceries.meat} </p>
    <p> ${groceries.veggie} </p>
    <p> ${groceries.fruit} </p>
    <p>${groceryList(groceries.others)} </p>
  <div>
`
```

&nbsp;


## Tagged template literals

By tagging a function to a template literal we can run the template literal through the function, providing it with everything that's inside of the template.

The way it works is very simple: you just take the name of your function and put it in front of the template that you want to run it against.


 ```js
let person = "Alberto";
let age = 25;

function myTag(strings,personName,personAge){
  let str = strings[1];
  let ageStr;

  personAge > 50 ? ageStr = "grandpa" : ageStr = "youngster";

  return personName + str + ageStr;
}

let sentence = myTag`${person} is a ${age}`;
console.log(sentence);
// Alberto is a youngster
```

We captured the value of the variable age and used a ternary operator to decide what to print.
`strings` will take all the strings of our `let` sentence whilst the other parameters will hold the variables.


&nbsp;

To learn more about use cases of *template literals* check out [this article](https://codeburst.io/javascript-es6-tagged-template-literals-a45c26e54761).

&nbsp;
&nbsp; 

## Additional string methods

We are going to cover 4 new strings method:

- `startsWith()`
- `endsWith()`
- `includes()`
- `repeat()`

&nbsp;

### `startsWith()`

This new method will check if the string starts with the value we pass in:

```js
const code = "ABCDEFG";

code.startsWith("ABB");
// false
code.startsWith("abc");
// false, startsWith is case sensitive
code.startsWith("ABC");
// true
```

We can pass an additional parameter, which is the starting point where the method will begin checking.


``` js
const code = "ABCDEFGHI"

code.startsWith("DEF",3);
// true, it will begin checking after 3 characters
```

&nbsp;

### `endsWith()`

Similarly to `startsWith()` this new method will check if the string ends with the value we pass in:

```js
const code = "ABCDEF";

code.endsWith("DDD");
// false
code.endsWith("def");
// false, endsWith is case sensitive
code.endsWith("DEF");
// true

```

We can pass an additional parameter, which is the number of digits we want to consider when checking the ending.

``` js
const code = "ABCDEFGHI"

code.endsWith("EF", 6);
// true, 6 means that we consider only the first 6 values ABCDEF, and yes this string ends with EF therefore we get *true*
```

&nbsp;

### `includes()`

This method will check if our string includes the value we pass in.

```js
const code = "ABCDEF"

code.includes("ABB");
// false
code.includes("abc");
// false, includes is case sensitive
code.includes("CDE");
// true
```

&nbsp;

### `repeat()`

As the name suggests, this new method will repeat what we pass in.

``` js

let hello = "Hi";
console.log(hello.repeat(10));
// "HiHiHiHiHiHiHiHiHiHi"
```


---
&nbsp;

This was the third part of my ES6 for beginners course, check out the rest of them [here](https://albertomontalesi.github.io/courses/es6).

You can also read this articles on medium, on my [profile](https://medium.com/@labby92).

Thank you for reading.