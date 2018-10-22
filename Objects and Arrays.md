## Data Structures: Objects and Arrays
>Notes based on: [Eloquent JavaScript 3rd edition](http://eloquentjavascript.net/).

`Object.assign` copies all properties from source object into target object.
```javascript
let objectA = {a: 1};
Object.assign(objectA, {a: 2; b: 3});
console.log(objectA);
// → {a: 2, b: 3}
```

 The `Object.create()` method creates a new object, using an existing object to provide the newly created object's `prototype` .
  ```javacript
const person = { isHuman: false }};
const me = Object.create(person);
```

Arrays: evaluate `typeof []` produces `"object"`.
 ```javascript
 let journal = [
  {events: ["work", "touched tree", "pizza",
            "running", "television"],
   squirrel: false}]
```
## Creating  a Reference
Consider the following code,  `object2` is created as reference to `object1`,  while `object3` and `object1` are two different objects with the same properties. 
```javascript
let object1 = {value: 10};
let object2 = object1;
let object3 = {value: 10};

console.log(object1 == object2);
// → true
console.log(object1 == object3);
// → false

object1.value = 15;
console.log(object2.value);
// → 15 since object2 is the refernence to object1
console.log(object3.value);
// → 10
```
## JSON
JSON looks similar to JavaScript’s way of writing arrays and objects, with a few restrictions. 
- All property names have to be surrounded by double quotes, and only simple data expressions are allowed—no function calls, bindings, or anything that involves actual computation. 
-  Comments are not allowed in JSON.

A journal entry might look like this when represented as JSON data:
```javascript
{
  "squirrel": false,
  "events": ["work", "touched tree", "pizza", "running"]
}
```
JavaScript gives us the functions `JSON.stringify` and `JSON.parse` to convert data to and from this format. `JSON.stringify` takes a JavaScript value and returns a JSON-encoded string. `JSON.parse` takes JSON-encoded string and converts it to the value it encodes.
```javascript
let string = JSON.stringify({squirrel: false, events:["weekend"]});
console.log(string);
// → {"squirrel":false,"events":["weekend"]}
console.log(JSON.parse(string).events);
// → ["weekend"]
```

