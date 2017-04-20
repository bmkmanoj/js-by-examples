## About delete

###### Q: What is the output?

```js

	var myVar = 1;
	var output = (function(){
		delete myVar;
		return myVar;
	})();
	
	console.log(output);		// 1
	
	function MyFunc(){}
	MyFunc.prototype.bar = 42;
	var myFunc = new MyFunc();

	delete myFunc.bar;	
	console.log(myFunc.bar);	// 2

	delete MyFunc.prototype.bar;
	console.log(myFunc.bar);	// 3
	￼	
```

###### A: 

```		
	1
	42
	undefined

```

###### Explanation

1. The `delete` operator is useful when we wish to delete properties from an object. As `myVar` is a variable and not an object, at #`1` we see the  assigned value of `myVar` getting printed as `delete` has no effect on it.
2. Fair enough, but why is the log at #`2` printing the value? When we take a closer look at the `myFunc.bar`, it is an inherited property. So `delete` applied on an inherited property also has no effect and the existing value gets printed.
3. However, the last log at #`3` prints `undefined` as we have deleted the property directly on the prototype `MyFunc.prototype` because of which the property would no longer exist in the instance `myFunc` as well and hence the log at #`3`.

###### Link

1.	[MDN on delete](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/delete)
