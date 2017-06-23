## TypeScript
### `const`, `let`, `var`

* Always declare variables `const` when possible. If a variable will be written to, declare it with `let`. If you must use `var`, add a comment documenting why `var` was necessary in that special case.

### Type Inference

* Let the TypeScript compiler help you write less code. If you assign a value to a variable when you declare it, you don't need to give it an explicit type.

```typescript
    // Correct
    const myString = "A string"; // String type
    let someObj = {}; // Object type

    // Wrong
    const myArray: Array = []; // unnecessary  
```

