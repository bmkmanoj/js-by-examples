## Comma operator

###### Q: What is the output?

```js

	(function() {
		var myVarOne = [10, 20, 30, 40][1, 2, 3];
		var myVarTwo = [10, 20, 30, 40][3, 2, 1];

		console.log("myVarOne = "+myVarOne);
		console.log("myVarTwo = "+myVarTwo);
	})();
	￼	
```

###### A: 

```		
	myVarOne = 40
	myVarTwo = 20

```

###### Explanation

1. At first look it may seem like two arrays in conjunction. But the second brackets are evaluated using comma operator and not considered like an array. The first one is indeed an array.
2. When we look at `myVarOne`,  the last value `[1, 2, 3]` is considered or evaluated as 3. Hence like an array `myVar[1, 2, 3]` as if it were equivalent to `myVar[3]`. However, this is not entirely true. The parsing happens as follows: 
	
	```
		var myVarOne = [10, 20, 30, 40][((1, 2), 3)];
		var myVarTwo = [10, 20, 30, 40][((3, 2), 1)];
	
	```
3. When [10,20,30,40][1,2,3] is parsed, [ is understood as the start of the array or object property accessor. Hence the expression inside the accessor is simply treated as a vanilla expression with the comma operator. The confusion mainly lies in that the reader expects [1,2,3] to be an array literal as well.
4. The comma operator can be mostly seen as used in the multiple variable declaration a.k.a. single var pattern.

###### Link

1.	[MDN on comma operator](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Operators/Comma_Operator)
2.      [Single var pattern](http://sixrevisions.com/javascript/single-var-pattern)
