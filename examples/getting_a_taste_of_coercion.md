
## Getting a taste of coercion
 

###### Q: What would be the Output?

```js

function printHi() {

    var myVar = 5; 

    if(myVar == '5') {  // 1
        console.log("Hi, from if block")
    }
    
    switch(myVar){		// 2
        case '5':
        	console.log("Hi, from switch case block");        
    }
}

printHi(); 
```

##### A: 

```
> Hi, from if block
````

##### Explanation: 

There are basically two things to notice above. 

1. The if block (#`1`), compares the number `5` with the string `'5'` with double equals. JavaScript does coercion when comparing "things" using `==` and due to this coercion, the `console.log` within the if block gets executed. 
2. Is the coercion not applicable to switch case block (#`2`)? Well, the `console.log` within the `case` statement didn't get executed. Coercion is not application for variables within the switch statement as switches use strict type checking (`===`).

###### Links

1. [JavaScript Coercion](https://github.com/getify/You-Dont-Know-JS/blob/master/types%20%26%20grammar/ch4.md)
2. [Switch case and coercion](http://qfox.nl/notes/110)
3. [Stackoverflow question on comparison in JS switch statement](http://stackoverflow.com/questions/6989902/is-it-safe-to-assume-strict-comparison-in-a-javascript-switch-statement)
