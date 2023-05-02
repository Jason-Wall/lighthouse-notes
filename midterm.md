# Midterm planning notes:

# Front End

## Index.html
Entry point for the site, all pages will build off this. SPA.

* Need to have jquery loaded into scripts.

``` html
 <!-- External JS -->
  <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.4.1/jquery.min.js"></script>
  <!-- Fonts, google maps... -->
  ```

* Need to have internal JS scripts loaded as well:
``` html 
 <!-- App JS -->
  <script type="text/javascript" src="/scripts/constants.js"></script>
  <script type="text/javascript" src="/scripts/supportFunctions.js"></script>
  <script type="text/javascript" src="/scripts/app.js"></script>
  ```
* Add unique class names to major divs so they can be hooked later with jquery


## public/scripts/app.js
Client side tools aggregation. This is file contains all of the actions that will be conducted on page ready:
``` js
$(document).ready(() => {
  submitTweetAJAX();
  loadTweetsAJAX(renderTweets);
  charCounterSetup();
  navButtonSetup();
});
```
## public/scripts/user.js, maps.js, pins.js ...
Client side helper functions. These functions are loaded before app.js in the html and have do all the the heavy lifting with jquery and ajax. 

``` js
// POST Example
const submitTweetAJAX = () => {
  const tweetForm = $('#tweet-form');
  tweetForm.on('submit', function(event) {
    event.preventDefault();
    const serializedData = $(this).serialize();
    $.ajax({
      method: 'POST',
      url: '/tweets',
      data: serializedData
    })
      .then(() => {
        loadTweetsAJAX((results) => {
          const newestTweet = [results.pop()];
          $('.tweet-text').val('');
          $('#counter').text(140);
          renderTweets(newestTweet);
        });
      });
  });
};

// GET Example
const loadTweetsAJAX = (callback) => {
  $.ajax({
    method: 'GET',
    url: '/tweets'
  })
    .then((result) => {
      callback(result);
    });
};

```

## March 11 Objectives:
[ ] Create a front page - Index.html\
[ ] Create a app.js file\
[ ] Manipulate DOM using helper functions

 # Back End
 ## server.js
 Web server set up. Runs middleware and routing.\
 Currently running ejs - remove/ comment this out.\
 Routing template in existing file is good.


## /routes/users.js, maps.js ...

Routes to the appropriate resources.

``` js 
// Note these all call the database...
module.exports = function(router, database) {

  router.get('/properties', (req, res) => {
    database.getAllProperties(req.query, 20)
    .then(properties => res.send({properties}))
    .catch(e => {
      console.error(e);
      res.send(e)
    }); 
  });

  router.post('/properties', (req, res) => {
    const userId = req.session.userId;
    database.addProperty({...req.body, owner_id: userId})
      .then(property => {
        res.send(property);
      })
      .catch(e => {
        console.error(e);
        res.send(e)
      });
  });

  return router;
}
  ```

## server/database.js
Responsible for server queries.
``` js
const { Pool } = require('pg');

const pool = new Pool({  // We generally want to use pool.
  user: 'labber',
  password: 'labber',
  host: 'localhost',
  database: 'lightbnb'
});

const getUserWithEmail = function(email) {
  const queryVars = [email];
  return pool
    .query(`SELECT * FROM users
            WHERE email = $1;`, queryVars)
    .then(res => {
      if (res.rows.length) {
        return (res.rows[0]);
      }
      return null;
    })
    .catch(err => {
      console.error('query error', err.stack);
    });
};
  
exports.getUserWithEmail = getUserWithEmail;
```