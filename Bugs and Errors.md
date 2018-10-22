## Bugs and Errors
>Notes based on: [Eloquent JavaScript 3rd edition](http://eloquentjavascript.net/).

"Debugging is twice as hard as writing the code in the first place. Therefore, if you write the code as cleverly as possible, you are, by definition, not smart enough to debug it."
-Brian Kernighan and P.J. Plauger,  *The Elements of Programming Style*

![Picture of a collection of bugs](http://eloquentjavascript.net/img/chapter_picture_8.jpg)

## Strict mode
JavaScript can be made a _little_ stricter by enabling _strict mode_. This is done by putting the string `"use strict"` at the *top of a file* or a *function body*. Without `"use strict"` , the following code is allowed.
```javascript
function Person(name) { this.name = name; }
let ferdinand = Person("Ferdinand"); // oops
console.log(name);
// → Ferdinand
```
## Exceptions
The `try` and `catch` functionalities stay the same as in C++ or other languages.
```javascript
function Direction(question) {
  let result = prompt(question);
  if (result.toLowerCase() == "left") return "L";
  if (result.toLowerCase() == "right") return "R";
  throw new Error("Invalid direction: " + result);
}

try {
  console.log("You see",Direction("Which way?"));
} catch (error) {
  console.log("Something went wrong: " + error);
}
```
There is another feature that `try` statements have. They may be followed by a `finally` block either instead of or in addition to a `catch` block. A `finally` block says “no matter _what_ happens, run this code after trying to run the code in the `try` block.”
```javascript
try {
  console.log("You see",Direction("Which way?"));
} finally {
  console.log("Go home!");
}
```
We can define the type of error and use `instanceof` to identify it.
```javascript
class InputError extends Error {}

function Direction(question) {
  let result = prompt(question);
  if (result.toLowerCase() == "left") return "L";
  if (result.toLowerCase() == "right") return "R";
  throw new InputError("Invalid direction: " + result);
}

try {
  console.log("You see",Direction("Which way?"));
} catch (er) {
	if (e instanceof InputError) {
      console.log("Not a valid direction. Try again.");
    } else {
      throw e;
    }
}
```
