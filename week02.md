# W02

## More Mocha and Chai
**Mocha** is a test runner and gives us the ```describe``` and ```it``` functions. Each ```it``` is a test, and each test should have at least one assertion.\
**Chai** is an assertion library. Chai assertion functions are deliberately designed to integrate with testing frameworks like Mocha.
**Assertion Libraries** don't return truthy/falsy. They error if they don't pass - The test runners visualize the errors.

## [.gitignore](https://git-scm.com/docs/gitignore)
Create a .gitignore file in the top directory of the project.\
Best practice to omit the node-module from git.\
Any file listed in ```.gitignore``` will be omitted from status, adds, or commit all.\
Omit folders by including a forward slash - eg. ```/node_module```

## ES6 Object Property Shorthand
You can shorten the code needed to define a property by allowing the name and value of a variable to be assigned ot the object.
```js
const age = 33;
const person = {
  name: 'Pat',
  age
};
//same as const person = {  name: 'Pat',  age: age};
```
## npm and Uploading
[npm landing page](https://www.npmjs.com/)\
login to NPM using `npm login` and follow the instructions.\
*Publishing Scoped Public Packages* - follow the [instructions](https://docs.npmjs.com/creating-and-publishing-scoped-public-packages#publishing-scoped-public-packages)\

## Asynchronous
Allows other aspects of the code to run while longer tasks are running (network calls, read/write to disk)\
Be careful about order of actions - If there are a few async processes running, their callbacks will execute whenever they finish. No guarantee of order unless you program them specifically to do things in order.
### setTimeout







# Difficult Syntax
### setTimeout
`setTimeout(callback, delay)` - delay in msec, ie. 1000 ms = 1 sec.
```js
console.log('first line');
setTimeout(() => {
  console.log('timeout line');
}, 1000);
console.log('last line');
/// This would print in order: first, last, timeout
```