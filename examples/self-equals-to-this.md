## Self equals to this

###### Q: What is the output?

```js

	var myObject = {
	    myName: "Minkowsky",
    	myFunc: function() {
        	var self = this;		// 1
        	console.log("outer func:  this.myName = " + this.myName);
        	console.log("outer func:  self.myName = " + self.myName);
        	(function() {
            	console.log("inner func:  this.myName = " + this.myName);
            	console.log("inner func:  self.myName = " + self.myName);
        	}());
    	}
	};
	myObject.myFunc();

```

###### A: 

```	
	
	outer func:  this.myName = Minkowsky
	outer func:  self.myName = Minkowsky
	inner func:  this.myName = undefined
	inner func:  self.myName = Minkowsky
	
```

###### Explanation

1. The outer function output is straight forward. Both `this` and `self` refer to `myObject` and therefore both can properly reference and access myName.
2. However, in the inner function (the IIFE), the `this` is not referring to the `myObject` anymore, its the inner function scope rather. So, `this.myName` is `undefined` within the inner function, whereas the reference to the local variable `self` remains in the scope and hence, accessible there.
3. The #`1` is a technique used to cache the outer function's `this` reference to another variable (like `self` / `that`) and by doing so, it becomes available to the inner function via lexical scope chain.


###### Links:
1. [Stackoverflow on self equals to this pattern](http://stackoverflow.com/questions/337878/var-self-this)
