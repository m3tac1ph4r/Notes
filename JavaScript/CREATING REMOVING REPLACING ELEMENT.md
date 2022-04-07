## CREATING NEW ELEMENT AND ADDING  IN EXISTING ELEMENT


```html
<!DOCTYPE html>

<html lang="en">

<head>

<meta charset="UTF-8">

<meta http-equiv="X-UA-Compatible" content="IE=edge">

<meta name="viewport" content="width=device-width, initial-scale=1.0">

<title>Document</title>

</head>

<body>

<div class="container">

<h1>Hello we are</h1>

<ul class="this">

<li class="my">hello</li>

<li class="my">bois</li>

<li class="my">cascas</li>

</ul>

</div>

<script src="./test.js"></script>

</body>

</html>
```


```javascript
const ele=document.createElement('li');
ele.id="my"

ele.innerText="beti";

ele.innerHTML="<b>beti</b>"

let ul=document.querySelector('.this');

ul.appendChild(ele);

console.log(bol);
```

