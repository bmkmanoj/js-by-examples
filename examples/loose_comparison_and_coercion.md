## Loose comparison and coercion

###### Q: What is the output?

```js
	
	(function () {
		falseString = "false";		// 1
		if(true) {				
			var falseString;		// 2
			if(falseString) {		// 3
				console.log(falseString == true);	// 4
				console.log(falseString == false);  // 5
			}
		}
	})();
	￼	￼	
```

###### A: 

```	js

	false
	false

```

###### Explanation

1. There are four concepts involved in this. Hoisting, scoping, type coercion of boolean expressions and type coercion while loose comparison. The variable declaration of `false` at #`2` is hoisted to the top of the function, hence the it is not having `undefined` rather it has the assigned string `falseStr` value (from #`1`).
2. Also, the scope in JS is at the function level and not the block level. Next, we see at #`3` the boolean expression and type coercion comes into play. The string is a non empty one and it gets coersed to `true` (though the string value `"false"` as such seems to suggest it should be coerced as `false` but it is not) according to the rules.
3. The crucial part comes as two `console.log`s where the type coercion happens but this time, in terms of loose comparison with `==`. When JavaScript does a loose comparison on a `Boolean` and a `String`, it attempts to convert them both to a `Number` before doing a strict comparison. The logs can be rewritten as follows:

	```js
		
		console.log(Number(falseStr) == Number(true));  //console.log(NaN == 1);
		console.log(Number(falseStr) == Number(false)); //console.log(NaN == 0);
		
	```
4. This explains why both the statements are printing `false`.

##### Links

1.	[Scoping and hoisting](http://www.adequatelygood.com/JavaScript-Scoping-and- Hoisting.html)
2.	[MDN on Functions](https://developer.mozilla.org/en- US/docs/Web/JavaScript/Reference/Functions)
3.	[ES5 Spec on Boolean expression in if condition](http://www.ecma-international.org/ecma-262/5.1/#sec-12.5)
4.	[ES5 spec on loose comparisons](http://www.ecma-international.org/ecma- 262/5.1/#sec-11.9.3)
