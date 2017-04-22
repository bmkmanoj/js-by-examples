## Functions and implicit eval

###### Q: What is the output?

```js

	var count = 1;
	if (function tempFunc(){}) {
		count += typeof tempFunc;
	}
	console.log(count);
￼	
```

###### A: 

```		
	1undefined

```

###### Explanation

1. To understand the logged output, we need to understand how JS treats functions within the condition checking. The `if` condition evaluates function expression (though it seems like a declaration) using `eval`, so `eval(function tempFunc() {})` returns `function tempFunc() {}` which is coerced as true. So, we actually get inside the if block and `console.log` gets executed.
2. However, when executing the `typeof tempFunc` - it returns `undefined` because the `if` code executes at run time and the statement inside the `if` condition is evaluated only during the run time.
3. To verify the behavior, we can also check the modified code below - which also prints `1undefined`.

	```js
		
		var count = 1;
		if (true) {
    		eval(function tempFunc(){});
    		count += typeof tempFunc;
    	}
		console.log(count);		// also prints: 1undefined
		
	```
4. To make it print `1function`, use the function declaration form as shown below.


	```js
		
		var count = 1;
		if (true) {
    		function tempFunc(){};
    		count += typeof tempFunc;
    	}
		console.log(count);
		
	```
