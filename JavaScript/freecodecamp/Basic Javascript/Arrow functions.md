# Arrow functions in ES6

ES6 provides us with the syntactic sugar to not have to write anonymous functions this way. Instead, you can use **arrow function syntax**:

```Javascript
const myFunc = function() {
  const myVar = "value";
  return myVar;
}
```


**Arrow function**
```js
const myFunc = () => {
  const myVar = "value";
  return myVar;
}
```

When there is no function body, and only a return value, arrow function syntax allows you to omit the keyword `return` as well as the brackets surrounding the code. This helps simplify smaller functions into one-line statements:

```js
const myFunc = () => "value";
```

This code will still return the string `value` by default.



###  Write Arrow Functions with Parameters

If an arrow function has a single parameter, the parentheses enclosing the parameter may be omitted.
 
 ```js
const doubler = item => item * 2;
```


It is possible to pass more than one argument into an arrow function.

```js
const multiplier = (item, multi) => item * multi;
multiplier(4, 2);
```

### Set Default Parameters for Your Functions

In order to help us create more flexible functions, ES6 introduces default parameters for functions.

```js
const greeting = (name = "Anonymous") => "Hello " + name;

console.log(greeting("John"));
console.log(greeting());
```


### Use the Rest Parameter with Function Parameters

In order to help us create more flexible functions, ES6 introduces the rest parameter for function parameters. With the rest parameter, you can create functions that take a variable number of arguments. These arguments are stored in an array that can be accessed later from inside the function.

```js
function howMany(...args) {
  return "You have passed " + args.length + " arguments.";
}
console.log(howMany(0, 1, 2)); // You have passed 3 arguments
console.log(howMany("string", null, [1, 2, 3], { })); //You have passed 4 arguments
```


```js
const sum = (...args) => {
  // const args = [x, y, z];
  return args.reduce((a, b) => a + b, 0);
}
```
