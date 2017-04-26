## Extracted method and bind

###### Q: What is the output?

```js

	var myObject = {
    		myCountryName: 'India',
    		getMyCountryName: function (){			   // 1
        		return this.myCountryName;
    		}
	};

	var countryInfo = myObject.getMyCountryName;  // 2

	console.log(countryInfo());	                  // 3
	console.log(myObject.getMyCountryName());	  // 4
	
```

###### A: 

```	
	
	undefined
	India	

```

###### Explanation

1. The `console.log` at #`3` prints `undefined` as we have extracted the method from the `myObject` object. So when we invoke `countryInfo`, effectively we are invoking `getMyCountryInfo` method of `myObject` in the global context. In this case, the `this` variable is the `window` object.
2. As the property `myCountryName` doesn't exist in the `window` object, we see the `undefined` getting printed at #`3`. However, the printed output at #`4` is as expected. Here, the `this` variable is set to `myObject` and hence the appropriate info is getting printed.
3. One way to overcome the inappropriate object binding is to explicitly bind the object on which we wish to invoke the extracted method while defining `countryInfo` like

	```js
		
		var countryInfo = myObject.getMyCountryName.bind(myObject);
		
	``` 
