





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

<div id="first">Child 1</div>

<div id="second">Child 2</div>

<div id="third">Child 3</div>

<h1> Hello Bois</h1>

</div>

<script src="./test.js"></script>

</body>

</html>
```

```javascript
const a=document.querySelector(".container");
console.log(a.childNodes);
```

## Child nodes
This will take all the text including text and comments.

### Types of Child Nodes

console.log(nodeType)

**Node types:** 
1. Element
2. Attribute
3. Text Node
8. Comment
9. document
10. docType

> If you want to count the child nodes
> console.log(a.childElementCount);


