## Closures in loop

###### Q: What is the output?


```js

	var data = [0, 1, 2];
	var funcs = [];
	
	function init() {						// 0
		for (var i = 0; i < 3; i++) {
    				
	    	var x = data[i];				// 1
 	    	var innerFunc = function() { 	// 2
 	    		return x;
 	    	};
 
 			funcs.push(innerFunc);			// 3
 		}
	}
	
	function run() {						// 4
		for (var i = 0; i < 3; i++) {
		    console.log(data[i] + ", " +  funcs[i]());   // 5
  		}
	}
	
	init();
	run();
	
```

###### A: 

```
		0, 2
		1, 2
		2, 2

```

###### Explanation

1. This popularly is known as "closure in loop" issue in JavaScript and beginners to this language invariably encounter this. We need to understand the concept of closure to undestand the output. Closures are functions that refer to independent (free) variables. In other words, the function defined in the closure 'remembers' the environment in which it was created.

2. The problem is that the variable x, within each of the inner functions at #`2` (i.e. `innerFunc`), is bound to the same variable outside of the function. This is because the variables are scoped to the function `init` and not block scoped in JS. Take a look at this modified code which prints the output you expect (`0, 0` ...) to understand the variable scope binding inside the `innerFunc`.

	```js
		
		var data = [0, 1, 2];
		var funcs = [];
	
		function init() {						// 0
			for (var i = 0; i < 3; i++) {
    				
	    		var x = data[i];				// 1
 	    		var innerFunc = function() { 	// 2
 	    			var temp = x;
 	    			return function() {
 	    				return temp;
 	    			}; 
 	    		}();
 
 				funcs.push(innerFunc);			// 3
 			}
		}
	
		function run() {						// 4
			for (var i = 0; i < 3; i++) {
			    console.log(data[i] + ", " +  funcs[i]());   // 5
  			}
		}
	
		init();
		run();
	
	```
	 
3. There are atleast 3 more ways to overcome the closure in loop issue, Dave Herman's article (see the link below) describes them in details. Also, ES6 has provision for block scoping of variable through `let` keyword declaration.

4. Do not fret if you still are not clear about how the closures work, it takes sometime to come to terms with closures. So, do read on.

###### Links

1. [MDN on JS Closures](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Closures)
2. [Dave Herman on Closure in loop](http://calculist.blogspot.com/2005/12/gotcha-gotcha.html)
3. [Stackoverflow question on closures](http://stackoverflow.com/questions/111102/how-do-javascript-closures-work)
4. [Stackoverflow question on closures in loop](http://stackoverflow.com/questions/750486/javascript-closure-inside-loops-simple-practical-example/19323214#19323214)
5. [JSFiddle for closures in loop](https://jsfiddle.net/davidojedalopez/jvhw9846/)
