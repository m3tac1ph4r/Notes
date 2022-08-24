# ReactJS Important Interview Questions


### 1. What is useState() in React?
The useState() is a built-in React Hook that allows you for having state variables in functional components. It should be used when the DOM has something that is dynamically manipulating/controlling.

### 2. What are the differences between functional and class components?
-   **Declaration**
Functional components are nothing but JavaScript functions and therefore can be declared using an arrow function or the function keyword:
```javascript
  function card(props){
   return(
      <div className="main-container">
        <h2>Title of the card</h2>
      </div>
    )
   }
   const card = (props) =>{
    return(
      <div className="main-container">
        <h2>Title of the card</h2>
      </div>
    )
   }
```

Class components, on the other hand, are declared using the ES6 class:
```JS
class Card extends React.Component{
  constructor(props){
     super(props);
   }
    render(){
      return(
        <div className="main-container">
          <h2>Title of the card</h2>
        </div>
      )
    }
   }
```

-   **Handling props**
```plaintext
<Student Info name="Vivek" rollNumber="23" />
```
In functional components, the handling of props is pretty straightforward. Any prop provided as an argument to a functional component can be directly used inside HTML elements:

```JS
 function StudentInfo(props){
   return(
     <div className="main">
       <h2>{props.name}</h2>
       <h4>{props.rollNumber}</h4>
     </div>
   )
 }
```

In the case of class components, props are handled in a different way. We use **this** keyword in class based component.
```JS
class StudentInfo extends React.Component{
   constructor(props){
     super(props);
    }
    render(){
      return(
        <div className="main">
          <h2>{this.props.name}</h2>
          <h4>{this.props.rollNumber}</h4> 
        </div>
      )
    }
   }
```

![[functionalVSclass component.png]]


### 3. What are props in React ?
The props in React are the inputs to a component of React. They can be single-valued or objects having a set of values that will be passed to components of React during creation by using a naming convention that almost looks similar to HTML-tag attributes. We can say that props are the data passed from a parent component into a child component.


### 4. Explain React state and props.

![[stateVSprops.png]]


### 5. What are the rules that must be followed while using React Hooks?
There are 2 rules which must be followed while you code with Hooks:

-   React Hooks must be called only at the top level. It is not allowed to call them inside the nested functions, loops, or conditions.
-   It is allowed to call the Hooks only from the React Function Components


### 6. What is the use of useEffect React Hooks?
The useEffect React Hook is used for performing the side effects in functional components. With the help of useEffect, you will inform React that your component requires something to be done after rendering the component or after a state change. The function you have passed(can be referred to as “effect”) will be remembered by React and call afterwards the performance of DOM updates is over. Using this, we can perform various calculations such as data fetching, setting up document title, manipulating DOM directly, etc, that don’t target the output value. The useEffect hook will run by default after the first render and also after each update of the component. React will guarantee that the DOM will be updated by the time when the effect has run by it.

The useEffect React Hook will accept 2 arguments: `useEffect(callback,[dependencies]);`

Where the first argument callback represents the function having the logic of side-effect and it will be immediately executed after changes were being pushed to DOM. The second argument dependencies represent an optional array of dependencies. The useEffect() will execute the callback only if there is a change in dependencies in between renderings.


### 7. Why do React Hooks make use of refs?
The refs are used for:

-   Managing focus, media playback, or text selection.
-   Integrating with DOM libraries by third-party.
-   Triggering the imperative animations.

