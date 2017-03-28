# this

>In most cases, the value of this is determined by how a function is called. 
>It can't be set by assignment during execution, and it may be different each time the function is called
>You can change the this context through .call(), .apply() and .bind()
>Value of *this* is equal to the value of the object which invokes the function
>*this* is not assigned a value until an object invokes the function where *this* is defined

### Global Context

>When functions are executed in the global scope, value of *this* is *windows* boject
>In strict mode, value of *this* in the global context will undefined.
>Consider the below example:

```javascript
var myFunciton = function(){
  console.log(this);
  console.log(this=== window);
}

myFunction();// Output: Window object. In strict mode value will be undefined 
```

>The above function was not executed inside any other function or object hence, by default the myFunction was called on the global oject
>Hence the value of this is 'window'. In strict, value would be undefined.

![this in the global context](https://github.com/rupeshmi/CodeSprint/blob/dev/JavaScript/Part5/CodeSnippets/thisGlobal.jpg)

In strict mode, value of this will be undefined
![Value of this in strict model](https://github.com/rupeshmi/CodeSprint/blob/dev/JavaScript/Part5/CodeSnippets/UseStrict.jpg)

### As an object method
>When a function is called as a method of an object, its this is set to the object the method is called on.

To understand this, consider the below example:

```javascript
var val = 37;
var myObj = {
	val : 10,
	someFunction : function(){
		console.log(this.val);//Output: 10 since tha value of this is equal to myObj
		console.log(window.val); //Output: 37
		console.log(this === myObj) // true
		console.log(this)//Output: myObj object
	}
}

myObj.someFunction();
```
#### Console output:
![](https://github.com/rupeshmi/CodeSprint/blob/dev/JavaScript/Part5/CodeSnippets/this.jpg)

> Let's consider an another example to understand *this*

```javascript
//Variable defined in global scope
var val = 37;

var myObj = {
	val : 10
}

var someFunction = function(){
		console.log(this.val);
		console.log(window.val);
		console.log(this === myObj);
		console.log(this);
		console.log(this === window) 
}

myObj.objectFunc = someFunction;
myObj.objectFunc();  
/*
Output:
	1. 10
	2. 37
	3. true
	4. myObj
	5. false
*/

someFunction();
/*
Output:
	1. 37
	2. 37
	3. false
	4. window
	5. true
*/
```
> In the above example, first we call someFunction() in the context of myObj. 
>Later we called the function in the global context. This shows that the value of *this* was determined dynamically 
>on the basis of execution context.

### As a constructor

>When a function is used as a constructor (with the new keyword), its *this* is bound to the new object being constructed.

```JavsScript

function ConstructorFunc(value){
	this.someValue = value;
}

var obj1 = new ConstructorFunction(20);
console.log(obj1.someValue)//Output: 20
```
![](https://github.com/rupeshmi/CodeSprint/blob/dev/JavaScript/Part5/CodeSnippets/constructorThis.jpg)










