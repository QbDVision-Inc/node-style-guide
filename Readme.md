# QbDVision, Inc. Software Code Style Guide

This is a guide for writing consistent and aesthetically pleasing code at QbDVision, Inc.
It is inspired by what is popular within the community, and flavored with some
personal opinions.

This guide was originally created and forked from [Felix Geisendörfer](http://felixge.de/)'s
[Node.js Style Guide](https://github.com/felixge/node-style-guide) and is
licensed under the [CC BY-SA 3.0](http://creativecommons.org/licenses/by-sa/3.0/)
license. Other companies are encouraged to fork this repository and make adjustments
according to their preferences.

![Creative Commons License](http://i.creativecommons.org/l/by-sa/3.0/88x31.png)

## Table of contents

### Formatting
* [2 Spaces for indentation](#2-spaces-for-indentation)
* [Newlines](#newlines)
* [No trailing whitespace](#no-trailing-whitespace)
* [Use Semicolons](#use-semicolons)
* [80 characters per line](#80-characters-per-line)
* [Use double quotes](#use-double-quotes)
* [Opening braces go on the same line](#opening-braces-go-on-the-same-line)
* [Declare one variable per let statement](#declare-one-variable-per-let-statement)

### Naming Conventions
* [Use lowerCamelCase for variables, properties and function names](#use-lowercamelcase-for-variables-properties-and-function-names)
* [Use UpperCamelCase for class names](#use-uppercamelcase-for-class-names)
* [Use UPPERCASE for Constants](#use-uppercase-for-constants)
* [HTML and CSS](#html-and-css)
* [Filenames](#filenames)

### Variables
* [Use prefixes when naming booleans](#use-prefixes-when-naming-booleans)
* [Never use var](#never-use-var)
* [Object / Array creation](#object--array-creation)

### Conditionals
* [Use the === operator](#use-the--operator)
* [Use descriptive conditions](#use-descriptive-conditions)

### Functions
* [Write small functions](#write-small-functions)
* [Return early from functions](#return-early-from-functions)
* [Use the => syntax for nested closures](#use-the--syntax-for-nested-closures)
* [Method chaining](#method-chaining)

### Comments
* [Use comments intelligently](#use-comments-intelligently)
* [Use JsDoc syntax](#use-jsdoc-syntax)

### Miscellaneous
* [Object.preventExtensions, Object.seal, with, eval](#objectpreventextensions-objectseal-with-eval)
* [Requires At Top](#requires-at-top)
* [Getters and setters](#getters-and-setters)
* [Do not extend built-in prototypes](#do-not-extend-built-in-prototypes)
* [Use ES6 Syntax](#use-es6-syntax)
* [SQL](#sql)

## Formatting

### 2 Spaces for indentation

Use 2 spaces for indenting your code and swear an oath to never use tabs instead of
spaces - a special kind of hell is awaiting you otherwise.

### Newlines

Use UNIX-style newlines (`\n`), and a newline character as the last character
of a file. Windows-style newlines (`\r\n`) are forbidden inside any repository.

### No trailing whitespace

Just like you brush your teeth after every meal, you clean up any trailing
whitespace in your JS files before committing. Otherwise the rotten smell of
careless neglect will eventually drive away contributors and/or co-workers.

### Use Semicolons

According to [scientific research][hnsemicolons], the usage of semicolons is
a core value of our community. Consider the points of [the opposition][], but
be a traditionalist when it comes to abusing error correction mechanisms for
cheap syntactic pleasures.

[the opposition]: http://blog.izs.me/post/2353458699/an-open-letter-to-javascript-leaders-regarding
[hnsemicolons]: http://news.ycombinator.com/item?id=1547647

### 80 characters per line

Limit your lines to 80 characters. Yes, screens have gotten much bigger over the
last few years, but your brain has not. Use the additional room for split screen,
your editor supports that, right?

### Use double quotes

Use double quotes, unless you are already inside of a string.

*Right:*

```js
let foo = "bar";
```

*Wrong:*

```js
let foo = 'bar';
```

### Opening braces go on the same line

Your opening braces go on the same line as the statement.

*Right:*

```js
if (true) {
  console.log("winning");
}
```

*Wrong:*

```js
if (true)
{
  console.log("losing");
}
```

Also, notice the use of whitespace before and after the condition statement.

### Declare one variable per let statement

Declare one variable per let statement, it makes it easier to re-order the
lines. However, ignore [Crockford][crockfordconvention] when it comes to
declaring variables deeper inside a function, just put the declarations wherever
they make sense.

*Right:*

```js
let keys   = ["foo", "bar"];
let values = [23, 42];

let object = {};
while (keys.length) {
  let key = keys.pop();
  object[key] = values.pop();
}
```

*Wrong:*

```js
let keys = ["foo", "bar"],
    values = [23, 42],
    object = {},
    key;

while (keys.length) {
  key = keys.pop();
  object[key] = values.pop();
}
```

An exception to this rule is when pulling multiple variables out of an object. This is fine:
```
let {id, typeCode, data} = this.props;
```

## Naming Conventions

### Use lowerCamelCase for variables, properties and function names

Variables, properties and function names should use `lowerCamelCase`.  They
should also be descriptive. Single character variables and uncommon
abbreviations should generally be avoided.

*Right:*

```js
let adminUser = db.query("SELECT * FROM users ...");
```

*Wrong:*

```js
let admin_user = db.query("SELECT * FROM users ...");
```

### Use UpperCamelCase for class names

Class names should be capitalized using `UpperCamelCase`.

*Right:*

```js
function BankAccount() {
}
```

*Wrong:*

```js
function bank_Account() {
}
```

### Use UPPERCASE for Constants

Constants should be declared as regular variables or static class properties,
using all uppercase letters.

*Right:*

```js
let SECOND = 1 * 1000;

function File() {
}
File.FULL_PERMISSIONS = 0777;
```

*Wrong:*

```js
const SECOND = 1 * 1000;

function File() {
}
File.fullPermissions = 0777;
```

[const]: https://developer.mozilla.org/en/JavaScript/Reference/Statements/const

### HTML and CSS

In HTML and CSS, use kebab case for class names and camel case for IDs.  For example, in CSS you might see:

*Right:*

```css
.this-is-a-class {
  //..
}

#thisIsAnId {
  //..
}
```

*Wrong:*

```css
.thisIsAClass {
  //..
}

#this-Is-An-Id {
  //..
}
```

### Filenames

JS, JSX and SCSS filenames are snake case. For example:

```
snapshot_helper.js
some_thing.jsx
_bootstrap_overrides.scss
```

HTML and all other files are camel case.  For example:
```
cannedReports.html
deployEnvironment.template
```

If it’s a Lambda function, name it `*_handler.js`.
Otherwise name it after an appropriate design pattern.  For example:
```
something_factory.js
this_other_facade.js
```

Directories are camel case (ex. `webapp/controlMethods`)


## Variables

### Use prefixes when naming booleans

When naming boolean variables (and functions that return booleans), use prefixes that give yes/no answers such as *is/are*, *has*, and *should*:

*Good:*
```
let isValid = true;
let arePointersNull = false;
let shouldRenderComponent = true;
let hasLicense = true;
```

*Bad:*
```
let valid = true;
let pointersNull = false;
let renderComponent = true;
let license = true;
```
Note: Avoid boolean variables that represent the negation of a condition unless necessary e.g., use isValid instead of isNotValid

### Never use var

Never use var, always use let. Ex:

*Right:*
```
let a=2;
```

*Wrong:*
```
var a = 2;  ← Bad
```

### Object / Array creation

Use trailing commas and put *short* declarations on a single line. Only quote
keys when your interpreter complains:

*Right:*

```js
let a = ["hello", "world"];
let b = {
  good: "code",
  "is generally": "pretty",
};
```

*Wrong:*

```js
let a = [
  "hello", "world"
];
let b = {"good": "code"
        , is generally: "pretty"
        };
```

## Conditionals

### Use the === operator

Programming is not about remembering [stupid rules][comparisonoperators]. Use
the triple equality operator as it will work just as expected.

*Right:*

```js
let a = 0;
if (a !== "") {
  console.log("winning");
}

```

*Wrong:*

```js
let a = 0;
if (a == "") {
  console.log("losing");
}
```

[comparisonoperators]: https://developer.mozilla.org/en/JavaScript/Reference/Operators/Comparison_Operators

### Use descriptive conditions

Any non-trivial conditions should be assigned to a descriptively named variable or function:

*Right:*

```js
let isValidPassword = password.length >= 4 && /^(?=.*\d).{4,}$/.test(password);

if (isValidPassword) {
  console.log("winning");
}
```

*Wrong:*

```js
if (password.length >= 4 && /^(?=.*\d).{4,}$/.test(password)) {
  console.log("losing");
}
```

## Functions

### Write small functions

Keep your functions short. A good function fits on a slide that the people in
the last row of a big room can comfortably read. So don't count on them having
perfect vision and limit yourself to ~15 lines of code per function.

### Return early from functions

To avoid deep nesting of if-statements, always return a function's value as early
as possible.

*Right:*

```js
function isPercentage(val) {
  if (val < 0) {
    return false;
  }

  if (val > 100) {
    return false;
  }

  return true;
}
```

*Wrong:*

```js
function isPercentage(val) {
  if (val >= 0) {
    if (val < 100) {
      return true;
    } else {
      return false;
    }
  } else {
    return false;
  }
}
```

Or for this particular example it may also be fine to shorten things even
further:

```js
function isPercentage(val) {
  let isInRange = (val >= 0 && val <= 100);
  return isInRange;
}
```

### Use the => syntax for nested closures

Use => syntax for nested closures. This is because it binds the `this` variable better.

*Right:*

```js
req.on("end", () => {
  console.log("winning");
});
```

*Wrong:*

```js
req.on("end", function() {
  console.log("losing");
});

// Also wrong:

req.on("end", function onEnd() {
  console.log("losing");
});
```

### Avoid unnecessary brackets

Don't add unnecessary brackets to closures.

*Right:*

```js
let theThing = myArray.find(item => item.isThing === true);
```

*Wrong:*

```js
let theThing = myArray.find((item) => item.isThing === true);
```

### Method chaining

One method per line should be used if you want to chain methods.

You should also indent these methods so it's easier to tell they are part of the same chain.

*Right:*

```js
User
  .findOne({ name: "foo" })
  .populate("bar")
  .exec(function(err, user) {
    return true;
  });
```

*Wrong:*

```js
User
.findOne({ name: "foo" })
.populate("bar")
.exec(function(err, user) {
  return true;
});

User.findOne({ name: "foo" })
  .populate("bar")
  .exec(function(err, user) {
    return true;
  });

User.findOne({ name: "foo" }).populate("bar")
.exec(function(err, user) {
  return true;
});

User.findOne({ name: "foo" }).populate("bar")
  .exec(function(err, user) {
    return true;
  });
```

## Comments

### Use comments intelligently

Use single or multi line comments. Try to write
comments that explain higher level mechanisms or clarify difficult
segments of your code. Don't use comments to restate trivial things.

*Right:*

```js
// "ID_SOMETHING=VALUE" -> ["ID_SOMETHING=VALUE", "SOMETHING", "VALUE"]
let matches = item.match(/ID_([^\n]+)=([^\n]+)/);

/* This function has a nasty side effect where a failure to increment a
   redis counter used for statistics will cause an exception. This needs
   to be fixed in a later iteration. */
function loadUser(id, cb) {
  // ...
}

let isSessionValid = (session.expires < Date.now());
if (isSessionValid) {
  // ...
}
```

*Wrong:*

```js
// Execute a regex
let matches = item.match(/ID_([^\n]+)=([^\n]+)/);

// Usage: loadUser(5, function() { ... })
function loadUser(id, cb) {
  // ...
}

// Check if the session is valid
let isSessionValid = (session.expires < Date.now());
// If the session is valid
if (isSessionValid) {
  // ...
}
```

### Use JsDoc syntax

When documenting methods and classes  use [JSDoc](https://devdocs.io/jsdoc/) syntax.

### Every file should have a comment at the top

Every JS file should have a comment at the top that explains the reason for this file existing.  For example:
```
"use strict";

/* The functions here are responsible for ...
 */
```

Or if the file is for a class:

```
"use strict";

import //...

/**
 * This class is responsible for ...
 */
class SomeClass extends SomeOtherClass {
```

## Miscellaneous

### Object.preventExtensions, Object.seal, with, eval

Crazy stuff that you will probably never need. Stay away from it.

### Requires At Top

Always put requires at top of file to clearly illustrate a file's dependencies. Besides giving an overview for others at a quick glance of dependencies and possible memory impact, it allows one to determine if they need a package.json file should they choose to use the file elsewhere.

### Getters and setters

Do not use setters, they cause more problems for people who try to use your
software than they can solve.

Feel free to use getters that are free from [side effects][sideeffect], like
providing a length property for a collection class.

[sideeffect]: http://en.wikipedia.org/wiki/Side_effect_(computer_science)

### Do not extend built-in prototypes

Do not extend the prototype of native JavaScript objects. Your future self will
be forever grateful.

*Right:*

```js
let a = [];
if (!a.length) {
  console.log("winning");
}
```

*Wrong:*

```js
Array.prototype.empty = function() {
  return !this.length;
}

let a = [];
if (a.empty()) {
  console.log("losing");
}
```

### Use ES6 syntax

Always use ES6 syntax.

### SQL

For SQL, follow [this style guide](https://www.sqlstyle.guide/).

