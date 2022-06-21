# Important code snippets



### To access variable from .env file

```bash
npm install dotenv
```

```JS

const dotenv = require('dotenv');
dotenv.config();
const apiKey = process.env.REACT_APP_ACCESS_KEY;
```

### To create random secret token
[source](https://www.digitalocean.com/community/tutorials/nodejs-jwt-expressjs)

```JS
require('crypto').randomBytes(64).toString('hex')
```

### Generating hash of password using bcrypt :

More you can check reactJS iNotebook project backend/routes/auth.js file

```JS
// creating hash of password
const salt = await bcrypt.genSalt(10);
const secPass = await bcrypt.hash(req.body.password, salt);
```

### Generating JWT AUTH TOKEN using jsonwebtoken

More you can check reactJS iNotebook project backend/routes/auth.js file

```JS

const authToken = jwt.sign(data, TOKEN_SECRET, { expiresIn: process.env.JWT_EXPIRES_IN });
```

### To check wthere entered data is blank or not

```JS

body('password','Password cannot be blank').exists()
```


### To find in which location you are :

We can use useLocation() in react-router-dom to find this

```JS

import { useLocation } from "react-router-dom";
let location = useLocation();
useEffect(() => {
    console.log(location.pathname);
}, [location]);
```


### To update the state values :

The onchange event occurs when the value of an element has been changed. Now, we would be assigning the ‘onChange’ function to the onChange event of the Title and the description field, having type as text. However, to use the ‘onchange’ function we have to first create it. Thus, let’s create the On change function as shown below-

```JS

<div className="mb-3">
    <label htmlFor="title" className="form-label">Title</label>
    <input type="text" className="form-control" name="title" id="title" onChange={onChange} />
</div>

const [note, setNote] = useState({ title: "", description: "", tag: "" });
const onChange = (event) => {
      setNote({ ...note, [event.target.name]: event.target.value })
}
```

**Explanation:** Above, All the values inside the note object will remain on executing the ‘onchange’ function. But, the properties written after the note will be added or overwritten. Consequently, we are using the target property to change the name, that is ‘description’ text, to the value of ‘onchange’. Remember, we are taking ‘event’ of the event as a parameter.

- More you can check on iNotebook project src/components/AddNote.js



### To Prevent reloading after clicking button :

```JS
const handleClick =(event) =>{
	event.preventDefault();
}

<button type="submit" onClick={handleClick}>Submit</button>
```


### To remove the input feild when user entered the input :

If we are useState then we will update the state when submit button is clicked and then after that change the value of input tag

* This is the state declaration
```JS

const [note, setNote] = useState({ title: "", description: "", tag: "" });
```

* This is the onClick function when button is clicked
```JS

const handleClick = (event) => {
        setNote({ title: "", description: "", tag: "" });
}
```

* These are the input tag in which we added value attribute which will update the values after submit button is clicked
```JS

<input type="text" className="form-control" name='description' id="description" value={note.description} onChange={onChange} minLength={3} required />
```
	