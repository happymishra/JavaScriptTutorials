#Inheritance in JavaScript

## Prototype Chaining
>JavaScript does not have classes unlinke other languages. It uses the concept of prototypes for inheritance.
>To understand how JavaScript implements inheritance, go through [this artice](https://github.com/rupeshmi/CodeSprint/blob/dev/JavaScript/Part2/Prototypes.md) to understand how prototypes work.
>Prototype chaining means an objects dunder proto or __proto__ will point to another object instead of 
>pointing to the constructor function prototype. If the other object's dunder proto or __proto__ property points to another object
>it will results into chain. This is prototype chaining. 

![Prototype chaining](https://github.com/rupeshmi/CodeSprint/blob/dev/JavaScript/Part4/CodeSnippets/ProtoTypeChaining.jpg)

Let's implement prototype chaining
```javascript
//SuperType constructor function
function SuperType(){
	this.name = "Virat"
}

//SuperType prototype
SuperType.prototype.getSuperName = function(){
	return this.name
}

//SubType prototype function
function SubType(){
	this.age = 26
}

//Inherit the properties from SuperType
SubType.prototype = new SuperType();

//Add new property to SubType prototype
SubType.prototype.getSubAge = function(){
	return this.age;
}

//Create a SubType object
var subTypeObj = new SubType();
console.log(subTypeObj.name); //Output: Virat
console.log(subTypeObj.age); //Output: 26
console.log(subTypeObj.getSuperName()); //Output: Virat
console.log(subTypeObj.getSubAge()); //Output: 26
```
>Above code defines two consructor functions, SuperType and SubType. 
>By default, *SubType.prototype* has a *constructor* function which points to the constructon function itself
>and *__proto__* property which inherits the default object properties

```javascript
//Inherit the properties from SuperType
SubType.prototype = new SuperType();
```

>Above line rewrites the default prototype of the SubType constructon function 
>and makes SubType.prototype to point to an object of SuperType constructor function.
>This means that all the properties and methods that typically exists on an instance of SuperType now also on SubType.prototype
>This means that now, SubType function has access to all the SuperType properties and methods

```javascript
//Add new property to SubType prototype
SubType.prototype.getSubAge = function(){
	return this.age;
}
```
>After the default prototype of SubType constructor function has been overwritten, by using the above line of code
>we add a new method *getSubAge()* on top of what was inherited from SuperType, to the prototype object of SubType constructor function

>**Note**: New methods must be added to the SubType after the inheritance 
>because inheritance overwrites the existing prototype of SubType

![Inheritance using prototype chaingin](https://github.com/rupeshmi/CodeSprint/blob/dev/JavaScript/Part4/CodeSnippets/ProtoChainInheritance.jpg)

#### Console Output
>SuperType.prototype

![SuperType prototype](https://github.com/rupeshmi/CodeSprint/blob/dev/JavaScript/Part4/CodeSnippets/SuperTypePrototype.jpg)

>SubType prototype

![SubType.prototype](https://github.com/rupeshmi/CodeSprint/blob/dev/JavaScript/Part4/CodeSnippets/SubTypeProtoType.jpg) 

>SubType constructor

![SubType constructor](https://github.com/rupeshmi/CodeSprint/blob/dev/JavaScript/Part4/CodeSnippets/SubTypeConst.jpg)

>***Note***: getSuperName() method remains on the SuperType.prototype object, but name property ends up on
SubType.prototype. That’s because getSuperName() is a prototype method, and property is
an instance property. SubType.prototype is now an instance of SuperType, so property is stored
there. Also note that SubType.prototype.constructor points to SuperType, because the constructor
property on the SubType.prototype was overwritten.

#### Problems with prototype chaining
>As all the properties of the super type prototype are shared among the child objects, if one child modifies the property of the 
>Super type prototype, other childs also gets affected. This issue has been explined in greate details 
[here](https://github.com/rupeshmi/CodeSprint/blob/dev/JavaScript/Part2/Prototypes.md)

>To fix this issue, we use constructor to inherit the instance properties and prototype chaining to to inherit methods and share properties


```javascript
//SuperType constructor function
function SuperType(firstName, lastName){
	this.firstName = "Virat",
	this.lastName = "Kohli",
	this.friends = ["Ashwin", "Jadeja"]
}

//SuperType prototype
SuperType.prototype.getSuperName = function(){
	return this.firstName + " " + this.lastName;
}

//SubType prototype function
function SubType(firstName, lastName, age){
	//Inherit instance properties
	SuperType.call(this, firstname, lastName);
	this.age = age;
}

//Inherit methods and shared properties
SubType.prototype = new SuperType();

//Add new property to SubType prototype
SubType.prototype.getSubAge = function(){
	return this.age;
}

//Create SubType objects
var subTypeObj1= new SubType("Virat", "Kohli", 26);
var subTypeObj2 = new SubType("Sachin", "Tendulkar", 39);

//Modify the friends property using the subTypeObj1
subTypeObj1.friends.push("Amit");

console.log(subTypeObj1.friends);//["Ahswin", "Jadega", "Amit"]
console.log(subTypeObj2.friends);//["Ashwin", "Jadega"]

//subTypeObj1
console.log(subTypeObj1.firstName); //Output: Virat
console.log(subTypeObj1.age); //Output: 26
console.log(subTypeObj1.getSuperName()); //Output: Virat Kohli
console.log(subTypeObj1.getSubAge()); //Output: 26

//subTypeObj2
console.log(subTypeObj2.firstName); //Output: Sachin
console.log(subTypeObj2.age); //Output: 39
console.log(subTypeObj2.getSuperName()); //Output: Sachin Tendulkar
console.log(subTypeObj2.getSubAge()); //Output: 39
```
>Let's try to understand the code
>First, we have defined a SuperType constructor function with firstName, lastName and friends as instance properties
>Then we defined a superName property on prototype of SuperType

>Now, let's look how we define the SubType constructr function

```javascript
//SubType prototype function
function SubType(firstName, lastName, age){
	//Inherit instance properties
	SuperType.call(this, firstname, lastName);
	this.age = age;
}
```
>Here, we define a SubType constructor function. 
>Inside the SubType constructor function, we call the SuperType constructor function with call.
>Call executes the SuperType constructor function in contecxt of the object begin created using the SubType constructor fucntion
>After inheriting the instance properties of the SuperType, we add one age property to the SubType constructor function


```javascript
//Inherit methods and shared properties
SubType.prototype = new SuperType();
```
>So far we have just inherited all the instance properties of the SuperType constructor function, but the shared properties and methods 
of the SuperType constructor function are still not inherited. We inherit them using the above lines of code. 

>Once the above lines of code are executed, we have inherited all the properties of the SuperType constructor function


```javascript
//Add new property to SubType prototype
SubType.prototype.getSubAge = function(){
	return this.age;
}
>Using the above lines of code, we add a new property to SubType prototype on top of the methods and properties inherited 
>from the SuperType constructor function

>Let's understand the whole process by creating an object using SubType constructor function
```javascript
var subTypeObj1= new SubType("Virat", "Kohli", 26);
```

>When we execute the above line of code, all the three parameters(Virat, Kohli and 26) are passed to the SubType constructor function.
>SubType constructor function, then calls SuperType constructor function using call *SuperType.call(this, firstname, lastName)*
>*this* here represent the *subTypeObj1*

>SuperType constructor function is executed in the context of *subTypeObj1* and add propeties firstName, lastName, friends to the *subTypeObj1* object
>After return of *SuperType.call(this, firstname, lastName)*, SubType constructor function adds a *age* property to *subTypeObj1* object.

>Thus as of now there are properties with the *subTypeObj1* object (firstName, lastName and age).
Currently SubType constructor function has following methods and shared propertes in its prototype property:
1. getSuperName()
2. getSubAge

*subTypeObj1* inherits all these properties from SubType constructor function. 

```javascript
console.log(subTypeObj1)
```

>Console output

![](https://github.com/rupeshmi/CodeSprint/blob/dev/JavaScript/Part4/CodeSnippets/subTypeObj1.jpg)
