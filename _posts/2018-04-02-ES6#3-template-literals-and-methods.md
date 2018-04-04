---
title: "ES6 for Beginners #3: Template literals & additional string methods"
categories:
  - ES6
tags:
  - programming
  - guide
---


![ES6-card-3](https://albertomontalesi.github.io/assets/images/ES6/ES6-card-3.jpg)

Prior to ES6 they were called *template strings*, now we call them  *template literals*. Let's have a look at what changed in the way we interpolate strings in ES6.

&nbsp;

### Interpolating strings

In ES5 we used to write this, in order to interpolate strings:

``` javascript
var greeting = 'Hello my name is' + name;
var name = "Alberto";
```

In ES6 we can use backticks to make our life easier.

``` javascript
const greeting = `hello my name is ${name}`;
let name  = "Alberto";
```


### Expression interpolations

In ES5 we used to write this:

``` javascript
var a = 1;
var b = 10;
console.log('1 * 10 is ' + ( a * b));
// "1 * 10 is 10

```

In ES6 we can use backticks to reduce our typing:

``` javascript
var a = 1;
var b = 10;
console.log(`1 * 10 is ${a * b}`);
// "1 * 10 is 10
```

&nbsp;

###  Create HTML fragments

In ES5 we used to do this to write multi-line strings: 

``` javascript
// We have to include a backslash on each line
var text = " hello, \
my name is Alberto \
how are you?\
```

In ES6 we simply have to wrap everything inside backticks, no more backslash on each line.

``` javascript 
const content = ` hello,
my name is Alberto
how are you?`;
```

&nbsp;

### Nesting templates 

It's very easy to nest a template inside another one, like this: 

``` js
const markup = `
<li>
  ${people.map(person => `<li>  ${person.name}</li>`)}
</li>
`;
```

&nbsp;

###  Add a ternary operator

We can easily add some logic inside our empplate string by using a ternary operator:

``` js
// create an artist with name and age
const artist = {
  name: "Bon Jovi";
  age: 56;
}

// only if the artist object has a song property we then add it to our paragraph, otherwise we return nothing
const text = `
  <div>
    <p>  `${artist.name} is ${artist.age} years old ${artist.song ? ` and wrote the song ${artist.song}` : ' '}
    </p>
  </div>
`
```
&nbsp;

### pass a function inside a template literal

Similarly to the example above, if we want we can pass a function inside a template literal.

``` js
const groceries = {
  meat: "pork chop";
  veggie: "salad";
  fruit: "apple";
  others: ['mushrooms', 'instant noodles', 'instant soup']
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
    ${groceryList(groceries.others)}
  <div>
`
```
&nbsp;
&nbsp;

## Tagged template literals

By tagging a function to a template literal we can run the template literal through the function, providing it with everything that's inside of the template.

The way it works is very simple: you just take the name of your function and put it in front of the template that you want to run it against.


``` js
// our function will take an array of strings and an array of values, Here we use the **rest** operator to take all the values from our variable and put them in an array
function myTag(strings, ...values){
  // code goes here
}


const name = "Alberto";
const age = "25'
// we tag the function by putting its name in front of our string
const sentence = myTag `Hello my name is ${name} and I am ${age} years old`;

```

The first thing we get is an array of strings, which are  all the content in between each of our arguments.

- Hello my name is
- and I am
- years old

The second thing we get are all the arguments that we interpolated.  If you don't know how many arguments are there you need to use the rest operator (more on this in a next chapter).

As the name implies the rest operator (the three dots) will just take whatever is left after our first parameter strings and put it into an array.

What we have now are two arrays, one of strings and one of values.

We can now build our own string by combining strings and values together.

``` js
function myTag(strings, ...values){
  // create an empty variable
  let str = ();
  // for each string take its value and an index
  strings.forEach(string, i => {
  // add to the variable the value of the string and the content of values at the index of the string
  // as our original string ends with a string it means that we have one more *string* than *value* so we add a simple **||** to check, if there is a value, add it, otherwise add nothing.
    str += string + (values[i] || '') ;
  });
  return str;
}

const name = "Alberto";
const age = "25";
const sentence = myTag `Hello my name is ${name} and I am ${age} years old`;

```

If we did not add this line 

``` js
str += string + (values[i] || '') ;
```

We would have gotten

```js 
"Hello, my name is ALberto and I am 25 years oldundefined"
```



--- 

&nbsp;
&nbsp;

To learn more about use cases of *template literals* check out [this article](https://codeburst.io/javascript-es6-tagged-template-literals-a45c26e54761).

&nbsp;
&nbsp; 

## Additional string methods

We are going to cover 4 new strings method:
- startsWith()
- endsWith()
- includes()
- repeat()

### startsWith()

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

### endsWith()

Similarly to **startsWith()** this new method will check if the strings end with the value we pass in:

```js
const code = "ABCDEF";

code.endssWith("DDD");
// false
code.endssWith("def");
// false, endsWith is case sensitive
code.endssWith("DEF");
// true

```

We can pass an additional parameter, which is the number of digits we want to consider when checking the ending. 

``` js
const code = "ABCDEFGHI"

code.endsWith("EF", 6);
// true, 6 means that we consider only the first 6 values ABCDEF, and yes this string ends with EF therefore we get *true*
```

&nbsp;


### includes()

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

### repeat()

As the name suggests, this new method will repeat what we pass in.

``` js

let hello = "Hi";
console.log(hello.repeat(10));
// "HiHiHiHiHiHiHiHiHiHi"
```


---

This was the third part of my ES6 for beginners course, check out the rest of them [here](https://albertomontalesi.github.io/courses/es6).

You can also read this articles on medium, on my [profile](https://medium.com/@labby92).

Thank you for reading.