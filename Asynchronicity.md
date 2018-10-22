## Asynchronicity
>Notes based on: [Eloquent JavaScript 3rd edition](http://eloquentjavascript.net/).

An _asynchronous_ model allows multiple things to happen at the same time. When you start an action, your program continues to run. When the action finishes, the program is informed and gets access to the result (for example, the data read from disk).

One approach to asynchronous programming is to make functions that perform a slow action take an extra argument, a _callback function_. The action is started, and when it finishes, the callback function is called with the result.

As an example, the `setTimeout` function, waits a given number of milliseconds and then calls a function.
```javascript
setTimeout(() => console.log("Tick"), 5000);
```

## Promises
In the case of asynchronous actions, you could, instead of arranging for a function to be called at some point in the future, return an object that represents this future event.

This is what the standard class  `Promise`  is for. A `promise` is an asynchronous action that may complete at some point and produce a value. It is able to notify anyone who is interested when its value is available.
```javascript
let fifteen = Promise.resolve(15);
fifteen.then(value => console.log(`Got ${value}`));
```
To get the result of a promise, you can use its `then` method. This registers a callback function to be called when the promise resolves and produces a value. You can add multiple callbacks to a single promise, and they will be called, even if you add them after the promise has already _resolved_ (finished).


## Failure
Regular JavaScript computations can fail by throwing an exception. Asynchronous computations often need something like that.

![](https://mdn.mozillademos.org/files/15911/promises.png)

A `Promise` object is created using the `new` keyword and its constructor. This function should take two functions as parameters. The first of these functions (`resolve`) is called when the asynchronous task completes successfully and returns the results of the task as a value. The second (`reject`) is called when the task fails, and returns the reason for failure, which is typically an error object.

When a handler throws an exception, this automatically causes the promise produced by its `then` call to be rejected. So if any element in a chain of asynchronous actions fails, the outcome of the whole chain is marked as rejected, and no success handlers are called beyond the point where it failed.

The chains of promise values created by calls to `then` and `catch` can be seen as a pipeline through which asynchronous values or failures move.
```js
function myAsyncFunction(url) {
  return new Promise((resolve, reject) => {
    const xhr = new XMLHttpRequest();
    xhr.open("GET", url);
    xhr.onload = () => resolve(xhr.responseText);
    xhr.onerror = () => reject(xhr.statusText);
    xhr.send();
  });
}
```
The chains of promise values created by calls to `then` and `catch` can be seen as a pipeline through which asynchronous values or failures move.
```js
new Promise((_, reject) => reject(new Error("Fail")))
  .then(value => console.log("Handler 1"))
  .catch(reason => {
    console.log("Caught failure " + reason);
    return "nothing";
  })
  .then(value => console.log("Handler 2", value));
```

The `Promise.all(iterable)` method returns a single `Promise`. The Promise object represents the eventual completion (or failure) of an asynchronous operation, and its resulting value) that resolves when all of the promises in the `iterable` argument have resolved or when the iterable argument contains no promises. It rejects with the reason of the first promise that rejects.
```js
var promise1 = Promise.resolve(3);
var promise2 = 42;
var promise3 = new Promise(function(resolve, reject) {
  setTimeout(resolve, 100, 'foo');
});

Promise.all([promise1, promise2, promise3]).then(function(values) {
  console.log(values);
});
// expected output: Array [3, 42, "foo"]
```
## The event loop
Callbacks are not directly called by the code that scheduled them. If I call `setTimeout` from within a function, that function will have returned by the time the callback function is called. And when the callback returns, ==control does not go back to the function that scheduled it==.

Asynchronous behavior happens on ==its own empty function call stack==. This is one of the reasons that, without promises, managing exceptions across asynchronous code is hard. Since each callback starts with a mostly empty stack, your `catch` handlers won’t be on the stack when they throw an exception.
```js
try {
  setTimeout(() => { throw new Error("Woosh");},20);
} catch (_) {
  // This will not run
  console.log("Caught!");
}
********************
Promise.resolve("Done").then(console.log);
console.log("Me first!");
// → Me first!
// → Done
```

