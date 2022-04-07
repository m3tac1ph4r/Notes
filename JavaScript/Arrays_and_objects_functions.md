## Arrays

```Javascript
const marks=[25,36,96,55,66,25,6,6];
const fruits=["banana","apple","grapes","kiwi"];
const mixed=[25,22,33,"fruits","apple"];

console.log(mixed.length); //5

let index=mixed.indexOf(33); //2

mixed.push(1005);  // [25, 22, 33, 'fruits', 'apple', 1005]

mixed.unshift(1339); //[1339, 25, 22, 33, 'fruits', 'apple', 1005]

mixed.pop(); //[1339, 25, 22, 33, 'fruits', 'apple']

mixed.splice(2,3); //[1339, 25, 'apple']

marks.reverse(); //['apple',25,1339]
```


## Objects

```Javascript
let myObj={

name: 'Harry',

channel: 'CodeWithHarry',

isActive: true,

marks:[1,5,3,6]

}
console.log(myObj.name) //Harry
```

```Javascript
let myObj={

'first_name': 'Harry',

channel: 'CodeWithHarry',

isActive: true,

marks:[1,5,3,6]

}
console.log(myObj['first_name'])  //harry
```



## Functions

```Javascript
function greet(name,greetings){

console.log(`My name is ${name} and I want to say ${greetings}`)

}

greet("ashu","Hey baby");

greet("bero","Hey bro");
```


If by mistake user doesn't give vaue of greeting then it will print *undefined*. To overcome this we can write default value
```Javascript
function greet(name,greetings="Thank you"){

console.log(`My name is ${name} and I want to say ${greetings}`)

}

greet("ashu","Hey baby");

greet("bero");  // it will print thank you in place of greetings in greet()
```



