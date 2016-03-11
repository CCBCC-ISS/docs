# CCBCC JavaScript Code Standards

These rules are used in JavaScript code linting (codified through either `.jshintrc` or `.eslintrc` files)

## Language-specific rules
* Never use `eval`.
* Always use curly braces, even for single line conditional statements.
	```javascript
	// Wrong
	if (foo) 
		bar();
	
	// Correct
	if (foo) {
		bar();
	}

	if (foo) { bar(); }
	``` 
---

## Spacing, Formatting and Syntax
* When declaring a top level function, include a space between the `function` keyword, the function name, and the arguments list.
* Include a space between the closing parentheses of the arguments list and the opening curly brace of the function body.
* When assigning a function to a variable, include a space between the `function` keyword (if present) and the arguments list.
* The opening curly brace of a function body goes on the same line as the function declaration. 
    ```javascript
	// Wrong
	function MyFoo(x, y){
		...	
	}

	function MyBar(x)
	{
		...
	}

	// Correct
	function MyFoo (x, y) {
		...
	};
	
	var foo = function (x, y) {
		...
	}; // always end function assignment with a semicolon

	var bar = (x, y) => {
		...
	};
	```

* Don't use postfix or prefix increment/decrement operators. These operators can cause confusion among developers, 
and many other languages such as Python and (soon) Swift don't even have support for these operators. Avoiding these 
operators encourages a more consistent coding style.
```javascript
	// Wrong 
	x++;
	x--;

	// Correct
	x += 1;
	x -= 1;
	
	// More consistent
	x += 1;
	x -= 2;
	x *= 3;
 
	// instead of
	x++;
	x += 2;
	x += 3;
```
--- 

## Language Clarification
### `for...of` vs.`for...in`
* `for...in` enumerates the keys of an object
```javascript
const arr = ['a', 'b', 'c', 'd'];
for (let key in arr) { 
	let localVar = arr[key]; // 'key' is set to 0
	...
}
```

* `for...of` enumerates the values of an object
```javascript
cost arr = ['a', 'b', 'c', 'd'];
for (let letter of arr) {
	console.log(letter); // 'letter' is set to 'a'
}
```
* There is a little-known syntax of `for...in` that can be incredibly useful and even elegant at times.
```javascript
var myObj = {a: 1, b: 2, c: 3}, myKeys = [], i=0;
 
for (myKeys[i++] in myObj);
 
myKeys; //['a','b','c'];
```
Read [this](https://javascriptweblog.wordpress.com/2011/01/04/exploring-javascript-for-in-loops/) for more information about `for...in` loops.