# JavaScript Style Guide  -- Problems

Identify the code that violates the Airbnb JavaScript style guide, and update the code to fix the issues you identify. There may be more than one issue in each code snippet.

Using the [AirBnB JavaScript Styleguide](https://github.com/airbnb/javascript)

## Problem 1

```javaScript
var title = "The Three-Body Problem";
```

### Style Guide Violations

Strings 6.1: Use single quotes `''` for strings.

  * https://github.com/airbnb/javascript#strings--quotes

### LS Answer

The style guide recommends using single quotes (`'`) with Strings, unless the String contains single quotes.


## Problem 2

```javaScript
var title = 'The Three-Body Problem',
    author = 'Cixin Liu',
    page_count = 400;
```

### Style Guide Violations

Variables 13.1: USe `const` or `let` to declare Variables.

  * https://github.com/airbnb/javascript#variables--const

Though this is ES6-specific:

  * https://github.com/airbnb/javascript#ecmascript-6-es-2015-styles
  * https://github.com/airbnb/javascript#references--prefer-const

Variables 13.2: Use one `const` or `let` declaration per variable.

  * https://github.com/airbnb/javascript#variables--one-const

Naming Conventions 23.2: Use camelCase when naming objects, functions, and instances.

  * https://github.com/airbnb/javascript#naming--camelCase


## Problem 3

```javaScript
var completed = lastPageRead == 400;
```

### Style Guide Violations

Comparison Operators & Equality 15.1: Use `===` and `!==` over `==` and `!=`.

  * https://github.com/airbnb/javascript#comparison--eqeqeq


## Problem 4

```javaScript
if (finishedBook())
  console.log('You have finished reading this book');
```

### Style Guide Violations

Blocks 16.1: Use braces with all multi-line blocks.

  * https://github.com/airbnb/javascript#blocks--braces

## Problem 5

```javaScript
function read(pages) {
      console.log('You started reading.');
      for (var i=0; i<pages; i++) {
              var message = 'You read page '+i;
              console.log(message);
      }
}

read(400);
```

### Style Guide Violations

Whitespace 19.1: Use soft tabs (space character) set to 2 spaces.

  * https://github.com/airbnb/javascript#whitespace--spaces

Whitespace 19.4: Set off operators with spaces.

  * https://github.com/airbnb/javascript#whitespace--infix-ops

Variables 13.6: Avoid using unary increments and decrements (`++`, `--`).

  * https://github.com/airbnb/javascript#variables--unary-increment-decrement

### LS Answer

It also recommends (on the ES5 page) that all variables be declared at the top of the function.

  * https://github.com/airbnb/javascript/tree/es5-deprecated/es5#variables
