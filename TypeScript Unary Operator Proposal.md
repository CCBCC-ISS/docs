# Deprecate ++ and -- operators
Author: [Daniel Strokis](https://github.com/talzag)

## Introduction
* The unary operators `++` and `--` are no longer necessary.

## Reasons to Deprecate

* Many posts on stackoverflow discussing the subtleties of these operators, indicating the confusion among developers that these operators cause.

* Sometimes the results these operators give is [unexpected](http://stackoverflow.com/questions/13565217/javascript-increment-while-assigning).
	```javascript
		var v = 0;
		v = ++v + ++v + ++v;
		// v = 6
	```

* Many languages do not support these operators, or are dropping support for them.
	* Python
	* [Swift 3.0](https://github.com/apple/swift-evolution/blob/master/proposals/0004-remove-pre-post-inc-decrement.md)

* Don't encourage a consistent coding style:
	```javascript
		// Not consistent
		x++; 
		x += 2; 
		x += 3;
	
		// Consistent
		x += 1; 
		x += 2; 
		x += 3;
	```

* To quote [Chris Lattner](https://github.com/apple/swift-evolution/blob/master/proposals/0004-remove-pre-post-inc-decrement.md): 

	> Code that actually uses the result value of these operators is often confusing and subtle to a reader/maintainer of code. They encourage "overly tricky" code which may be cute, but difficult to understand.

* Douglas Crockford [recommends against using them](http://www.youtube.com/watch?v=_EANG8ZZbRs&t=42m25s)

## Reasons to Keep
* Any valid JavaScript must be valid TypeScript

## Proposed Solution
* Modify `emitter.ts`

## Alternatives to Deprecation
* Keep TypeScript compiler as-is, no changes required.
 

---
See the [recommendations](https://github.com/Microsoft/TypeScript/wiki/Writing-Good-Design-Proposals) on writing proposals.
See the TypeScript team's [design goals](https://github.com/Microsoft/TypeScript/wiki/TypeScript-Design-Goals).