# Objects in Javascript

#### To delete property from object:

```Javascript
const myDog = {
  "name": "Happy Coder",
  "legs": 4,
  "tails": 1,
  "friends": ["freeCodeCamp Campers"],
  "bark": "woof"
};

delete myDog.tails;
```


#### To check whether the object own the property or not:

Sometimes it is useful to check if the property of a given object exists or not. We can use the `.hasOwnProperty(propname)` method of objects to determine if that object has the given property name. `.hasOwnProperty()` returns `true` or `false` if the property is found or not.

```Javascript
const myObj = {
  top: "hat",
  bottom: "pants"
};

myObj.hasOwnProperty("top");	// true
myObj.hasOwnProperty("middle");	// false
```


#### Accessing the nested objects:

The sub-properties of objects can be accessed by chaining together the dot or bracket notation.

```Javascript
const ourStorage = {
  "desk": {
    "drawer": "stapler"
  },
  "cabinet": {
    "top drawer": { 
      "folder1": "a file",
      "folder2": "secrets"
    },
    "bottom drawer": "soda"
  }
};

ourStorage.cabinet["top drawer"].folder2; //secrets
ourStorage.desk.drawer; //stapler
```


```Javascript
const myStorage = {
  "car": {
    "inside": {
      "glove box": "maps",
      "passenger seat": "crumbs"
     },
    "outside": {
      "trunk": "jack"
    }
  }
};

const gloveBoxContents = myStorage.car.inside["glove box"]; //maps
```
