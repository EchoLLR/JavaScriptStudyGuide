
##  Function Definition
A function **definition** is a regular binding where the value of the binding is a function.
```javascript
const square = function(x) {
  return x * x;
};
```
## Function Declaration
There is a slightly shorter way to create a function binding. This is a function **declaration**.
```javascript
function square(x) {
  return x * x;
}
```
## Arrow functions

 - When there is only ==one parameter== name, you can omit the parentheses around the ==parameter list==. If the body is a single expression, rather than a block in braces, that ==expression== will be returned from the function. Thus,  `square2` and `square3` definitions are equivalent.
 - When an arrow function has no parameters at all, its parameter list is just an empty set of parentheses as in 	`square4`.

```javascript
// Syntax:
 1. const square1 = (x,y) => { return x * x; }; 
 2. const square2 = (x) => {return x * x; }; 
 3. const square3 = x => x * x; 
 4. const square4 = () => { return 1*1;};
```
##  Bindings and scopes
Each binding has a _scope_, which is the part of the program in which the binding is visible.

Bindings declared with `let` and `const` are in fact local to the _block_ that they are declared in.
```javascript
if (true) {
  let x = 20;
  var y = 30;
}
// x is not visible here but y is visible
console.log(x + y);
```
## Optional Arguments
The following code is allowed and executes without any problem:
```javascript
function square(x) { return x * x; }
console.log(square(4, true, "hedgehog"));
```
JavaScript is extremely broad-minded about the number of arguments you pass to a function. If you pass too many, the extra ones are ignored. If you pass too few, the missing parameters get assigned the value `undefined`.

If you write an `=` operator after a parameter, followed by an expression, the value of that expression will replace the argument when it is not given (default parameter).
```javascript
function power(base, exponent = 2) {
  let result = 1;
  for (let count = 0; count < exponent; count++) {
    result *= base;
  }
  return result;
}

console.log(power(4)); // → 16
console.log(power(2, 6)); // → 64
```
