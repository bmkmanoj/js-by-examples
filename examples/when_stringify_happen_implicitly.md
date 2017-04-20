## When Stringify happens implicitly

###### Q: What is the output?

```js

	var root = {};
    var elementOne = {key:'1'};
    var elementTwo = {key:'2'};

	root[elementOne] = "Element One"; 
	root[elementTwo] = "Element Two";

	console.log(root[elementOne]);

```

###### A: 


```		
	
	Element Two
	
```


###### Explanation


1. When setting an object property, JavaScript will internally convert the parameter/key using its `toString` and since here, we have objects as keys and since these object do not have their own implementation of `toString`, the default `Object.toString` method will be invoked.
2. In this case, both objects will be converted to "[object Object]". So `root[elementOne]`  and `root[elementTwo]` will be both equivalent to `root["[object Object]"]` and hence, will have the last assigned value. Effectively, `root[elementOne]` and `root[elementTwo]` will be referencing the same value.
3. We can verify that, if we override `toString` method in each of the `elementOne` and `elementTwo` objects, we will have a different behavior. Take a look at the following example.



	```js

		var root = {};
    	var elementOne = { 
    		key:'1',
    		toString: function() {
    			return '1';
    		}    	
    	};
    	
    	var elementTwo = {
    		key:'2',
    		toString: function() {
    			return '2';    		
    		}
    	};

		root[elementOne] = "Element One"; 
		root[elementTwo] = "Element Two";

		console.log(root[elementOne]);		// prints "Element One"

	```
