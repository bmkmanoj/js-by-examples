## Grouping operator

######Q: What is the output?

```js

	function myFunc(myVar) { 
		console.log(arguments);
```

######A: 

```		
	3

```

######Explanation

1. At first look it may seem like an IIFE, but it is not. Here, `myFunc` is a *function declaration* form and not `function expression`.
2. The returned value is coming not from the `console.log` but the code following the function declaration as you see, the function is not getting invoked here. It is a grouping operator (i.e. open close parenthesis) for the numbers inside it. Essentially, the code above is going to be parsed like:
	```js
		
		function myFunc(myVar) { 
			console.log(arguments);

	```

######Link

1.	[MDN on grouping operator](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Grouping)