## call() and apply()

>The call() and apply() method calls a function with a given *this* value and arguments provided.
>The fundamental difference between call() and apply() is call() accepts an argument list, while apply() accepts a single array of arguments.
The first parameter in the call and apply methods set the this value to the object that the function is invoked upon

###call()
>Example:

```javascript
var globalString = "Be happy";

function someFunction(name){
	// The "this" keyword here will be bound to the global object, unless we set the "this" with Call or Apply
	this.globalString = name;
}

var myObj = {
}
 // If we execute the someFunction function here, "this" inside the function is bound to the global window object:
someFunction("Sachin");

 // Proof that the globalString was set on the global window object
console.log(window.globalString); //Output: Sachin
console.log(myObj.globalString); // Output: undefined

globalString = "Be happy"

// To set the "this" value explicitly, so that "this" is bound to the gameController,
// We use the call () method:
someFunction.call(myObj, "Virat");

console.log (window.globalString); //"Be happy"
console.log (myObj.globalString); // Virat
```

