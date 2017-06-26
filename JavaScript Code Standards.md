# CCBCC JavaScript Code Standards

These rules are used in JavaScript code linting (codified through either `.jshintrc` or `.eslintrc` files, 
or through the `jshintConfig` property in a project's `package.json`).

Linting is the process of flagging anything suspicious looking in source code. Suspicious, in this case, being
constructs and statements that are syntactially legal but violate coding standards, commonly introduce bugs, 
make the code less maintainable, or otherwise cause headaches for develoeprs.

See the entry on the tool [lint](https://en.wikipedia.org/wiki/Lint_%28software%29) for more information.

---

`eval` is a way to execute raw JavaScript source code within a JavaScript context.

```javascript
    //myFile.js

    var source = 'var foo() { }';
    eval(source);
```

`eval` has the same privilages as it's caller. If any of the input to `eval` is touched by a third-party it could be compromised and you could
be running malicious code.

`eval` is almost always slower than it's alternativs (`eval`ed code is interpreted, and interpreters are the bottom tier of JS engines).

* Never use `eval`.


JavaScript doesn't <i>require</i> semicolons, but a missing semicolon can lead to strange results. 

* Always end lines with a semicolon.


Even though JavaScript engines try to be smart, sometimes they can still get things wrong. If a curly brace is not on the same line as a function declaration,
the engine might interpret the declaration as invocation. 

In addition, it can be very easy to write several statements after a control flow statement.

* Always use curly braces, even for single line conditional statements, on the same line as the conditional statement.

```javascript
    // Wrong
    if (foo) 
        bar();
        baz(); // baz will get call regardless of the truthiness of foo
    
    if (foo)
    {
        bar();
    }

    // engine may see this as calling myFunc
    myFunc()
    {
        //...
    }
    
    // Correct
    if (foo) {
        bar();
    }

    if (foo) { bar(); }
``` 

---

Strict mode helps prevent a certain class of bugs from being introduced into our code. 

* Always include the `'use strict'` pragma in your code. 

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

---

It's a common pattern in languages like C# to check for null like this:

```csharp
    if (myObj == null) {
        // do something with myObj
    }
```

In JavaScript, the above code is legal, but it might give unexpected results.

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

* Use camel casing for variable names and Pascal casing for class names.
```javascript
    let myVar = 42;

    class MyClass = {};
```

---

* Use ES6 syntax where possible. 

*Note* ES6 syntax is <i>*not*</i> supported in Internet Explorer. If you must support a legacy application you should either avoid ES6 features or transpile your code to ES5.

The `class` keyword and syntax is syntactic sugar over the typical function declaration style.
```javascript
    class MyClass {
        constructor() {
            this._prop = 42;
        }
        
        // classes can have static properties available to all instances
        // MyClass.classProp
        static classProp = 'a static variable';

        // classes can have properties and methods
        myFirstProperty = "bar";
        
        myMethod() {
            return "foo";
        }

        // classes can have getters and setters for properties
        get myProp {
            return this._prop;
        }
        
        // you can put custom logic in getters and setters
        set myProp(val) {
            this._prop = val * 2;
        }
    }
    
    // VS.

    var MyClass = function () {
        this._prop = 42;
    };

    MyClass.prototype.myMethod = function () {
        return "foo";
    };
    // etc...
```

`const` declares a constant and requires a value at initialization.

`let` declares a variable that obeys block scoping.

* Use `const` and `let` instead of `var`. If you <i>must</i> use `var`, add comments explaining why it's needed.

```javascript
    const kGLOBAL_ID = 1000000;

    const id = function () {
        let x = Math.rand();

        return x * kGLOBAL_ID;
    };
```

Arrow functions are more concise than using the `function` keyword. 

* Use arrow functions for non-method functions.

```javascript
    [0, 1, 2, 3, 4].map(n => n * 2);
    // [0, 2, 4, 6, 8]
```

