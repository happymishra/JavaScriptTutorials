# Global Object function

>JavaScript runtime has many global objects and functions.
Global object function is a function in JavaScript which is called as **Object**

>Let's see an example:

```javascript
console.log(Object); //Global constructor function with name as Object
```

![](https://github.com/rupeshmi/CodeSprint/blob/dev/JavaScript/Part3/CodeSnippets/ObjectFunction.png)

>Above statement gives the definition of the *Object* function. 

>Prototype of the Object() function

```javascript
console.log(Object.prototype); //Global constructor function with name as Object
```
![](https://github.com/rupeshmi/CodeSprint/blob/dev/JavaScript/Part3/CodeSnippets/ObjectPrototype.png)

>Let's call this function

```javascript
console.log(Object()); //Outputs: Empty object with __proto__ prperty
```
![](https://github.com/rupeshmi/CodeSprint/blob/dev/JavaScript/Part3/CodeSnippets/ObjectfromObjectfn.jpg)

>Object() gives an object which is empty and have __proto__ property
This object is inherited by all other objects in JavaScript

>\_\_proto\_\_ property points to the prototype object of the constructor function i.e Object()

```javascript
var obj = Object()
console.log(obj.__proto__); //Outputs: An object with some properties
console.log(a.__proto__ === Object.prototype) //true
```

![](https://github.com/rupeshmi/CodeSprint/blob/dev/JavaScript/Part3/CodeSnippets/ObjectObjProto.jpg)

>Let's create an empty functiom

```javascript
var a = function(){}
console.log(a.prototype)
```

![](https://github.com/rupeshmi/CodeSprint/blob/dev/JavaScript/Part3/CodeSnippets/aPrototype.jpg)

>Above image shows that a.prototype has two propertis

1. constructor - which points to the function itself (console.log(a === a.prototype.constructor) // true)
2. __proto__ - which is inherited from Object() 

```javascript
console.log(a.prototype.__proto__ === Object().__proto__); //Output: true
```



