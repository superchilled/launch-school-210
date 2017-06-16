# Practice Problems: Variable Scopes in JavaScript (2)

Please predict the output of the following programs and explain why they output what they do.

### Problem 1

```javascript
function say() {
  if (false) {
    var a = 'hello from inside a block';
  }

  console.log(a);
}
say();
```

**My Solution:**

  * `console.log(a)` will log `undefined` on line 6. The variable declaration is hoisted, so `a` is `undefined`
  * The `if` branch will not be executed since the condition is false, so the variable `a` will never be assigned

**LS Explanation:**

Scoping in JavaScript is function-level, not block-level. Therefore, after hoisting, this code becomes:

```javascript
function say() {
  var a;
  if (false) {
    a = 'hello from inside a block';
  }

  console.log(a);
}
say();
```

Since we declare but never assign `a`, line 7 logs `undefined`.

### Problem 2

```javascript
function hello() {
  a = 'hello';
  console.log(a);

  if (false) {
    var a = 'hello again';
  }
}

hello();
console.log(a);
```

**My Solution:**

  * This will log `hello` and also raise a reference error
  * When `hello()` invoked on line 10, the variable declaration `var a;` is hoisted to the top of the function, but not the global scope.
  * `a` is then assigned to the String `hello` on line 2, this value is logged on line 3
  * the `console.log(a)` on line 11 doesn't have access to the `a` declared within the function and so raises a reference error

**LS Explanation:**

After hoisting:

```javascript
function hello() {
  var a;
  a = 'hello';

  console.log(a);

  if (false) {
    a = 'hello again';
  }
}

hello();
console.log(a);
```

`a`'s scope is the body of `hello()`. Since there is no global variable named `a`, line 13 raises an error.


### Problem 3

```javascript
var a = 'hello';

for (var i = 0; i < 5; i++) {
  var a = i;
}

console.log(a);
```

**My Solution:**

  * The number `4` is logged
  * `a` is declared and assigned to the String `hello` on line 1
  * `a` gets reassigned mutliple times within the `for` loop, ending with assignment to `4`. Although there is a new declaration here as well, loops do not have a separate scope, so the `a` in the for loop` is not local to the loop, but global

**LS Explanation:**

JavaScript hoists the variable declaration on line 4 to the top of the global scope. Since a global variable named `a` exists, the hoist has no direct effect on operation. Inside the loop, `a` gets assigned five times; at the end of the loop, it has a value of `4`. Thus, line 7 logs `4`.

### Problem 4

```javascript
var a = 1;

function foo() {
  a = 2;
  function bar() {
    a = 3;
    return 4;
  }

  return bar();
}

console.log(foo());
console.log(a);
```

**My Solution:**

  * This code will log `4` and `3`
  * Line 13 invokes the `foo()` method and logs the return value, which is `4` since `foo()` returns `bar()` which returns `4`
  * Line 14 logs teh value of the global variable `a`; this is `3` since it is reassigned in `bar()` to that value

**LS Explanation:**

The `foo` function returns the return value of the `bar` function, which is `4`. During this process, the code changes the global variable twice. Thus, the final value is `3`.

### Problem 5

```javascript
a = 'global'

function checkScope() {
  var a = 'local';
  function nested() {
    var a = 'nested';
    function supernested() {
      a = 'supernested';
      return a;
    }

    return supernested();
  }

  return nested();
}

console.log(checkScope());
console.log(a);
```

**My Solution:**

  * This will log `supernested` and `global`
  * Line 18 invokes `checkScope()` and logs the return value. `checkScope()` returns the return of `nested`, which returns the return of `supernested()` which is the `a` declared local to `nested()` which is reasigned to `supernested` on line 8.
  * Line 19 logs the value of the global`a` which is the `global` string assigned to the undeclared variable `a` on line 1

**LS Explanation:**

With super-nested functions, you must chase through the functions starting with the function invocations. Here, we start with line 18, the first function invocation. From there, line 4 goes to line 5, line 5 to line 15, and so on through lines 6, 7, 12, 8, and 9. Line 9 obviously returns 'supernested', so line 12 must return 'supernested' too. This takes us back to line 15 which also returns `'supernested'`. Finally, line 18 receives the final return value (`'supernested'`) and logs it. During this entire process, we never modify the global `a`, so it still has the value `global`.

### Problem 6

```javascript
var a = 'outer';
var b = 'outer';

console.log(a);
console.log(b);
setScope(a);
console.log(a);
console.log(b);

function setScope(foo) {
  foo = 'inner';
  b = 'inner';
}
```

**My Solution:**

  * This logs `outer`, `outer`, `outer`, `inner`
  * `a` and `b` are declared and assigned on lines 1 & 2 and logged on lines 4 & 5
  * `setScope()` is invoked on line 6 with the value of `a` (`outer`) passed to it and assigned to parameter `foo`
  * `foo` is reassined to `inner` within `setScope()` and `b` is also reassigned to `inner`, `a` remains unchanged
  * `a` (still `outer`) and `b` (now `inner`) are again logged on lines 7 & 8

**LS Explanation:**

Function arguments become local variables in the function, so assigning to an argument has no effect on the original argument.

### Problem 7

```javascript
var total = 50;
var increment = 15;

function incrementBy(increment) {
  total += increment;
}

console.log(total);
incrementBy(10);
console.log(total);
console.log(increment);
```

**My Solution:**

  * This logs `50`, `60`, `15`
  * `total` is declared on line 1 and assigned to `50`
  * `increment` is declared on line 2 and assigned to `15`
  * `total` is logged on line 8; at this point its value is still `50`
  * `incrementBy()` is called on line 9 with `10` passed to it as an argument and assigned to the local variable `increment`; this reassigns `total` to `60` (`50 + 10`)
  * `total` (now `60`) is logged on line `10`
  * The global `increment` whose value has not changed from `15` is logged on line 11

**LS Explanation:**

Though our parameter has the same name as the variable declared on line 2, it is not the same variable. Function arguments are locally scoped variables, even when they have the same names as variables defined in the outer scope.

### Problem 8

```javascript
var a = 'outer';

console.log(a);
setScope();
console.log(a);

var setScope = function() {
  a = 'inner';
}
```

**My Solution:**

  * This logs `outer` and raises an uncaught type exception
  * `a` is declared and assigned to `outer` on line 1
  * `a`, with a value of `outer` is logged on line 3
  * The declaration of `setScope` is hoisted, but its value is `undefined` since the assignement to `function()` does not occur until line 7. When we attempt to invoke `setScope()` as a function on line 4, an uncaught type exception is raised since at that point `setScope` has not been assigned to a function and so we cannot invoke it as a funtion

**LS Explanation:**

With hoisting, the above code is equivalent to:

```javascript
var a;
var setScope;

a = 'outer';

console.log(a);
setScope();
console.log(a);

setScope = function() {
  a = 'inner';
}

```

Line 7 tries to call setScope as a function. However, it is just a declared global variable that doesn't have a defined value. Note unlike function declarations, function expressions are effectively the same as assignment operations; JavaScript hoists only the variable names, not the function bodies.
