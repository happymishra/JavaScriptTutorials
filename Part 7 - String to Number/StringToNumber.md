# Difference between *~~*, *+* and *parseInt* and Number()

>An empty string ("") evaluates to *0* by the unary plus operator and ~~ operator, while parseInt evaluates to NaN.
```javascript
~~""          //Output -  0
+""           //Output - 0
parseInt("")  //Ooutput - NaN
```

> parseInt builds and parses the string from left to right.  While parsing if it gets an invalid or non-numnerical character
   it returns whatever has been parsed so far. On the contrary unary+ operator gives NaN and ~~ operator gives output as 0
 ```javascript
~~"12rt"          //Output -  NaN
+"12rt"           //Output - NaN
parseInt("12rt")  //Ooutput - 12
  ```
 [link for complete difference](http://jsfiddle.net/EpUBN/8/)
 
 >Conversion of *undefined*
  ```javascript
~~null          //Output -  0
+null          //Output - 0
parseInt(null)  //Ooutput - NaN
  ```
  
   >Conversion of *undefined*
  ```javascript
~~undefined          //Output -  0
+undefined          //Output - NaN
parseInt(undefined)  //Ooutput - NaN
  ```
  
  ```javascript
typeof NaN //Number
123/0 //Infinity
var a = 123/0 
typeof a //Number

isNaN("2") //false - JS internally tries to convert this to number using parseInt("2"). 
  ```
> Values that are truthy or falsey

Any number is except 0 are true
undefined, NaN, null is false

Infinity is true

Strings with characters are true but empty string  is false

> Implicit typecasting
 ```javascript
 

var myString = "88";
var myNum = 88

if(myNum == myString){
	console.log("mystring is equal to mynum");
}
 ```

