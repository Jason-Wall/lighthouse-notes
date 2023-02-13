# W01

## Mentor Hours:


|Monday - Thursday  |	Friday      |   	Saturday|	Sunday|
|:--------------:   |:---:        |:---:        |:---:|
|12pm - 9pm	        |12pm - 6pm   |12pm - 4pm	  |not available|




## Gists and Repos

Gists are single serving repos for small projects - typically just one file. Great for sharing.\
Forking creates a copy of the gist/ repo unique to your github account.\
Clone a gist/ repo into your project by clicking on copying the SSH and entering the following in CLI:\
```
git clone <pasteSSH> <targetFolderName>
```

## Linting
We're using ESLint - Install and setup:
```
npm install -g eslint
```
Lighthouse has its own [ESLint](https://gist.github.com/kvirani/6cdb9511522d4357839718a050e7dd3b) file. Running the code below will install it.
```
cd ~
curl -o .eslintrc.json https://gist.githubusercontent.com/kvirani/6cdb9511522d4357839718a050e7dd3b/raw/.eslintrc.json
```
Command format:
```
eslint [options] file.js [file.js] [dir]
or
eslint --fix file.js
```

## Command Line Arguments
You can enter arguments to applications using the Node command line. example:
```
node <filename.js> arg1 arg2 [etc.]
```
 Refer to those arguments using ```process.argv```\
This returns an array containing the file location, and name in index 0 and 1.\

Use ```<array>.slice(2)``` to remove the first two elements.

## Truthy Falsey
All of the following are inherently falsey:
```js
False
0
""
null
undefined
NaN
```

## Comparing Arrays and Objects
We can't just equate arrays or objects - We need to check their stored values. 
## Primitives
* undefined
* null
* boolean
* string
* number
* symbol

## Objects
Keys/ properties and values. Keys are always strings.\
Use square-bracket when you need to pass in the value of the property ```<object>[variable]```\
Use dot notation if you know the string name of property ```<object>.<property>```\
Can store objects and functions as values of objects.\
A function stored in an object property is a method. 
```this``` refers to the object the function resides in (for now...)

## Useful Object Methods
* [Object.hasOwn(target)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/hasOwn) Checks to see if the object
* [Object.assign(target, source)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/assign) Copies all properties from a source to a target.

* [Object.keys(object)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/keys) Return all top layer keys in an object.
 Dive deeper by appending subkeys in the arguments.

## Callback Functions
Functions that are passed as parameters to other functions. A good example is the array Filter, Map, and Reduce functions. Of course we can create our own functions too.

## [VIM](https://web.compass.lighthouselabs.ca/days/w01d4/activities/280)
difficult to use... might as well go through it all over again.

## Closure
The idea that a function can always see it's parents scope. If you return a function from a function it will still maintain access to any variables that were available to the parent even if the parent
```js
function makeIdGenerator() {
  let id = 0;
  // The following is the closure function
  return function() {
    // This inner function accesses and assigns the value of
    // the variable id, which was defined in the parent function
    id += 1;
    return id;
  }
}

// makeIdGenerator returns a function which is assigned to
// the variable nextId
const nextId = makeIdGenerator(); /// anytime nextId is called it uses the id variable.
console.log(nextId()); // Logs: 1
console.log(nextId()); // Logs: 2
```
## Recursion
A technique where a function calls itself until a conditions is satisfied.\
Best to define a path that the program will follow if it's happy and one that requires recursion. More discussion on recursion later.


## Modules
Files have to export their functions/ objects if other files are to see them. Similarly files have to import to use outside information.
```js
//import to file:
const sayHelloTo = require('./myModule');// .js file extension optional

//export from file:
module.exports = sayHelloTo;
```
## Package Install for Unit Testing
Setup packages for projects from CLI:
1) Create a folder to work in, ```cd``` to it.
2) ```npm init -y``` Creates a new package management system. ```-y```  chooses yes for all options.
3) Install your packages! ```npm install mocha@9.2.2 chai --save-dev```
4) Open ```package.json``` and edit ```"scripts":``` to recognize mocha
```js
  "scripts": {
    "test": "./node_modules/mocha/bin/mocha"
  },  
  ```


## Unit Testing Setup
In your test folder, create a file called test.js and paste the following code in:
```js
const chai = require('chai');  // import the chai library
const assert = chai.expect;  // establish a variable to be used in our tests
const validator = require('../javascript/groupValidator.js'); // import the file where our function lives
describe("The function groupValidator()", () => {
   //tests
   it("should return true if there are between 2 and 5 group members", () => {
    assert(validator.isGroupValid(["a", "b", "c"])).to.be.true
  });

});
```
[Mocha](https://mochajs.org/) and [Chai](http://chaijs.com/) documentation.\
Chai [```.assert```](https://www.chaijs.com/api/assert/) api


# Difficult syntax:
## Arrays
### [for...of](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/for...of) is for Arrays
### [for...in](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/for...in)  is for Objects
### [Slice](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/slice)
Removes everything outside of the slicing range. Doesn't impact the original array.
```js
const animals = ['ant', 'bison', 'camel', 'duck', 'elephant'];

console.log(animals.slice(2));
// Expected output: Array ["camel", "duck", "elephant"]

console.log(animals.slice(2, 4));
// Expected output: Array ["camel", "duck"]

console.log(animals.slice(-2));
// Expected output: Array ["duck", "elephant"]

console.log(animals.slice(2, -1));
// Expected output: Array ["camel", "duck"]
```
[Array.prototype.filter()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/filter) - Filters an array\

[Array.prototype.map()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map) - Executes a function on each element and returns transformed array of the same length.\

[Array.prototype.reduce()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/reduce) - Reduces all the array values down to a single value according to a user callback function.
