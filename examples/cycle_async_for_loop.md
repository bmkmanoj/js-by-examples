## Asynchronous for cycle in JavaScript

###### Q: What is the output?

```js
    function async(i, func, callback) {
        var index = 0;
        var done = false;
        var loop = {
            next: function() {
                if (done) {
                    return;
                }

                if (index < i) {
                    index++;
                    func(loop);

                } else {
                    done = true;
                    callback();
                }
            },

            iteration: function() {
                return index - 1;
            },

            break: function() {
                done = true;
                callback();
            }
        };
        loop.next();
        return loop;
    }



	￼	
```

###### Calling the function:

```js
$('input[type=button]').click( function() {
        async(10, function(loop) {

           testFunction(1, 2, function(result) {

              console.log(loop.iteration());

              loop.next();
          })},
          function(){console.log('cycle ended')}
      );
    });

     function testFunction(a, b, callback) {
            console.log('Doing iterations!');
            callback();
        }
);

```

###### Explanation

1. The decoupling of the caller from the response allows for the JavaScript runtime to do other things while waiting for your asynchronous operation to complete and their callbacks to fire.
2. The Async function recives the number of iterations in the i variable.
3. While index value is lower than i, the loop function  will continue to run until callback is called.

###### Link

1.	    [JsFiddle Example](https://jsfiddle.net/mcasanova/1awzgvL6/4/)
