## Time for some Timeout

###### Q: What is the output?

```js

	￼(function() {
    	console.log(1);				// 1
    	setTimeout(function() {
    		console.log(2)			// 2
    	}, 2000);
    	 
    	setTimeout(function() {
    		console.log(3)			// 3
    	}, 0); 
    	console.log(4);				// 4
	})();
￼	
```

###### A: 

```	
	
	1
	4
	3
	2

```

###### Explanation

1. The first two `console.log` prints may be obvious as they are basic invocation of `console.log` without any delay. But should not the log at #`3` print just after #`2` as the time delay provided there is 0 msecs?
2. To understand this, we need to understand how events and timers are handled in JS through event loop.  The browser basically has a place holder for queuing up the events before processing them. So `setTimeout` puts the execution of the anonymous function into the event queue. After that, it is the browsers responsibility to run it when it gets free.
3. So, when a value of zero is passed as the second argument to `setTimeout`, though it seems like it should get executed immediately, actually the execution of the function is placed on the event queue to occur on the next timer tick. So the function is not executed until the next tick. That’s why the log at #`4` occurs before the log at #`3` (since the `console.log` is invoked via `setTimeout`, so it is slightly delayed).


###### Links
1. [Events and timing in-depth](http://javascript.info/tutorial/events-and-timing-depth)
2. [Timeout jsfiddle example](https://jsfiddle.net/mcasanova/2bt1jx1h/)
