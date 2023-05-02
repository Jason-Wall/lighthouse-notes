# W04
## HTML
**Block** elements fill the full width of the parent. Each block gets a new line.
```html
headings (<h1>, <h2>, <h3>,<h4>,<h5>,<h6>)
div (<div>)
section (<section>)
footer (<footer>)
article (<article>)
paragraph (<p>)
lists (<ul>, <ol>)
nav (<nav>)
```

**Inline** elements expand only to fill the width of their content. Cant add width, height, padding, margin to inlines.
```html
anchor (<a>)
em (<em>)
strong (<strong>)
span (<span>)
```

**Inline-Block** Best of both. No new line in browser, but can have margin, width, etc.
```html
image (<img src="" alt="">) <!-- No closing brackets!  -->
button (<button>)
```

[DOM Events Article](https://www.smashingmagazine.com/2013/11/an-introduction-to-dom-events/)

## **CSS**
## [Flex](https://css-tricks.com/snippets/css/a-guide-to-flexbox/)
```css
.parent {
display: flex; /*choose betwen row, column, or reverses*/
justify-content: space-between; /*Primary axis*/
align-items: center; /*Secondary axis*/
}
```
display
justify-content sets the items along the primary axis
Align-Items

## Content Delivery Networks (CDN)
[CDNJS](https://cdnjs.com/) Libraries that can be accessed by the browser. React, Vue, Bootstrap, etc.

[Google Fonts](https://fonts.google.com/)

## Javascript in the browser
find elements using:
```js
document.getElementById(elementID);
document.getElementsByClassName(className)
document.querySelector(cssSelector) //uses css class, id, etc.
```
## jquery
Include the jQuery library in the html header:
``` html
<script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
```
jquery can use [CSS selectors](https://www.w3schools.com/jquery/jquery_ref_selectors.asp) to find elements.\
Here is a [List of event methods](https://www.w3schools.com/jquery/jquery_ref_events.asp)\
Here is a list of [DOM manipulation tools](https://api.jquery.com/category/manipulation/) Add a space between methods to add multiple methods.

Best practice to enclose your jquery scripts inside of `.ready()`. This is an async function that executes once the page is loaded.
```js
$(document).ready(function() {
  $(#id).on('click', function() { //careful with arrow functions, bad for `this`
    alert("Element clicked!");
  })
});
```
[.submit](https://api.jquery.com/submit/#submit-handler)\
[.serialize](https://api.jquery.com/serialize/)\
[.post](https://api.jquery.com/jQuery.post/#jQuery-post-url-data-success-dataType) (HTTP request)\
[.get](https://api.jquery.com/jquery.get/) (HTTP request)\
[.ajax](https://api.jquery.com/jQuery.ajax/)

## Responsive Design
Thou shalt disable viewport zooming in all projects:\
`<meta name='viewport' content='width=device-width, initial-scale=1.0, maximum-scale=1.0' />`




## JS Tricks:
**[Optional chaining](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Optional_chaining)** (?.) operator accesses an object's property or calls a function. If the object accessed or function called using this operator is undefined or null, the expression short circuits and evaluates to undefined instead of throwing an error.
```js
const adventurer = {
  name: 'Alice',
  cat: {
    name: 'Dinah'
  }
};

const dogName = adventurer.dog?.name;
console.log(dogName);
// Expected output: undefined
console.log(adventurer.someNonExistentMethod?.());
// Expected output: undefined
```
**[Short Circuit Evaluation](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Logical_AND#short-circuit_evaluation)** The logical AND expression is a short-circuit operator. As each operand is converted to a boolean, if the result of one conversion is found to be false, the AND operator stops and returns the original value of that falsy operand; it does not evaluate any of the remaining operands.
```js 
a1 = true && true; // t && t returns true
a2 = true && false; // t && f returns false
a3 = false && true; // f && t returns false
a4 = false && 3 === 4; // f && f returns false
a5 = "Cat" && "Dog"; // t && t returns "Dog"
a6 = false && "Cat"; // f && t returns false
```

## [SQL](https://www.seancarney.ca/wp-content/uploads/2020/10/SQL-Cheat-Sheet-Quick-Reference-Guide.pdf)
Khan Academy has a great [intro course for SQL.](https://www.khanacademy.org/computing/computer-programming/sql)
```sql
CREATE TABLE groceries (id INTEGER PRIMARY KEY, name TEXT, quantity INTEGER, aisle INTEGER);

INSERT INTO groceries VALUES (1, 'bananas', 4, 1);
INSERT INTO groceries VALUES (2, 'Peanut Buter', 3, 8);

SELECT name FROM groceries WHERE aisle > 5 ORDER BY aisle;

SELECT aisle, SUM(quantity) FROM groceries GROUP BY aisle;

/* _ is a single character wildcard, % is multi
 Find the countries that have "t" as the second character. */
SELECT name FROM world
 WHERE name LIKE '_t%'

```
### Case - acts like a JS switch statement:
``` sql
/* CASE */
SELECT type, heart_rate,
    CASE 
        WHEN heart_rate > 220-30 THEN "above max"
        WHEN heart_rate > ROUND(0.90 * (220-30)) THEN "above target"
        WHEN heart_rate > ROUND(0.50 * (220-30)) THEN "within target"
        ELSE "below target"
    END as "hr_zone"
FROM exercise_logs;```