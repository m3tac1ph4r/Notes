

### starting the project

```bash
npm init
npm install express
```

### Create express application

```javascript
var express = require('express')
var app = express()
```


### API Methods

* **GET** - read data *app.get(route,callback)*
* **POST** - create new data
* **PUT** - update data
* **DELETE** - Delete data

### GET

The callback function has 2 parameters -> request(req) and response(res). 
The request object (req) represents the HTTP request and has properties for the request query string, parameter, body, HTTP headers etc.

Simlarly the response object represents the HTTP response that the express app sends when it receives as HTTP request.



```JS
app.get("/",(req,res) => {
    res.send("Hello WORLD from the express");
});

app.get("/about",(req,res) => {
    res.send("This is about");
});
```



### How to send json data:

```JS
app.get("/about",(req,res) =>{
    res.send({
        id:1,
        name:"ashu",
	});
});
```


### To listen at specfic port

```JS
app.listen(8000,() =>{
    console.log("listening the port at 8000");
});
```


### Serve file in express using middleware

There are two types of path:

1. **Absolute Path :** An **absolute path** is defined as specifying the location of a file or directory from the root directory(/). In other words,we can say that an absolute path is a complete path from start of actual file system from / directory.
2. **Relative Path :** Relative path is defined as the path related to the present working directly(pwd). It starts at your current directory and **never starts with a /** .

	
We use relative path in expressjs to serve files.

```JS
const static_path=path.join(__dirname,'../public');
app.use(express.static(static_path));
```

We willl use express.static for serving files 