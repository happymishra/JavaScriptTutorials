# Prototypes in JavaScript

### Problems with the constructor function

>In the previou [post](https://github.com/rupeshmi/CodeSprint/edit/dev/JavaScript/Part1/Object.md) 
>,we discuss about various ways of creating objects in JavaScript.
>One of the ways to create objects in JavaScript is using the **Constructor** function.
>Consider the construction function below:

```javascript
function Human(firstName, lastName){
	this.firstName = firstName,
	this.lastName = lastName,
	this.fullName = function(){
		return this.firstName + " " + this.lastName;
	}
}
```
>Let's create objects ***person1*** and ***person2*** using the ***Human*** constructor function.

```javascript
var person1 = new Human("Virat", "Kohli");
var person2 = new Human("Sachin", "Tendulkar");
```

>On execution of above code, JavaScript engines creates properties firstName, lastName and method fullName for instances ***person1*** and ***person2*** as shown below:

![alt-text](https://github.com/rupeshmi/CodeSprint/blob/dev/JavaScript/Part2/CodeSnippets/person1.png)
![alt-text](https://github.com/rupeshmi/CodeSprint/blob/dev/JavaScript/Part2/CodeSnippets/person2.png)

> i.e. every object created using the constructor function will have it's own copy of properties and methods. 
>It doesn’t make sense to have two instances of function *fullName* that do the same thing. 
>Storing separte instances of function for each ojects results into wastage of memory.
>We will see as we move forward how we can solve this issue.

### Prototypes

>When a function is created in JavaScript, JavaScript engine adds a *prototype* property to the function. 
>This *prototype* property is an object (called as prototype object) which has a *constructor* property by default. 
>*constructor* property points back to the function on which *prototype object* is a property.
>We can access the function's prototype property using the syntax **functionName.prototype**. 

![](https://github.com/rupeshmi/CodeSprint/blob/dev/JavaScript/Part2/CodeSnippets/ConstructorPrototype.png)

>As shown in the above image, **Human** constructor function has a *prototype* property which points to the prototype object. 
> The prototype object has a *constructor* property which points back to the **Human** constructor function. Let's see an example below:

```javascript
function Human(firstName, lastName){
	this.firstName = firstName,
	this.lastName = lastName,
	this.fullName = function(){
		return this.firstName + " " + this.lastName;
	}
}

console.log(Human);
```
#### Console output
![](https://github.com/rupeshmi/CodeSprint/blob/dev/JavaScript/Part2/CodeSnippets/ObjectUsingConstructorFn.png)

>To access prototype property of the *Human* constructor use the below syntax:

```javascript
console.log(Human.prototype)
```
#### Console output
![](https://github.com/rupeshmi/CodeSprint/blob/dev/JavaScript/Part2/CodeSnippets/HumanPrototype.png)

>As seen from the above image *prototype* property of the function is an oject (prototype object) with two properties

1. *constructor* property which points to  *Human* function itself
2. *\_\_proto\_\_* property - We will discuss about this while explaining *inheritance* in JavaScript

### Creating an object using the constructor function

>When an object is created in JavaScript, JavaScript engine adds a \_\_proto\_\_  property to the newly created object
>which is called as *dunder proto*. **dunder proto or \_\_proto\_\_** points to the prototype object of the constructor function.

![](https://github.com/rupeshmi/CodeSprint/blob/dev/JavaScript/Part2/CodeSnippets/HumanObjectProto.png)

>As shown in the above image, **person1** object which is created using the **Human** constructor function has a 
>**dunder proto or \_\_proto\_\_** property which points to the prototype object of the constructor function.

>Let's see this in code:
```javascript
//Create an object person1 using the Human constructor function
var person1 = new Human("Virat", "Kohli");
console.log(person1);
```
#### Console output

![alt text](https://github.com/rupeshmi/CodeSprint/blob/dev/JavaScript/Part2/CodeSnippets/HumanProtoConsole.png)

>As it can be seen from the above image, both person1's *dunder proto or \_\_proto\_\_* property and *Human.prototype* property are equal
>let's check if they point at the some location using === operator

```javascript
Human.prototype === person1.__proto__ //true
```
>This shows that person1's *dunder proto* property and *Human.prototype* are pointing to the same object. 

>Now, lets's create an another object *person2* using the *Human* constructor function
```javascript
var person2 = new Human("Sachin", "Tendulkar");
console.log(person2);
```
#### Console output
![](https://github.com/rupeshmi/CodeSprint/blob/dev/JavaScript/Part2/CodeSnippets/person2HumanProto.png)

>Above console output shows that even person2's *dunder proto* property is equal to the *Human.prototype* property and they points 
>to the same oject

```javascript
Human.prototype === person2.__proto__ //true
```

>Let's verify if person1's dunder proto and person2's dunder proto points to the same oject

```javascript
person1.__proto__ === person2.__proto__ //true
```
>Above statement proves that the person1's and person2's dunder proto properties points to **Human**  constructor function's prototype object

![](https://github.com/rupeshmi/CodeSprint/blob/dev/JavaScript/Part2/CodeSnippets/person12ConsProto.png)

**Prototype object of the constructor function is shared among all the objects created using the constructor function.**

### Prototype object
>As prototype object is an object, we can attach properties and methods to the prototype object. Thus, enabling all the objects created
>using the constructor function to share the properties and methods.

> New property can be added to the constructor function's prototype property using either the dot notation or square bracket notation as
>shown below:
```javascript
//Dot notation
Human.prototype.name = "Ashwin";
console.log(Human.prototype.name)//Output: Ashwin
//Square bracket notation
Human.prototype["age"] = 26;
console.log(Human.prototype["age"]); //Output: 26
console.log(Human.prototype);
```
#### Console output

![](https://github.com/rupeshmi/CodeSprint/blob/dev/JavaScript/Part2/CodeSnippets/HumanProtAddProp.png)
>name and age properties have been added to Humam.prototype object

#### Example

```javascript
//Create an empty constructor function
function Person(){

}
//Add property name, age to the prototype property of the Person constructor function
Person.prototype.name = "Ashwin" ;
Person.prototype.age = 26;
Person.prototype.sayName = function(){
	console.log(this.name);
}
//Create an object using the Person constructor function
var person1 = new Person();
//Access the name property using the person object
console.log(person1.name)// Output" Ashwin
```
>Let's analyze what happened when we did **console.log(person.name)**
>Let's check if person object has name property
```javascript
console.log(person1);
```
#### Console output
![](https://github.com/rupeshmi/CodeSprint/blob/dev/JavaScript/Part2/CodeSnippets/personEmptyObject.png)

>As we can see that person1 object is empty and it does not have any property except it's *dunder proto* property. 
>So how does the output of console.log(person.name) was "Ashwin"

> When we try to access a property of an object, the seach for the property begins directly on the object itself.
> If a property with a given names is found on the instance, then that value
>is returned; if the property is not found, then the search
>continues up the pointer to the prototype of the object, and the prototype is searched for a property with
>the same name. If the property is found on the prototype, then that value is returned. 

>So, when person1.name is called, JavaScript engine checks if the property exsit on the person oject. In this 
>case, name property was not on the person's object. So, now JavaScript engine checks if the name property exists on the 
dunder proto property or the prototype of the person's object. In this cases, name property was there on 
>the dunder proto property or the prototype of person's object. Hence, the output was returned "Ashwin". 
>If the dunder proto property of the person's object does not have the name property
>then dunder proto property of the dunder proto prperty of the person's object was searched and this process will continue till the 
>dunder proto property is null. In this cases output will be *undefined*.

>Let's create an another object person2 using the Person constructor function
```javascript
var person2 = new Person();
//Access the name property using the person2 object
console.log(person2.name)// Output: Ashwin
```

Now, let's define a property *name* on the person1 oject

```javascript
person1.name = "Anil"
console.log(person1.name)//Output: Anil
console.log(person2.name)//Output: Ashwin
```
>This happended because, when we define a property on the object itself, JavaScript engine takes the *name*
>property from the object itself and not from the objects prototype property i.e. person1 object's *name* property shadows the 
>*name* property of the prototype object.

>person2 does not have *name* property hence, it looks up to the prototype to get the name property. 

#### Problems with the prototype

>Prototype object of the constructor function is shared among all the objects created using the constructor function.
>All properties on the prototype are shared among all the objects created using the constructor function, which is ideal for functions. >Properties that contain primitive values also tend to work well, as shown in the previous example, where it’s
>possible to hide the prototype property by assigning a property of the same name to the object as show in the above example.
>The real problem occurs when a prototype object contains a property of reference type. Consider the following example:

> Modifying the primitive type properties works well as shown below

```javascript
person1.name = "Ganguly"
console.log(perosn1.name);//Output: Ganguly
console.log(person2.name);//Output: Ashwin
```

#### Consider another example to display the issue with proptotypes when the prototype object contains a property of reference type

```javascript
//Create an empty constructor function
function Person(){
}
//Add property name, age to the prototype property of the Person constructor function
Person.prototype.name = "Ashwin" ;
Person.prototype.age = 26;
Person.prototype.friends = ['Jadeja', 'Vijay'],//Arrays are of reference type in JavaScript
Person.prototype.sayName = function(){
	console.log(this.name);
}

//Create objects using the Person constructor function
var person1= new Person();
var person2 = new Person();

//Add a new element to the friends array
person1.friends.push("Amit");

console.log(person1.friends);// Output: "Jadeja, Vijay, Amit"
console.log(person2.friends);// Output: "Jadeja, Vijay, Amit"
```

>Here, the Person.prototype object has a property called friends that contains an array of strings.
>Two objects of Person, person1 and person2 are created. *person1* modifies *friends* property and adds an another string in the array.
>string. Because the friends array exists on Person.prototype, not on person1, the changes made in the friends property by person1 objects are also reflected on person2.friends (which points to the same array). If the intention is to have
>an array shared by all instances, then this outcome is okay. Typically, though, instances want to
>have their own copies of all properties.

#### Combine Constructor/Prototype

>To solve the problems with the prototype and the problems with the constructor, we can combine both the constructor and function.
1. Problem with constructor: Every object has its own instance of the function
2. Problem with the prototype: Modifying a property using one object reflects the other object also

>To solve above both problmens, we can define all the object specific properties inside the constructor and all shared properties and methods insdie the prototype as shown below:

```javascript
//Define the object specific properties inside the constructor
function Human(name, age){
	this.name = name,
	this.age = age,
	this.friends = ["Jadeja", "Vijay"]
}
//Define the shared properties and methods using the prototype
Human.prototype.sayName = function(){
	console.log(this.name);
}
//Create two objects using the Human constructor function
var person1 = new Human("Virat", "Kohli");
var person2 = new Human("Sachin", "Tendulkar");

//Lets check if person1 and person2 have points to the same instance of the sayName function
console.log(person1.sayName === person2.sayName) // true

//Let's modify friends property and check
person1.friends.push("Amit");

console.log(person1.friends)// Output: "Jadeja, Vijay, Amit"
console.log(person2.frinds)//Output: "Jadeja, Vijay"
```
>friends property of person2 did not change on changing the friends property of person1
![](https://github.com/rupeshmi/CodeSprint/blob/dev/JavaScript/Part2/CodeSnippets/ConstProto.png)
