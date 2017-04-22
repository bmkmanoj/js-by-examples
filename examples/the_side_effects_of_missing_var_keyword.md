## The side effects of missing var keyword

###### Q: What is the output?

```js

	(function() {						// 1
   		var myVar = myVarCopy = 42;		// 2
	})();
	
	console.log(myVar);					// 3
	console.log(myVarCopy);				// 4
	
```

###### A:

```
	Uncaught ReferenceError: myVar is not defined
	42
```

###### Explanation

1. The code uses IIFE (Immediately Invoked Function Expression/Execution) pattern. This in turn creates a block scope, so `myVar` is not accessible outside the block. Hence, the `console.log` at #`3` (in the outer scope) gives a reference error. 
2. Unlike `myVar`, the `myVarCopy` is directly assigned `42` at #`2` without explicitly declaring it with `var` keyword and the gotcha here is the JavaScript engine doesn't complain and creates the `myVarCopy` variable in the global scope - in this case, the `window` object scope.
3. To avoid this side effect, ES5 has a provision to catch this kind of code. Its the `use strict` statement which can be used in any scope. Take a look at this code sample with `use strict`, it throws the ReferenceError

	```js

		(function (){
			"use strict";					// 5
			var myVar = myVarCopy = 42; 	// Uncaught ReferenceError: myVarCopy is not defined(…)
		})();
		
		console.log(myVar);					
		console.log(myVarCopy);				
	```


###### Links
1. [MDN on var](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Statements/var)
2. [MDN on 'use strict'](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Strict_mode)
3. [Stackoverflow question on strict mode](http://stackoverflow.com/questions/1335851/what-does-use-strict-do-in-javascript-and-what-is-the-reasoning-behind-it)


