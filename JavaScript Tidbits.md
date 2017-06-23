# JavaScript Tips, Tricks, and Tidbits

Miscellaneous notes about JavaScript.

`for...in` enumerates the keys of an object

```javascript
    const arr = ['a', 'b', 'c', 'd'];
    for (let key in arr) { 
        let localVar = arr[key]; // 'key' is set to 0
        ...
    }
```

`for...of` enumerates the values of an object

```javascript
    cost arr = ['a', 'b', 'c', 'd'];
    for (const letter of arr) {
        console.log(letter); // 'letter' is set to 'a'
    }
```

There is a little-known syntax of `for...in` that can be incredibly useful and even elegant at times.

```javascript
    const myObj = {a: 1, b: 2, c: 3}; 
    let myKeys = [], 
        i = 0;
     
    for (myKeys[i++] in myObj);
     
    myKeys; // ['a','b','c'];
```

Read [this](https://javascriptweblog.wordpress.com/2011/01/04/exploring-javascript-for-in-loops/) for more information about `for...in` loops.

