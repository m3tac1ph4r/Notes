
```HTML
<!DOCTYPE html>

<html lang="en">

<head>

<meta charset="UTF-8">

<meta http-equiv="X-UA-Compatible" content="IE=edge">

<meta name="viewport" content="width=device-width, initial-scale=1.0">

<title>Document</title>

</head>

<body>

<h1>Hello we are</h1>

<div id="first">Child 1</div>

<div id="second">Child 2</div>

<div id="third">Child 3</div>

<script src="./test.js"></script>

</body>

</html>
```

If we want to select any element using javascript then we can use this:

**Using getElementId()**

```Javascript

let a=document.getElementById('first');

a.style.color='red';

a.innerHTML="<b>Hello Ji</b>"
```


**Using querySelector()**

```Javascript
let a=document.querySelector('#first');

a.innerHTML="Hello Bois"
let sel=document.querySelector('h1');  // this will select the first tag name
```


**Selecting particular tag in DOM**

```Javascript
let sel=document.getElementsByTagName('h1');

for(let index=0;index<sel.length;index++){

sel[index].style.color="green";
//This will set green color to all h1
}
```


