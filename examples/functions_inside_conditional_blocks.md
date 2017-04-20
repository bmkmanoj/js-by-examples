## Functions inside conditional blocks

###### Q: What is the output?

```js

	(function(){
			
		if(true){								// 1
		
      		function innerFunc() {				// 2
      		
          		console.log("innerFunc: Inside if");
      		}
      		
      		var innerFuncExpr = function () {	// 3
      		
          		console.log("innerFuncExpr: Inside if");
      		}
      	} else {								// 4
      	
      		function innerFunc() {				// 5	
          		console.log("innerFunc: Inside else");
      		}
      		var innerFuncExpr = function () {	// 6
      		
          		console.log("innerFuncExpr: Inside else");
      		}
      	}

	   	innerFunc();							// 7
		innerFuncExpr();						// 8
		
	})();
	
```

###### A: 

```
	innerFunc: Inside else
	innerFuncExpr: Inside if

```

###### Explanation

1. There are two types of functions inside the `if else` blocks. The `innerFunc` is the commonly known function declaration and `innerFuncExpr` is the function expression. At any point of time, only one of the `if` or `else` block should get executed, in this case the `if` block at #`1`. 
2. But the first `console.log` output for the invocation at #`7` suggests as if the `else` block `innerFunc` is getting executed. To understand this behaviour, we have to know the concept of JavaScript Hoisting. Here though the function `innerFunc` is declared within both the `if` and the `else` block, the JS engine hoists the function declarations to the top of the enclosing function.
3. Efectively there is only one function declaration and that is the one which JS engine encounters last during the parsing phase. So, in this case the else block `innerFunc` overwrites the `if` block declaration, irrespective of where the declarations are within the conditional blocks, there is only one `innerFunc` declaration and hence the output of the invocation at #`7`
4. The `innerFuncExpr` is the function expression, which does not get hoisted to the top of the enclosing function scope. So, we see the appropriate `console.log` output for the invocation at #`8`.

###### Suggestions

1. Do not declare the functions or the variables within the conditional blocks as JS does not ensure block scope. In fact, going by JS specs function declarations are not allowed within the conditional blocks, however different browsers allow (and interpret) them and hence, we do not get the error.
2. If required, use function expression instead within the conditional blocks.

###### Links

1. [Kangax on Named Function Expressions](https://kangax.github.io/nfe/)
