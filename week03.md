# W03
## Embedded Javascript Templates (EJS)
Other systems exist - [Mustache](https://mustache.github.io/), [Handlebars](https://handlebarsjs.com/), Nunjucks, or Pug - But we're using [EJS](https://ejs.co/).\
Allows you to create modular HTML. [How To](https://www.digitalocean.com/community/tutorials/how-to-use-ejs-to-template-your-node-application)\
**Server**
```js
var express = require('express');
var app = express();
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
Setting cookies in [Express](https://expressjs.com/en/api.html#res.cookie)\
[Cookie Parser](https://github.com/expressjs/cookie-parser) 
``` js 
npm install cookie-parser

const express = require('express')
const cookieParser = require('cookie-parser')

const app = express()
app.use(cookieParser())

app.get('/', function (req, res) {
  // Cookies that have not been signed
  console.log('Cookies: ', req.cookies)
  // Cookies that have been signed
  console.log('Signed Cookies: ', req.signedCookies)
})

app.listen(PORT)
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
Math.random().tostring(36).substring(2,5)



 
