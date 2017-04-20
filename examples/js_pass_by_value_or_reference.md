## Pass by value or reference

###### Q: What is the output?

```js

	var me = {					// 1
		'partOf' : 'A Team'
	}; 

	function myTeam(me) {		// 2

		me = {					// 3
			'belongsTo' : 'A Group'
		}; 
	} 
	
	function myGroup(me) { 		// 4
		me.partOf = 'A Group'; // 5
	} 
	
	myTeam(me);		
	console.log(me);			// 6
	
	myGroup(me);
	console.log(me);			// 7
	
```

###### A: 

```	
	
	{'partOf' : 'A Team'}
	{'partOf' : 'A Group'}
	

```

###### Explanation

1. JavaScript is pass-by-value, technically. It is neither pass-by-value or pass-by-reference, going by the truest sense of these terms. When the `myTeam` gets invoked, JavaScript is *passing the reference to* `me` *object as value, as it is an object* and invocation itself creates two independent references to the same object, (though the name being same here i.e. `me`, is misleading and gives us an impression that it is the single reference) and hence, the reference variable themselves are independent.
2. When we assigned a new object at #`3`, we are changing this reference value entirely within the `myTeam` function, and it will not have any impact on the original object outside this function scope, from where it was passed and the reference in the outside scope is going to retain the original object and hence the output from #`6`.
3. In the case of `myGroup` invocation, we are passing the object `me`. But unlike the above scenario, we are not assigning this variable to any new object, effectvely meaning the object reference value within the `myGroup` function scope still is the original object's reference value and when we are modifying the property within this scope, it is effectively modifying the original object's property. Hence, you get the output from #`7`.
4. So does this later case not prove that javascript is pass-by-reference? No, it does not. Remember, *JavaScript passes the reference as value, in case of objects*. The confusion arises as we tend not to understand fully what pass by reference is. This is the exact reason, some prefer to call this as *call-by-sharing*. 

###### Links

1. [StackOverflow question on this topic](http://stackoverflow.com/questions/518000/is-javascript-a-pass-by-reference-or-pass-by-value-language)
2. [JavaScript, pass by value or reference?](http://nsono.net/javascript-pass-by-value-or-pass-by-reference/)
