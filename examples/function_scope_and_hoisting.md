## Function scope and hoisting

###### Q: What is the output?

```js

	var name = "John";

	(function(){
	  	console.log("The name is : " + name);

	  	var name = "Jane";

	  	console.log("The name is : " +name);
	})();

```

###### A:

```
	The name is : undefined
	The name is : Jane

```

###### Explanation:

1. **Hoisting :** Hoisting takes place during the parsing phase of executing a JS code. In this phase, all the variables declarations are taken and a default value of "undefined" is assigned to them. Note that the code is not run in this phase, so any assignment of a value to a variable will not be executed.

	So, the variable "name" will be available to the first statement console.log("The name is : " + name); but the variable will have a value of "undefined".

	Hence the first value **undefined** will be logged.


2. **Function Scope :**  Every variable in JS is scoped at a function level, means variables which are declared inside a function is not accessible outside the function in which it is declared.

3. **Scope chaining :** When a variable is not found in a function scope, the execution environment traverses to an outer scope to find the same. Otherwise, the variable which is found in the current scope is used.

	So in the above code, the statement var name = "Jane" declares a variable "name" which is local to the function scope. So the outer variable which has the same variable name is ignored, and the variable in current scope is used. Hence the second statement **console.log("The name is : " + name);** logs a value **Jane**.
	
###### Links:

1. [JavaScript variable scope and hoisting](http://javascriptissexy.com/javascript-variable-scope-and-hoisting-explained/)
