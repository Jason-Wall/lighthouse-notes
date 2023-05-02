# W03

  ## Git - Branching
```bash
# See all the branches, current has a *
git branch

# create a new branch :
git branch <newBranchTitle>

# Switch to a branch:
git checkout <branchTitle>

# or create and switch in one line!
git checkout -b <branchTitle>

# Merge branch into main
git checkout main
git merge <branchTitle>

# Rebase consolidates parallel commits from the working branch to main:
git checkout <branchTitle>
git rebase main
git rebase <branchTitle>
```
## Cookies
Setting cookies in [Express](https://expressjs.com/en/api.html#res.cookie) - Note these are initially unencrypted.
### [Cookie Parser](https://github.com/expressjs/cookie-parser)
``` js 
npm install cookie-parser

const express = require('express')
const cookieParser = require('cookie-parser')

const app = express();
app.use(cookieParser());

// Reading a cookie:
app.get('/', function (req, res) {
  // Cookies that have not been signed
  console.log('Cookies: ', req.cookies);
  // Cookies that have been signed
  console.log('Signed Cookies: ', req.signedCookies);
});

// Create a cookie:
app.post('/', (req, res) => {
  const username = req.body.username;
  res.cookie('cookieName', cookieValue); 
  res.redirect(`/`); // Cookie is sent on final response.
})

app.listen(PORT)
```

### [Cookie-Session](https://github.com/expressjs/cookie-session)
Encrypted cookies!
```js
npm install cookie-session

const cookieSession = require('cookie-session');
const express = require('express');

const app = express();

app.use(cookieSession({
  name: 'session',
  keys: ['key1', 'key2'] // Keys are random strings.
}));

// Set a cookie:
app.post('/register',(req, res) =>{
  req.session.user_id = id; //stores the cookie as an object - access its properties with dot format.
  res.redirect('/urls');
});

// Clear a cookie:
app.post('/logout', (req, res) => {
  req.session = null; // Null the whole object, I presume you can nullify specific properties.
  res.redirect(`/login`);
});
```




## HTML - Forms
Forms have to have a method and action
```html
<form method = 'POST' action = '<url>'>
  <input name = 'username'/>
  <br/>
  <input name = 'password'/>
  <button type = 'submit'>Register</button>
</form>
```

### Generate a random UID:
```js 
//makes a 3 char user id. Increase to 2,n for more!
Math.random().toString(36).substring(2,5)
```




## cURL
Make network requests from the command line:
```
curl -X POST -i example.com --cookie "user_id=20126"
```

## Embedded Javascript Templates (EJS)
Other systems exist - [Mustache](https://mustache.github.io/), [Handlebars](https://handlebarsjs.com/), Nunjucks, or Pug - But we're using [EJS](https://ejs.co/).\
Allows you to create modular HTML. [How To](https://www.digitalocean.com/community/tutorials/how-to-use-ejs-to-template-your-node-application)\
**Server**
```js
const express = require('express');
const app = express();
// set the view engine to ejs
app.set('view engine', 'ejs');
// use res.render to load up an ejs view file
// index page
app.get('/', function(req, res) {
  res.render('pages/index');
});
```
Render looks in the `views` folder for `.ejs` files to visualize as HTML.\
`partials` are reusable blocks of HTML that can be inserted into views. 
```
<%- include('partials/_header') %>
```

Can use javascript in the HTML! Indicate JS using `<%` and `%>`
```
<ul>
  <% mascots.forEach(function(mascot) { %>
    <li>
      <strong><%= mascot.name %></strong>
      representing <%= mascot.organization %>,
      born <%= mascot.birth_year %>
    </li>
  <% }); %>
</ul>
```

## [bcrypt/ bcryptJS](https://www.npmjs.com/package/bcrypt)
A library to help you hash passwords:
`npm install bcrypt`\
The NPM documentation recommends using the async version.

```js
const bcrypt = require('bcrypt');
const saltRounds = 10;
const myPlaintextPassword = 's0/\/\P4$$w0rD';

//generate password:
bcrypt.genSalt(saltRounds, function(err, salt) {
    bcrypt.hash(myPlaintextPassword, salt, function(err, hash) {
        // Store hash in your password DB.
    });
});
// Check your password:
bcrypt.compare(myPlaintextPassword, hash, function(err, result) {
    // result == true
});
```


## [nodemon](https://www.npmjs.com/package/nodemon)
nodemon is a tool that helps develop Node.js based applications by automatically restarting the node application when file changes in the directory are detected.\
`npm install --save-dev nodemon`\
Run at command line:\
`./node_modules/.bin/nodemon -L express_server.js`\
But better to create a script in package.json:
```jsx
"scripts": {
  "start": "./node_modules/.bin/nodemon <filename>.js"}

  //Then in the CLI..
  npm start
  ```


## Morgan
Outputs server requests to the command line. Runs inside the server.
 ```js
npm install morgan

 // Import
 const morgan = require('morgan')

// Setup
 app.use(morgan('dev'));
 ```

## Tree Search with Recursive Functions
Root at the top, leaves at the bottom.

```js
//Search for a name and then stops when it finds it:
vampireWithName(name) {
    let foundVampire = null;
    // Checks if this is the vampire?
    if (this.name === name) {
      return this;
    } else {
      for (let entry of this.children) {
        if (!foundVampire) {
          foundVampire = entry.vampireWithName(name);
        }
      }
      return foundVampire;
    }
  }
```
```js
  // Returns an array of all the vampires that were converted after 1980
  get allMillennialVampires() {
    let millenials = [];
    if (this.yearConverted > 1980) {
      millenials.push(this);
    }
   
    for (let entry of this.offspring) {
      millenials = millenials.concat(entry.allMillennialVampires);
    }
    return millenials;
  }
}
```