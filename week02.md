# W02

## More Mocha and Chai
`npm install --save-dev mocha chai`

**[Mocha](https://mochajs.org/)** is a test runner and gives us the ```describe``` and ```it``` functions. Each ```it``` is a test, and each test should have at least one assertion.\
`npm test` to run tests once `package.json` is setup. Save test files in a folder named 'test' in the main folder.
``` js
"scripts": {
    "test": "mocha"
  },
  ```
**[Chai]((https://www.chaijs.com/api/assert/))** is an assertion library. Chai assertion functions are deliberately designed to integrate with testing frameworks like Mocha. 
Assertions don't return truthy/falsy. They error if they don't pass - The test runners visualize the errors.
### Sync Testing Template
```js
const assert = require('chai').assert;
const moduleFunc = require('../moduleFunc');

describe('# Name of function being tested', () => {
  it('description of test', () => {
      // Code...
      assert.equal(moduleFunc(param),expect);
    });
});
```
### Async Testing Template
This one uses callbacks, we could probably use promises though.
```js
const assert = require('chai').assert;
const moduleFunc = require('../moduleFunc');

describe('# Name of function being tested', () => {
  it('description of test', (done) => {
    moduleFunc(param, (data) => {
      assert.equal(data, expect);
      done();
    });
  });
});
```

## Module Require and Export
Import and export have to have identical format - Object or single variable.
```js
module.exports = {a, b, c}; 

const {a, b, c} = const assert = require('./filename');
```
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

# Asynchronous
Allows other aspects of the code to run while longer tasks are running (network calls, read/write to disk).\
**Order of actions** - The main thread will always finish first. Async items will be pushed off to the event loop. As the async tasks finish the rest of the code will execute.

## Async Returns Using Callbacks
Returning values when using async can be done using callback functions.\
Difficult to error check
Example:
```js
const asyncFunc = function(arg,callback) {
  fs.readFile(`./data/${args}.txt`, 'utf8', (error, data) => {
    if (!error) {callback(data)};
  });
};

let collectedData;
mainFunction(arg, (data) => {collectedData = data});
```
  
## Async Returns using Promises


# Networking
net is a node package that allows newtorking\
For 
`.on` is an event listener. Lots of options for this on [Node API](https://nodejs.org/api/net.html) under socket\
Client connecting to a server with read/ write:
```js
//IMPORTS ////////////
const net = require("net");

// MAIN THREAD //////////
const connect = () => {
  const conn = net.createConnection(host, port);
  conn.setEncoding('utf8');
  
  conn.on('connect', () => {
    console.log('Connection successful!');
    conn.write(`Name: ${userVal.initials}`);
  })

  conn.on('data', (data) => {
    console.log(data);
  });
  
  return conn;
};
```

### URL - Uniform Resource Locator
[See MDN for writeup](https://developer.mozilla.org/en-US/Learn/Understanding_URLs)\
**://** - Authority  - Consists of domain name (://) and port (:). Port is often omitted if it follows standard (80 for HTTP and 443 for HTTPS).\
**/** - Path - Indicates where the resource can be found. May or may not be an actual file location.
**?** - Parameters - Passed parameters seperated by &\
**\#** - Anchor - A bookmark of sorts in the requested resource. Scrolls to a place in a page or finds a timestamp in a video, etc.

### HTTP Methods
*GET*: used to "get" some data from the server\
*POST*: usually used to create some new data\
*PUT*: generally used for editing existing data on the server\
*DELETE*: used to delete some existing data\
There are more out there - This is good for now.

### HTTP Response
Returns a code (200 = success, 404 = not found, 500 = server error)


## [request](https://www.npmjs.com/package/request)
A package that simplifies all of this networking business - Though there newer better versions out there.\
**Asynchronous, doesn't support promises** 😥

`npm install request`
```js
const fetchFunc = function(url, callback) {

  request(`${url}`, (error, response, body) => {
    // Write tests for edge cases, clean up data, etc.
    callback(error, body);
  });
};
```

## [request-promise-native](https://www.npmjs.com/package/request-promise)
A package that simplifies all of this networking business - Though there newer better versions out there.\
**Asynchronous, supports promises** 😎
```js
const request = require('request-promise-native');

const fetchFunc = (url) => {
  return request(`${url}`);
};
// Returns resolved or rejected promises. See ISS_Promised exercise for more.
```

## [Promises](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise)
`.then` and `.catch` represent the actions carried out upon a resolved or rejected async activity.\
If resolved the function will find the next available then, if rejected it will find the next available catch.\
```js
const mySequentialAsyncs = function() {
  return asyncA()
    .then(asyncB)
    .then(asyncC)
    .then((data) => {
      const { response } = JSON.parse(data);
      return response;
    };
    .catch(rejectFunc)
    );
};
```

Parallelization can be done with `Promise.all(iterable)` or `Promise.race(iterable)`.\
Make your own promises:
```js
const promise = new Promise((resolve, reject) => {
  setTimeout(() => {
    resolve('foo');  // Must has a resolve at minimum. reject optional.
  }, 300);
});
```
























# Difficult Syntax
### setTimeout
`setTimeout(callback, delay)` - delay in msec, ie. 1000 ms = 1 sec.
```js
console.log('first line');
setTimeout(() => {
  console.log('timeout line');
  //nest another time dependent function in here to keep calling or force a sequence
  //could be recursive
}, 1000);
console.log('last line');
/// This would print in order: first, last, timeout
```
  ### Readline
  Allows for user input at the command line. 
  ```js
  const readline = require('node:readline');
  const { stdin: input, stdout: output } = require('node:process');
  
  const rl = readline.createInterface({ input, output }); // Opens channel
  
  rl.question('What do you think of Node.js? ', (answer) => {
    // TODO: Log the answer in a database
    console.log(`Thank you for your valuable feedback: ${answer}`);
  
    rl.close(); // close channel
  });
```