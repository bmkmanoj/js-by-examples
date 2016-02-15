## Functions inside methods and this variable

###### Q: What is the output?

```js

	var myself = {
		myName: 'Manoj',
		myNickNames: [ 'Minko', 'BMK' ],
		printMyNickNames: function () {
			'use strict';
			this.myNickNames.forEach(
				function (nickName) {  // 1
					console.log(this.myName +' is also known as '+ nickName);  // 2
            	}
        	);
    	}
	};
	
	myself.printMyNickNames();
	
```

###### A: 

```	

	Uncaught TypeError: Cannot read property 'myName' of undefined
	
```

###### Explanation

1. It did not print "Manoj is also known as Minko/BMK". As you might have expected, the `this` context to get set at the object level scope inside the function at #`1`, so that it could access `myName` via `this.myName`. But, clearly it does not. We see that the `this` is set to `undefined`. Here, the function at #`1` is nested within the `printMyNickNames` method of the `myself` object. What we are trying here is to access the `this` context of `printMyNickNames` (effectively the `myself` object) within the function in the loop at #`1`.
2. Now, the function at #`1` itself has its own `this` context, and thats why it shadows the `this` context of the method `printMyNickNames` and also, as we are using the `use strict` within the method, the `this` context for the function at #`1` is set to `undefined`. On a side note, when we run the above code in the non strict mode, `this` object for the function at #`1` is set to the the global object i.e. the `window` object (try running the above code after commenting the `use strict` part and see it for yourself).
3. A thing to note here is because `this` is a special variable, the lexical scope chaining is not applicable to `this`. This is the biggest difference to the normal variables  declared via `var` and the `this` variable. 
4. To overcome *this* problem ( ~pun~ intended :) ), we need to bind the appropriate context to `this`. We can also cache the `this` variable to another temporary variable and use it to access the original `this` object members. The following code snippets illustate this, both of these would print the appropriate `console.log`s at #`2`.
	
	```js
	
		// One way to bind appropriate context to this
		
		var myself = {
			myName: 'Manoj',
			myNickNames: [ 'Minko', 'BMK' ],
			printMyNickNames: function () {
				'use strict';
				this.myNickNames.forEach(
					function (nickName) {  // 1
						console.log(this.myName +' is also known as '+ nickName);  // 2 - prints appropriately 
            		}.bind(this)
        		);
    		}
		};
	
		myself.printMyNickNames();
	
		
	
		// Another way, using "var that = this" technique

		var myself = {
			myName: 'Manoj',
			myNickNames: [ 'Minko', 'BMK' ],
			printMyNickNames: function () {
				'use strict';
				var that = this;
				this.myNickNames.forEach(
					function (nickName) {  // 1
						console.log(that.myName +' is also known as '+ nickName);  // 2 - prints appropriately 
            		}
        		);
    		}
		};
	
		myself.printMyNickNames();
	
	```
5. Few methods also support passing of context. Here, `this` can be sent as an additional parameter to the method and the method will bind it directly.
    ```js
        
		var myself = {
			myName: 'Manoj',
			myNickNames: [ 'Minko', 'BMK' ],
			printMyNickNames: function () {
				'use strict';
				this.myNickNames.forEach(
					function (nickName) {  // 1
						console.log(this.myName +' is also known as '+ nickName);  // 2 - prints appropriately 
            		},
            		this // 2nd parameter as context.
        		);
    		}
		};
	
		myself.printMyNickNames();
    ```
    Here is a minimalistic version of *forEach* function :
    ```js
        function forEach(array, callback, context) {
            var length = array.length;
            var i = 0;
            
            for(i; i < length; i++){
                callback.apply(context, [array[i], i, array]);
            }
        }
    ```
6. Use of arrow funtions from ES6, makes it even better.
    ```js
		var myself = {
			myName: 'Manoj',
			myNickNames: [ 'Minko', 'BMK' ],
			printMyNickNames: function () {
				'use strict';
				this.myNickNames.forEach(
				    nickName => console.log(this.myName + ' is also known as ' + nickName);
				);
    		}
		};
	
		myself.printMyNickNames();
    ```
###### Links

1. [StackOverflow question on that equals to this](http://stackoverflow.com/questions/4886632/what-does-var-that-this-mean-in-javascript?rq=1)
2. [StackOverflow question on this variable](http://stackoverflow.com/questions/3127429/how-does-the-this-keyword-work?rq=1)
