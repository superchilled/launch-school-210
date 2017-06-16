# Practice Problems: Variable Scopes in JavaScript (1)

Please predict the output of the following programs and explain why they output what they do.

### Problem 1

```javascript
var a = 'outer';

function testScope() {
  var a = 'inner';
  console.log(a);
}

console.log(a);
testScope();
console.log(a);
```

**My Solution:**

  * Line 8 will log the String `outer` since variable `a` is declared and assigned to `outer` on line 1
  * Line 9 will log the String `inner` since a new variable `a` is declared and assigned to `inner` within the `testScope()` function on line 4. When this function is invoked on line 9, this new variable `a` is declared and assigned, and then the value of it logged within the funtion on line 5
  * Line 10 will log the String `outer` since it accesses th variable `a` declared on line 1, and not the one declared on line 4 (within the function). The assignment to the `a` on line 4 doesn't change the value of the `a` on eline 1 since a new varaible of the same name has been declared within the scope of the function, it shadows the variable outside the funtion

**LS Explanation:**

Line 8 is the first invocation of `console.log();` here, `a` resolves as the global variable. Line 9 calls the `testScope()` function; in the function, `a` resolves as the local variable, so line 5 logs `inner`. After testScope() returns, the `a` on line 10 resolves as the global variable again; therefore, it logs `outer`.

### Problem 2

```javascript
var a = 'outer';

function testScope() {
  a = 'inner';
  console.log(a);
}

console.log(a);
testScope();
console.log(a);
```

**My Solution:**

  * Line 8 will log the String `outer` since variable `a` is declared and assigned to `outer` on line 1
  * Line 9 will log the String `inner` since the variable `a` declared on line 1 is reassigned to `inner` within the function on line 4, and the value of the variable logged to the console on line 5; so when the `testScope()` function is invoked on line 9, `a` is reassigned and logged
  * Line 10 will log the String `inner`, since it is logging the value of the `a` declared on line 1, and this has been reassigned to `inner` when the function was called

**LS Explanation:**

On line 4, `a` resolves as the global variable; the assignment assigns `inner` to the variable. Thus, line 10 logs `inner` instead of outer.

### Problem 3

```javascript
var basket = 'empty';

function goShopping() {
  function shop1() {
    basket = 'tv';
  }

  console.log(basket);

  function shop2() {
    basket = 'computer';
  }

  function shop3() {
    var basket = 'play station';
    console.log(basket);
  }

  shop1();
  shop2();
  shop3();

  console.log(basket);
}

goShopping();
```

**My Solution:**

  * Running this code will log: `empty`, `play station`, `computer`
  * The global variable `basket` is declared and assigned to the String `empty` on line 1
  * When the function `goShopping();` is invoked on line 26, line 8 logs the value of `basket`, which at that point is still `empty`
  * The nested 'shop' functions are then invoked on lines 19, 20, and 21
  * `shop1();` reassigns the global var to `tv` and `shop2();` reassigns it to `computer`
  * The shop3();` function declares a local `basket` variable and assigns to  the String`play station`; it also logs the value of this `basket`
  * Within the `goShopping();` function on line 23, the value of global `basket` is again logged, at that point it is `computer` since the last reassignment was enacted by the invocation of `shop2();` on line 20

**LS Explanation:**

The first log operation occurs on line 8; here, `basket` still has its original value, `empty`. The function call on line 19 changes basket to `tv`, and the call on line 20 changes it to `computer`. The function call on line 21 does not alter the value of the `basket` global, but defines and sets a local variable with the same name. It then logs `play station`. Upon returning from `shop3`, the local variable goes away, so line 23 logs the value of the global `basket`: `computer`.

### Problem 4

```javascript
function hello() {
  a = 'hello';
}

hello();
console.log(a);
```

**My Solution:**

  * Line 6 logs the String `hello`.
  * Since `a` is not declared in the global scope, when the `hello()` function is invoked on line 5, a new global `a` is created and assigned to `hello`

**LS Explanation:**

Here, we call the `hello()` function, so we assign a value of `hello` to the variable. The variable is a global variable since we don't declare it with `var`. Thus, line 6 logs `hello`.

### Problem 5

```javascript
function hello() {
  var a = 'hello'
}

hello();
console.log(a);
```

**My Solution:**

  * This will raise a reference error, since `a` is not defined within the global scope and so cannot be accessed on line 6
  * When `hello()` is called on line 5, it declares a local variable `a` and assigns it to `hello`, but because the variable is declared locally within the function, it is not available globally

**LS Explanation:**

Since we don't define a global variable `a`, line 6 does not find any variables named `a`; thus, it raises a `ReferenceError`.

### Problem 6

```javascript
console.log(a);

var a = 1;
```

**My Solution:**

  * This will log `undefined`.
  * The global variable `a` is declared and assigned to `1` on line 3.
  * The variable declaration is hoisted to the top of the program -- so above the `console.log(a);` on line 1, but the assignment stays on line 3 -- so below `console.log(a);`
  * When `a` when is hoisted it is assigned a value of `undefined`

**LS Explanation:**

After hoisting, this program is equivalent to:

```javascript
var a;
console.log(a);
a = 1;
```

Line 2 logs `undefined` since we declared a but never assigned it a value.


### Problem 7

```javascript
console.log(a);

function hello() {
  a = 1;
}
```

**My Solution:**

  * This raises a reference error, since `hello()` is never invoked, there is no declared variable `a` within the scope of `console.log(a)`
  * If `hello()` had ben invoked the assignement to an undeclared variable within the function would have created a global variable `a` and assigned it to `1`, so the value of `a` would have been `1` when `console.log(a)` was called

**LS Explanation:**

After hoisting, this program is equivalent to:

```javascript
function hello() {
  a = 1;
}

console.log(a);
```

We define `hello()`, but never call it, so we never assign a value to `a`. Since we also don't declare `a` anywhere, line 5 produces a `ReferenceError`.
