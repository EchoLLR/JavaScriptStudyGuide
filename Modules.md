## Modules
>Notes based on: [Eloquent JavaScript 3rd edition](http://eloquentjavascript.net/).

A module is a piece of program that specifies which other pieces it relies on and which functionality it provides for other modules to use (its _interface_). 

They make part of the module available to the outside world and keep the rest private. By restricting the ways in which modules interact with each other, the system becomes more like LEGO, where pieces interact through well-defined connectors.

The relations between modules are called _dependencies_. To separate modules, each needs it own private scope.

## Packages
A package is a chunk of code that can be distributed (copied and installed). It may contain one or more modules and has information about which other packages it depends on.

We need a place to store and find packages and a convenient way to install and upgrade them. In the JavaScript world, this infrastructure is provided by [NPM](https://npmjs.org/). NPM is an online service where one can download (and upload) packages and a program (bundled with Node.js) that helps you install and manage them.

## CommonJS
The most widely used approach to bolted-on JavaScript modules is called  _CommonJS modules_. Node.js uses it and is the system used by most packages on NPM.

The main concept in CommonJS modules is a function called  `require`. When you call this with the module name of a dependency, it makes sure the module is loaded and returns its interface.

Because the loader wraps the module code in a function, modules automatically get their own local scope. All they have to do is call  `require`  to access their dependencies and put their interface in the object bound to  `exports`.

```javascript
// ordinal: to convert numbers to strings like "1st" and "2nd"
// date-names to get the English names for weekdays and months.
const ordinal = require("ordinal");
const {days, months} = require("date-names");
// export formatDate function
exports.formatDate = function(date, format) {
  return format.replace(/YYYY|M(MMM)?|Do?|dddd/g, tag => {
    if (tag == "YYYY") return date.getFullYear();
    if (tag == "M") return date.getMonth();
    if (tag == "MMMM") return months[date.getMonth()];
    if (tag == "D") return date.getDate();
    if (tag == "Do") return ordinal(date.getDate());
    if (tag == "dddd") return days[date.getDay()];
  });
};
```
## ECMAScript modules
_ES modules_, where _ES_ stands for ECMAScript is a different module system. The main concepts of dependencies and interfaces remain the same, but the details differ.
```javascript
import ordinal from "ordinal";
import {days, months} from "date-names";

export function formatDate(date, format) { /* ... */ }
```
It is possible to rename imported bindings using the word  `as`.
```javascript
import {days as dayNames} from "date-names";
console.log(dayNames.length);
```
