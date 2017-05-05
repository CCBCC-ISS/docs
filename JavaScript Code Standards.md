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

## Strict mode

Strict mode helps prevent a certain class of bugs from being introduced into our code. 

* Always include the `'use strict'` pragma in your code. Alternatively, you can set the setting the `alwaysStrict` compiler option to `true` for a TypeScript project.

```javascript
    // in myFile.js
    // applies strict mode to global scope
    'use strict';
    
    (function () {
        // applies strict mode only to current function scope
       'use strict';
       
       //...
    }());
```

## Comparing and Equality

It's a common pattern in languages like C# to check for null like

```csharp
    if (myObj == null) {
        // do something with myObj
    }
```

In JavaScript, the above code is legal, but it may give unexpected results.

There are two equality comparison operators in JavaScript, `==` (equality) and `===` (strict equality). Strict equality doesn't type cast.

Because of the JavaScript type system, you can check for `null`, `undefined`, or `0` as if it were a boolean check.

```javascript
    // conditional check casts value of myObj to a boolean
    if (myObj) {
        // do something with myObj
    }
```

You can also take advantage of the type system to be sure that an object is not `null` or `undefined` by "double casting" it's value to a boolean.

```javascript
    /*
     * !myObj casts value to boolean
     * 
     * if myObj is not undefined or null, !myObj => false, e.g.
     * !!myObj => !(false) => true
     * 
     */
    
    if (!!myObj) {
        // do something with myObj
    }
```

* Always use `===` (strict equality comparison) when comparing values. If you use `==`, document why it was necessary.

## IIFE

* Immediately invoked function expressions should have their argument parenthese inside of the enclosing parentheses.

```javascript
    // Wrong
    (function () {
        //...
    })();
    
    // Correct
    (function () {
        
    }());
```

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
and many other languages such as Python and Swift don't even have support for these operators. Avoiding these 
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
    for (const letter of arr) {
        console.log(letter); // 'letter' is set to 'a'
    }
```

* There is a little-known syntax of `for...in` that can be incredibly useful and even elegant at times.

```javascript
    const myObj = {a: 1, b: 2, c: 3}; 
    let myKeys = [], 
        i = 0;
     
    for (myKeys[i++] in myObj);
     
    myKeys; // ['a','b','c'];
```

Read [this](https://javascriptweblog.wordpress.com/2011/01/04/exploring-javascript-for-in-loops/) for more information about `for...in` loops.

---

## TypeScript
### `const`, `let`, `var`

* Always declare variables `const` when possible. If a variable will be written to, declare it with `let`. If you must use `var`, add a comment documenting why `var` was necessary in that special case.

### Type Inference

* Let the TypeScript compiler help you write less code. If you assign a value to a variable when you declare it, you don't need to give it an explicit type.

```javascript
    // Correct
    const myString = "A string"; // String type
    let someObj = {}; // Object type

    // Wrong
    const myArray: Array = []; // unnecessary  
```
