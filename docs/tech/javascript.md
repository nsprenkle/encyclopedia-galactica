# JavasScript

## References
- Rapid ES6 Training ([Pluralsight](https://app.pluralsight.com/player?course=rapid-javascript-training&author=mark-zamoyta&name=rapid-javascript-training-m2&clip=4&mode=live))

## Concepts

### Hoisting
Variables declared anywhere in code will be available at the top of the scope, but will be undefined until initialized. It can be said that the declarations have been hoisted or moved to the top of their scope.

Why?

Javascript is parsed in 2 passes, one identifies functions and variables, making them available. Instead of getting reference errors for undeclared variables, you will get undefined. The next pass runs the code. Functions defined will be available anywhere, but function expressions won't be set until they are declared in code.

``` javascript
// Source
function foo() {
  var a = "foo";

  /* some code here */

  foo();

  var b = "bar";
  var c = foo();

  function foo() {}
}

// Becomes
function foo() {
  var a = "foo";
  var b = undefined;
  var c = undefined;

  /* some code here */

  foo(); // runs successfully

  b = "bar";
  var c = foo();

  funciton foo() {}
}
```

**Upshot:** to mirror implementation, it's convention to declare your variables at the top of a function
 
### Closure
Functions have access to parent scope even after parent function has closed.
https://www.w3schools.com/js/js_function_closures.asp

``` javascript
var a = "foo";

function foo() {
  console.log("I have access to a: " + a);
}

foo(); /* I have access to a: foo */
```

## ES6 Syntax

### Let

let, not hoisted like var (block scoping)

``` javascript
  console.log(foo);
  var foo = 12;

  // in essence behaves like

  var foo;
  console.log(foo);
  foo = 12;

  // versus here, logs undefined
  console.log(bar);
  let bar = 12;
```

### Block scoping

Putting brackets around variable declarations limits scope to that block

``` javascript
let foo = 12;
{
  let foo = 2000;
}

console.log(foo); /* 12 */

let foo = 42;
for(let foo = 0; foo < 10; foo ++) {
}
console.log(foo); /* 42 */ 
```

foo is the for loop is scoped to the block and doesn't overwrite original foo definition

### Const
Can set constant values, use uppercase w/ underscores

``` javascript
const FOO_VALUE = 100;
```

Must be initialized and cannot be changed

### Arrow Function
Use a "fat arrow" in place of a function keyword, maintains "this" scope (block scoping)
Syntax Note: arrow must be on same line as inputs
No inputs, need open parentheses:

``` javascript
var getPrice = () => 5.99;
console.log(typeof getPrice); /* function */
```

for one input, no parentheses are needed

``` javascript
var getPrice = count => count *4.00;
console.log(getPrice(2)); /* 8.00 */
```

Multiple inputs, require parentheses

``` javascript
var getPrice = (count, tax) => count * 4.00 * (1 + tax);
console.log(getPrice(2, .07)); /* 8.56 */
```

You can also specify a block function but need a return keyword

``` javascript
var getPrice = (count, tax) => {
  var price = count *4.00;
  price *= (1 + tax);
  return price;
}
console.log(getPrice(2, .07)); /*8.56 */
```

Note the difference in scope, without arrow function gets the function scope:

``` javascript
document.addEventListener('click', function() {
  console.log(this); /* #document */
};
  
var invoice = {
  number: 123,
  process: function() { 
    console.log(this);
  }
};
invoice.process(); /* Object { number: 123, process: function} */
```

With arrow function, scope is maintained from when function is called.
Cannot use bind to change value of this.

``` javascript
document.addEventListener('click', () => console.log(this)); /* Window */

var invoice = {
  number: 123,
  process: () => console.log(this)
};
invoice.process(); /* Window */
```

### Default Function Parameters

Can specify default parameter from a function, to be assumed if no value or undefined is passed

``` javascript
var getProduct = function(productId = 1000) {
  console.log(productId);
}
getProduct(); /* 1000 */

var getProduct = function(productId = 1000, type = 'software') {
  console.log(productId + ', '  + type);
}
getProduct(undefined, 'hardware'); /* 1000, hardware */

//Can access other parameters

var getTotal = function(price, tax = price * 0.07) {
  console.log(price + tax);
};
getTotal(5.00); /* 5.53 */
```

### Rest and Spread
Rest = gather up elements into an array

``` javascript
var showCategories = function (productId, …categories) {
  console.log(categories);
};
showCategories(123, 'search', 'advertising'); /* ['search', 'advertising'] */
```

Spread = spreading out elements of an array/string, opposite of rest

``` javascript
var prices = [12, 20, 18];
var maxPrice = Math.max(…prices);
console.log(maxPrice); /* 20 */
```

/* Note: Math.max usually takes individual numbers, spread converts an array to individual arguments */

Spread also works on strings
``` javascript
var code = "43210";
Math.max(…code); /* 4 */
```

### Object Literal Extensions

New shorthand for creating object literals

``` javascript
var price = 5.99, quantity = 30;

var productView =  {
  price, 
  quantity
};
```

vs old method

``` javascript
var prodcutView = {
  price: price,
  quantity: quantity
}
```

### Dynamic field example, non ES2015

``` javascript
var field = "dynamic", val = 42;
var obj2 =  {
  [field]: val
};
obj2.dynamicField; /* 42 */
```

And a getter/setter example, while we're here

``` javascript
var product = {
  unitPrice: 13.37,
  quantity: 2,
  get price () { return this.unitPrice * this.quantity; },
  set price(value) { this.unitPrice = value; }
};
product.price = 10;
product.price; /* 20 */
```

## General Syntax

### For …of loops

Use to iterate over an iterable

``` javascript
var categories = ['hardware', 'software'', 'vaporware'];
for (var item of categories) {
  console.log(item);
} /* hardware, software, vaporware */
```

Works on any iterable, including strings

``` javascript
var word = 'onomatopoeia', count = 0;
for (var letter in word) {
  count++;
}
console.log(count); /* 12 */
```

### Octal and Binary literals

Octal values are prefixed with 0o or 0O

``` javascript
0o10 = 8;
0O10 = 8;
```

Binary values are prefixed with 0b or 0B;

``` javascript
0b10 = 2;
0B10 = 2;
```

### Template Literals

Use backticks and `${}` to insert variables into strings

``` javascript
let invoiceNum = '1350';
console.log(`Invoice Number: ${invoiceNum}`); /* Invoice Number: 1350 */
```

Can also use with expressions

``` javascript
let invoiceNum = '1350';
console.log(`Invoice Number: ${"INV-" + invoiceNum}`); /* Invoice Number: INV-1350 */
```

Template literals also preserve whitespace

``` javascript
let message = `A
B
C`;
console.log(message); 
/* A
B
C */
```

**_Revisit tagged template literals_**

``` javascript
function processInvoice(segments, …values) {
  console.log(segments); /* ['Invoice ', ' for ' , ''] */
  console.log(values); /* [1350, 2000] */
}
```

### Destructuring

Break an array into individual elements

``` javascript
let salary = ['32000', '50000', '75000'];
let [low, average, high] = salary;
console.log(average); /* 50000 */
```

Can combine with rest parameters to gather remaining values…

``` javascript
let salary = ['32000', '50000', '75000'];
let [low, …remaining] = salary;
console.log(remaining); /* [50000, 75000] */
```

… and with default parameters…

``` javascript
let salary = ['32000', '50000',];
let [low, average, high = '88000'] = salary;
console.log(high); /* 88000*/
```

… and nested arrays…

… and function calls…

``` javascript
function reviewSalary([low, average], high = '88000') {
  console.log(average);
}

reviewSalary(['32000', '50000']); /* 50000 */
```

… and strings …

… and objects (by using curly braces)…

``` javascript
let salary = {
  low: '32000',
  average: '50000',
  high: '75000'
};
let { low, average, high } = salary;
console.log(high); /* 75000 */
```

… alternatively, usnig different names

``` javascript
let { low: newLow, average: newAverage, high: newHigh } = salary;
```

### Modules
Note: Setup is hugely frustrating.

Way of exporting values form one file to another

``` javascript
/* module1.js*/
export let projectId = 99;
export let projectName = 'BuildIt';

/* base.js */
import { projectId as id, projectName } from 'module1.js';
console.log(`${projectName} has id" ${id}`); /* BuildIt has id: 99 */
```

### Expression switch - when true is set in a switch condition, cases become expressions

``` javascript
switch (true) {
  case orderTotal >= 50 && orderTotal < 75:
    discount = 10;
    break;
  case orderTotal >= 75 && orderTotal < 100:
    discount = 20;
    break;
  default:
    discount = 0;
}
```

### Boolean conversion
0, undefined, null, and "" are converted to false
Any non-zero or non-empty objects, and strings are converted to true
Convert with `Boolean(<value>)` or `!!<value> `

### Objects
#### Implicit properties
`valueOf`: when working with objects, you can set an implicit numerical value with the valueOf function.

``` javascript
var obj = { valueOf: function() {return 100} }
obj + 3 = 103;
```

`toString`: when working with strings, this is the value that will be presented, note that this is only used if valueOf is not found.

#### Math operations
Term | String | Number
--- | --- | ---
NaN | "NaN" | NaN, Note: NaN in any equation makes the result NaN
undefined | "undefined" | NaN
null | "null" | 0
object | obj representation | Reads from the valueOf property

With +, it defaults to a string concatenation.
When working purely with numbers, calculations will work. Otherwise items will get a string interpretation.

With -, /, %, the opposite is true and it will attempt to provide a number conversion for any calculation.

When working purely with floating points, there will be rounding errors
e.g. 1.1 * 1.1 = 1.210000000002
Fix with <number>.toFixed(<number of places>)

#### Unary Operators
++/-- when before a number operate before expression, after operate after line is complete
+/- right before expression casts to number, - flips sign

Bitwise Operators
Symbol | Operation
--- | ---
& | Bitwise AND
\| | Bitwise OR
^ | Bitwise XOR
<< x | Bitwise left shift
>> x | Bitwise right shift
>>> x | Triple shift, used for 2s complement

### Boolean Operators
Symbol | Operation
--- | ---
! | NOT
!! | Shorthand Boolean conversion
A && B | A AND B
A \|\| B | A OR B

Operation table
Value | Boolean
--- | ---
0 | false
!0 | true
"" | false
"A" | true
Object | true
null | false
undefined | false
NaN | false

##### Special cases
Expression | Result | Note
--- | --- | ---
 true && value | value | If first value evaluates true, second operand is returned
false && value | false | Anything after a false is ignored
null && value | null | If either operand is null, null gets returned
value && null | | |
undefined && value | undefined | Ditto for undefined
value && undefined | | | 
NaN && value | NaN | Ditto for NaN
value && NaN | | | 
objA|| objB | objA | If first operand is object, first is returned
false || obj | obj | First valid object is returned

### Equality Operators
Note: JavaScript generally tries to judge equality in the number case
True evaluates to 1
False evaluates to 0

Operator | Example | note
--- | --- | ---
== | true == 1, false == 0
!= | true != 2, true != "true"
=== | 55 === 45 + 10 | Identically equal, must be same data type
!== | 55 !== '55' | 
!== | null !== undefined

#### Special cases
Expression | Result | Note
--- | --- | ---
undefined == null | true | 
NaN == NaN | false | 
null == any | false | 
undefined == any | false | 

### Relational Operators
Operator | Example | Note
--- | --- | ---
< | 1 < 2 | Less than
<= | 10 <= 10 | Less than or equal to
<= |  10 <= 11
> | "beta" > "Beta" | Greater than
> | "alpha" > "alph" 
>= | 55 >= "55" | Greater than or equal to
>= | "42" >= "142"

#### Special cases
String and String: Strings are compared alphabetically, extra letters at the end make it come later alphabetically.

The uppercase alphabet comes before the lowercase alphabet, so lowercase letters are evaluated as larger.

String comparisons should be case-insensitive unless this behavior is intended.

String and Number: string is parsed to a number for comparison.

NaN: will not compare. e.g.
  NaN < 5; // false
  NaN >=5; // false
  
### Misc. Operators
Note: operator precedence, most assignments (below) come after the unary (+, -, /, *) in precedence and will be evaluated last.

e.g.
var total = 6;
total += 4 + 1;
total == 30;

Operator | Example | Note
--- | --- | ---
+= | 6 += 4 = 10 | Add to a number
-= | 10 -= 4 = 6 | Subtract from a number
*= | 6 *= 4 = 24 | Multiply a number
/= | 6 /=3 = 2 | Divide by a number
%= | 6 %=4 = 2 | Modulus
<<= | 1 <<= 2 = 4 | Left shift
>> =  | 4 >>= 1=2 | Right Shift

### Reference Types
Different from primitives like Booleans, Strings, and Numbers; reference types include objects, arrays, dates, regexps, and functions.

When a primative is saved in memory, it is pass-by-value, the value is written into memory. Assigning one primative to another primative copies the value.

When a reference type is saved in memory, the variable is accessed through its pointer, and assignments will use the same pointer.

Arrays
0 indexed, out of bounds returns undefined

4 ways to create
1. new Array(a,b,c);
2. Array(a,b,c);
3. [a,b,c]
4. Array(length)
5. [] 


Append: 
- array.length = new value
- array.push(vals…)
- newArray = array.concat([vals]) create new array with tacked on values

Prepend:
- array.unshift(val) prepends value

Remove:
- value.pop()
- value.shift(), removes first entry and move all others left

Slice
- array.slice(beginIndex)
- array.slice(begin,end)
- Note: can be negative indexed to start from end

Splice: remove or write to middle of array
- array.splice(begin, numToDelete)
- array.splice(begin, numToDelete, values to insert)

array.reverse()
array.sort() or array.sort(function(v1, v2))
array.indexOf(val)  
  

array.toString() = comma separated list of elements
array.valueOf() = array of values
array.join(char) = join items with char

### Dates
RegExp
var pattern = new RegExp(term, flags);
var pattern = /term/flag;

Common functions:
pattern.test(input), runs progressively through the input
pattern.exec(input), returns the result in array [match, index, input]
input.match(pattern), returns array of matched entries

### Objects
var obj = new Object();
var obj = {};

Access:
  - obj.value
  - obj["value"]

### Prototypes
Every object has a prototype object, these are default functions built into objects. For example, you might define a toString() function, but if this isn't found defined by the developer, it will search in the prototype object. Effectively a form of inheritance, searching until an undefined prototype.

Gain access to the prototype by defining an object, then using Object.Create(proto) to create a new object from that prototype.

var proto = { fields… };
var newObj = Object.create(proto);

Define Property - used to configure fields on objects including access and enumeration.

var task = {};
Object.defineProperty(task, 'text', { //config
  value: 'Get this job done',
  writable: true,
  enumerable: true,
  configurable: false,
  get: fn(),
  set: fn()
}

Get these configurations with Object.getOwnPropertyDescriptor(object, field);

Misc. Functions:
object.hasOwnProperty('prop') is true if the object has a property, but doesn't check prototype.

obj.isPrototypeOf(obj2) checks to see if obj1 is in the prototype chain of object 2.

val in obj checks to see if val is a valid property on obj or its prototype chain.

### Functions
Constructor function (e.g. Object) are uppercase and set the this values.

var Employee = function(name) {
  this.name = name;
};
var newEmployee = new Employee('JJ');

Note: don't add functions to the constructor function because they are duplicated for each new instance. With constructor functions we have accses to the prototype, so we add functions there.

Employee.prototype.giveRaise = function () {};

This
In an object, this refers to the parent object. Globally, it refers to the window object. For a function within a function, this gets pushed to the window namespace.

Call
function.call(obj, args…); object becomes the this pointer for the function call.

Apply
Just like call but you pass an array as the function arguments:
function.apply(obj, [args]);

Closures
Saving a function/object with access to an object keeps it from getting garbage collected so you can still access the object.

IIFE - Immediately Invoked Function Expression
Wroap a function to call it immediately, this garbage collects items in the function scope to avoid polluting global namespace.

(function (internalArgs) {
  // code…
})(inputArgs);

+function () {
  // code…
}();

### BOM and DOM
Browser Object Model
Browser functions: window size, location, open pages, setInterval, and setTimeout.

Dialogs: alert, dialog, prompt

Document Object Model
Allows you to modify content on the page by accessing by ID, name, tag name, css, query selector (like jQuery), etc.

### Event Handlers
Types - UI events, mouse/keyboard events
Events pass event objects which have properties attached.

Event handlers - UI events can be wired in the UI or in JS through the DOM.

Event listeners - more modern way, harder to accidentally overwrite in code. Can apply multiple event listeners to a single event, will trigger in order.

Bubbling - the order that events propagate through parent/children.
Set order of bubbling with elem.addEventListener(event, handlerFunction, true/false);
True - parent gets to handle first
False - child gets to handle first
Stop bubbling with event.stopPropogation() in the handler.
Can also stop default behavior (follow link, submit form) with event.preventDefault().

### Built-in Objects and Functions
Global Functions
parseInt(string, radix) - note, will parse until it hits a failure and will return the parts it succeeded at.
parseFloat(string) - also allowed to use scientific notation e.g. 123e9
isFinite(number)
isNaN(number)
encodeURI()/decodeURI()
eval(code) // DANGER

Math
String
arguments

### Misc.
Error Handling
try {
  throw new Error("Message");
}
catch (e) {
  console.log(e.message + " - " + e.name);
} 
finally {
}