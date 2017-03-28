#Execution Context

>Execution context is the environment in which the code is executed. The execution context of a variable or function defines what 
>other data it has access to, as well as how it should behave. Execution context are of three types:

#### Global Execution Context: 
>This is the default exection context in the which JavaScript code first executes. 
>In web browsers, the global context is said to be that of the window object, so all global variables
>and functions are created as properties and methods on the window object.
>There can be only one global execution context. 

#### Functional Execution Context:
>Each function has its own executed context. Functional execution context are created on each function call. 
>There can be any number of functional execution context.

>When an execution context has executed all of its code, it is destroyed, taking with it all of the variables and functions
>defined within it. The global execution context isn’t destroyed until the application exits, such as when a web
>page is closed or a web browser is shut down.

###Execution context stack
>JavaScript creates a stack of execution context in which it stores all the execution context (both global and functional). 
>When the browser loads the JavaScript file, it pushes Global Execution Context in the Execution Context stack.
>While executing the code in the Global context, when the execution flow gets a function call, it creates a new functional executional 
>context and pushes it to the top in the Execution Context stack.The browser will always execute the current 
>execution context that sits on top of the stack, and once the function completes executing the current execution context, 
>it will be popped off the top of the stack, returning control to the context below in the current stack. 
>Lets understand this with the help of an example:

```javascript
var a = 10;

functionA();

function functionA(){

	console.log("Start function A");

	function functionB(){
		console.log("In function B");
	}

	functionB();

}

console.log("GlobalContext");
```
>Here, when the script loads, by default the global execution context is pushed in the Execution Context stack and
>and the code execution continues with the global execution context. 
>When the execution flow reaches functionA() i.e. call to the functionA, the execution flow enters the body of functionA
>and before executing any code it creates functional execution context and pushes it to the top the stack. 
>As functional execution context of functionA is on the top of execution context stack, JavaScript engines start executing the 
>functionA.
>When inside functionA, execution flow reaches functionB() i.e. call to the functionB, the above process repeats and 
>execution context of functionB is pushed to the top of execution context stack. 
>When functionB is completely executed, JavaScript engines pops off the functionB executional context and returns the 
>control to the functionA execution context.
>Similarly, once functionA is completely executed. functionA execution context will be popped of the execution context stack.
>and the control returns to the global execution context. 

### Execution context in detail
>An execution context can be divided into a creation and execution phase

#### Creation Stage [when the function is called, but before it executes any code inside]:
>In the creation stage, the syntax parser will walk through each line of code, and when it comes to a new variable or function definition, it will commit these variables and functions to memory













