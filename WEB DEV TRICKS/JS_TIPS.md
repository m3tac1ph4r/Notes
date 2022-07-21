
## Stop refereshing page

```JS
submitButton = document.getElementById("submitButton");

const getInfo= (event) =>{
    event.preventDefault();
    alert("Hey");
};
submitButton.addEventListener("click", getInfo);
```

We can use **preventDefault()** for this
