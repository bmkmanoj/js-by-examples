## Named function expression and typeof 

###### Q: What would be the Output?
```js
(function () {

	var func = function namedFuncExp(){ 
		return 23; 
	};
    
	console.log(typeof func);				// 1
	console.log(typeof func());				// 2
	console.log(typeof namedFuncExp);		// 3
	console.log(typeof namedFuncExp());	// 4

})();
```
###### A:

```
function
number 
undefined 
Uncaught ReferenceError: namedFuncExp is not defined(…)
```
###### Explanation

1. The first 2 `console.log`s (#`1` and #`2`) are straight forward, we got what we expected. If you are not clear, here is whats happening. The `typeof func` basically refers to the variable type, which is `function` and the `typeof func()` prints the `typeof` returned value from the function, which is a number (`23`). 

2. The `console.log` #`3` is trying to find the `typeof` named function expression. But this name is only available within the scope of the function (and not outside) and hence, it prints `undefined`. Take a look at the modified code block.


	```js
	(function () {
	
		var func = function namedFuncExp(){ 
	    	console.log(typeof namedFuncExp);  // prints: function
			return 23; 
		};
	
		func();
	})();
	```

3. The `console.log`#`4` is actually trying to execute a function that is not available with that variable name. Sure, we have `func` name defined but not `namedFuncExp` as we saw in the above. Hence, we get the `ReferenceError`.

###### Warning

Never ever do this, will leave it to you to figure out why.

```js	
	(function () {
	
		var func = function namedFuncExp(){ 
	    	console.log(typeof namedFuncExp());  // WTF?
			return 23; 
		};
	
		func();
	})();

```

###### Links

1. [Kangax on Named Function Expressions](https://kangax.github.io/nfe/)
