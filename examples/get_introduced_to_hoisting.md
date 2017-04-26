## Get introduced to hoisting 

###### Q: What is the output?


```js
	
	function func() {
		return varOrFunc;		// 1
		varOrFunc = 1;			// 2
		function varOrFunc() {		// 3
    			console.log("Inside varOrFunc")
    		}
    		var varOrFunc = '2';		// 4
	}
	console.log(typeof func());
	
```
###### A: 

```
	function
```

###### Explanation

1. It seems like the return statement at #`1` should return immediately, ignoring rest of the code below it. But that is not what happening here.
2. To understand the output, you need to understand a concept called *hoisting* (for both variable and function). Function declarations and variable declarations are hoisted to the top of the scope. In this case, the scope is at `func` level. Considering this, we can say that the following code mimicks (and not to be taken literally) the hoisting aspect/behaviour.

	```js
		
		function func() {
			// hoisted
			function varOrFunc() {	// 3
				console.log("Inside varOrFunc")
			}
			var varOrFunc;			// 2.1
			return varOrFunc;// 1
			varOrFunc = 1;			// 2.2
			varOrFunc = '2';		// 4
		}
		console.log(typeof func());

	```
3. A thing to note here is that, we have the same variable name `varOrFunc` being used for `function` name and for `var` declaration - in such scenarios, the function declaration takes precedence over the variable declaration and hence the line #`2.1` essentially has no effect on the output and we see that the `varOrFunc` is actually a function type in the `console.log`.
4. Also, only the variable and function declarations are hoisted. Function expressions are not.
5. Function declarations takes precedence over only variable declaration but not variable assignment.
     
	```js
	
		var varOrFunc = "String Assigned";
		
		function varOrFunc() {
			return "Function Executed";
		}
        
        	console.log("typeof of varOrFunc is " + typeof varOrFunc);  // output: typeof of varOrFunc is String
 	```

###### Links
1. [JS Scoping and Hoisting](http://www.adequatelygood.com/JavaScript-Scoping-and-Hoisting.html)
2. [JavaScript Variable Scope and Hoisting Explained] (http://javascriptissexy.com/javascript-variable-scope-and-hoisting-explained/)
