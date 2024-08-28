# switch - case
```js
switch(value) {
    case "val" : //strict equality checked ===
    break;
    case "var": //if break statement is missed and if matches then below cases(continuous (doesn't check whether match of not) untill break) also run
    case "let":
    break;
    default:
    break;
}
```
# code structure
give semicolon do not rely on js
nesting comments not possible

# functions
 - **local variables** -> A variable declared inside a function is only visible inside that function.
 - **outer variables** -> The function has full access to the outer variable. It can modify it as well.
 - **same name** -> if local and outer variable have same name then local variable is accessed
 - Global variables are visible from any function (unless shadowed by locals). **Avoid** global variables

### pass by value


### default values
- If a function is called, but an argument is not provided, then the corresponding value becomes **undefined**.
can give default values
```js
function showMessage(from, text = "no text given") {// just incase of undefined in case of null use ?? // explicit checking of === undefined
  alert( from + ": " + text );
}
//if default value not given the undefined is printed
//**if passed parameter is also undefined then also "no text given" is written
function showMessage(from, text = anotherFunction()) {
  // anotherFunction() only executed if no text given
  // its result becomes the value of text
}
showMessage("user");
```
- || can be used but falsify things can give undefined like 0||undefined gives undefined ?? operator is better
- `prompt("question?",defaultValue)` -> returns the value inputted

### returning a value
- do not add newline after return it will convert it to `return;`
```js
return (
    randomValues
);
```

### Naming a function 
- function name should ideally start with verb 

## arrow function
`let func = (arg1,arg2,..) => {expressions};`
- can remove parenthesis if only one argument
- can remove curly brackets if single line expression

## function keywword
`let x = function(args) {expressions}`
```js
let x = function y(args){expressions;}
x(); //calles the function
y(); //gives error cannot call undefined
```
- in strict mode function declaration remains in the scope in which it is defined
- in non strict mode function declaration can be accessed outside but after declaration(function(){}) only

# variables
- shadowing variable in same scope is not possible
- The name must contain only letters, digits, or the symbols $ and _.
- The first character must not be a digit.
- there is a list of reserved keywords that cannot be named variable
- in not strict case `num = 5;` where num variable was not created earlier will create a variable and assign value<br/>
constant should be declared capital snakecase `const RED_COLOR = 255;`

# data types
- typeof is an operator not a function
- `NaN**0 = 1`
- `5/0 = Infinity`
- `(anything except undeclared)**0 = 1`
- ` ±(2^53-1)` range of numbers in javascript
### big int 123n
```js
`variable = ${variable}` //opens the variables value ** STRIN INTERPOLATION
```
`typeof null = 'object'` 
`typeof variableHavingFunction = 'Function'`
### type conversions
- `Number(anything)` tries to convert everything to number if not possible then to NaN, true becomes 1 and false becomes 0
- `Boolean(anything)` 0,NaN,"",null,undefined becomes false; rest true

## comparison
- lexicographic comparison happens between strings
- "a" < "aaa" (true)
## of different types
- if are of different types converts it into number and then compare
- `null>=0` true but non of single case is true
- `null == undefined` true
- strict equality === checks both type and the value
```
14	unary plus	+
14	unary negation	-
13	exponentiation	**
12	multiplication	*
12	division	/
11	addition	+
11	subtraction	-
…	…	…
2	assignment	=
```

++ , -- precedence > arithematic operators

```
bitwise operators
AND ( & )
OR ( | )
XOR ( ^ )
NOT ( ~ )
LEFT SHIFT ( << )
RIGHT SHIFT ( >> )
ZERO-FILL RIGHT SHIFT ( >>> )
```
, (comma has very low precedence) <br/>

### || is also called short circuit
- if true expression then does not run further
- returns the first expression that is found to be true else last

### && 
- returns the value which is false
- else the last one is returned

`precedence of && is higher than ||`
<br/>
precedence of NOT ! is the highest of all logical operators<br/>

### ??
- except for null and undefined; return anything - last
- ?? cannot be used with || or &&
- same precedence as ||

#### break / continue operator cannot be used with ? ternary operator
- can label a loop and the break or continue

### sources, breakpoint, pause, variables in console 

space before and after parenthesis and operators, space after comma / semicolor, 

### writing comments
function: usage, parameters, returned value.

# Objects
- delete operator deletes key value pair from object<br/>
`delete obj.key`
- multiword key should be under double quotes
- `use[multiwordKey]`
```javascript
let fruit = "apple";
let bag = {
  [fruit]: 5, // the name of the property is taken from the variable fruit
};
let fruit = 'apple';
let bag = {
  [fruit + 'Computers']: 5 // bag.appleComputers = 5
};
```
- object properties have no restriction on name
-  special property named ``__proto__.`` We can’t set it to a non-object value.
- `key in obj` in operator to check whether key exists or not
- `for let key in obj {}` keys are in sorted order integers(just of integers) then string 
- integers go in the ascending sorted order
-  if the keys are non-integer, then they are listed in the creation order, for instance:
- objects are compared by their reference (equality operator)
- comparison operator converts into integers then compare
```javascript
let user = {};
Object.assign(user,{"name":"a"},{"name":"b"});
//user = {name:b}
```
- it copies all properties to user into the empty object and returns it(exact same reference).
- `structuredClone(objectName); //deep copy but cannot do function error comescan handle circular reference`
- lodash cloneDeep handles everything
- `null` always remains same

## gargage collection
- only incoming connections matter
- mark and sweep algorithm

## this
- The value of this is **evaluated during the run-time, depending on the context**
- arrow function do not have this they take their parents this
## new keyword
```javascript
let user = new function() {
  this.name = "John";
  this.isAdmin = false;
}; /// or
let newuser = new function() {
  this.name = "John";
  this.isAdmin = false;
}();
```
- this way can use constructor only once
- constructor should start with capital
```javascript
function User(name){
  this.name = name;
  return this;
}
let user = new User("name");
```
- they do not have the internal [[Construct]] method that is required to be used as a constructor with the new keyword.
- arrow functions with new keyword not possible
- `new.target` tells whether function called with new or not
- if constructor does not explicitly returns anything `return;` or no return statement then returns this else

### option chaining
- If there’s no variable user at all, then user?.anything triggers an error:
- cannot assign to option chaining `user?.name = "abc"` generates error
- can delete option chain if it exists then delete it
- We can use ?. for safe reading and deleting, but not writing
- ?. immediately stops (“short-circuits”) the evaluation if the left part doesn’t exist.
- returns undefined
- `obj?.prop` `obj?.[prop]` `obj.method?.()` 
- ?. checks the left part for null/undefined and allows the evaluation to proceed if it’s not so

## symbol type
- `Symbol(anything)` creates a new symbol for everything
- `Symbol.for(key)` is same for same key global registry
- `Symbol.keyFor(symbol)` gets the key for symbol
- converts key into string then makes symbol

## type conversion of objects
- all objects are boolean true
- We can implement string and numeric conversion by ourselves, using special object methods.
- use "default" when does not know what type to expect
- Symbol.toPrimitive handles all the cases
```javascript
obj[Symbol.toPrimitive] = function(hint) {
  // hint == "string", hint == "number", hint == "default"
}
obj.toString()//string
obj.valueOf() //returns the object itself
```
### primitives as objects
```js
let x = new Number(5);
typeof x //object
```
- Primitives except null and undefined provide many helpful methods. (like str.toUpperCase())
- at the time of calling function an object is created and after usage it is destroyed
```js
let str1 = "Hello\nWorld";
let str2 = `Hello
World`;
alert(str1 == str2); // true
```
- str.at(-1) //last character
- Strings **can’t be changed** in JavaScript. **Immutable**
-  `str.indexOf(substr, pos)`. It looks for the substr in str, starting from the given position pos, and returns the position where the match was found or -1 if nothing can be found.
-  `str.includes(substr, pos)` returns true/false depending on whether str contains substr within.
- `str.startsWith(substr)`
- `str.endsWith(substr)`
- `str.substring(start,end)`  `str.slice(start,end)` and `str.substr(start,length)` does not include end for start, end
- `str.codePointAt(pos)` Returns a decimal number ascii value
- toString(16) convert to hexadecimal string
- `String.fromCodePoint(90)` convert ascii to string(char)

`str.localeCompare(str2)` //capital>smaller//TODO
- Returns a negative number if str is less than str2.
- Returns a positive number if str is greater than str2.
- Returns 0 if they are equivalent.

### numbers
- `0x` prefix for hexa decimal
- `0b` for binary
- `0o` for octal
- `toString(base)`
- `123..toString()` double dot because one for float
- `Math.floor()`
- `Math.trunc()` removes decimal part
- `Math.ceil()` 
- `Math.round()` nearest integer in case of .5 larger number
- `toFixed(n)` rounds the number to n digits after the point and returns a string representation of the result. **can help with precision losses**
- `NaN == NaN//false`
- `Number.isNaN and Number.isFinite` They do not autoconvert their argument into a number, but check if it belongs to the number type instead.
- `isNaN and isFinite` converts and then checks
- isNaN gives true for undefined
- `parseInt and parseFloat` “read” a number from a string until they can’t. In case of an error, the gathered number is returned. 
- `parseInt(str, radix) //radis is base`
- `Math.random() //between 0 to 1`
- `Math.pow(n,power)`
## arrays check method
- can store any type of data
- here also -1 works `arr.at(-1)` //last element
- array is deque in js - push, pop, unshift, shift,(push(...items)),(pop(...items))
- unshift and shift have O(n) complexity
- arrays are object in behind so `arr["key"] = "value"` will work and also creating holes also work `arr[0] =100` `arr[1000] = 100` array optimizations fail because of this
```js
for (let fruit of fruits) {//actual content
  alert( fruit );
}
for (let key in fruits) {
  //gives key
  fruits[key];
}
```
- **for..in loop is optimized for generic objects, not arrays, and thus is 10-100 times slower.**
- decreasing array.length truncates the array and returns undefined if called
- `new Array("a","b","c")` can create a new array
- `new Array(size)` can be used to create array of size and undefined elements
- If new Array is called with a single argument which is a number, then it creates an array without items, but with the given length.
-  `0 == [] `; // true
- `array.forEach((item,index,array)=>{}) //return doesnt effect`
- filter - if true return items
- map - return changed item
- reduce - 
```js
arr.reduce(function(accumulator, item, index, array) {
  // ...
  return accumulator
}, [initial]);
```
- reduceRight does same but from right
- splice - `arr.splice(start[, deleteCount, elem1, ..., elemN])` elements can be negative 
```js
let arr = [1, 2, 5];
arr.splice(-1, 0, 3, 4);
alert( arr ); //12345 //negative while inserting
```
- slice - `arr.slice(start,end)` not including end
-  arr.concat creates a new array that includes values from other arrays and additional items.  `arr.concat(arg1, arg2...)`
- sort, reverse and splice modify the array itself.
- checking `Array.isArray(arr)// since typeof gives object`
- `arr.indexOf(item, from)` – looks for item starting from index from, and returns the index where it was found, otherwise -1.(===)
- `arr.lastIndexOf(item,from)` checks from back
- `arr.includes(item, from)` – looks for item starting from index from, returns true if found. handles `NaN` correctly
- `find, findIndex, findLastIndex` takes (item, index, array)=>{} , find returns item or undefined, rest return index or -1 , if you return true then stops if false then continues;
- `arr.sort(cmp)` - items are sorted as string by default give a comparator function
- str.split(delimiter) <-> arr.join(glue) //automatiaclly takes comma if not given
- Array.isArray(arr) -> to check array typeof gives object
- exception of sort thisArg can be applied to all ***see once again***






##
- execution context stack - when parent function calls child function then the execution context of the parent is stored and the parent is paused and child runs

### rest parameters
- a function can be called with any number of parameteres rest parameters will not be used only first ones will be used
```js
function(a,b,...rests){
  for rest in rests {
    //perform
  }
}
```
- rest should be at the end of the arguments
- in `function` based methods there is a special `arguments` object (keyed like array)  can be used to access any argument with which the method has been called
#### spread operator ...
- [...arr1, ...arr2] can be used to merge 2 arrays
- also be used to call functions with multiple parameters (must be at the last)
- string into array of characters `Array.from(string)` `let arr = [...string]`;
- **Spread syntax requires ...iterable[Symbol.iterator] to be a function**

## var
- var are either **function-scoped or global-scoped**
- var can be shadows by another var (not by let)
- var can be declared anywhere in its scope

## iife immediately invoked function expression
(declaration vs expression)
- parentheses around the function is a trick to show JavaScript that the function is created in the context of another expression, and hence it’s a Function Expression: it needs no name and can be called immediately.

##
- let is block scoped

## lexical environment
- **environment records** **outer reference**
- environment record stores all local variable as property and also this
#### function declaration
- Function Declaration is instantly fully initialized. When a Lexical Environment is created, a Function Declaration immediately becomes a ready-to-use function (unlike let, that is unusable till the declaration). (function declaration not function expression)
- function called -> new lexical scope created -> variable searched in new lexical scope if found do operation if not -> go to outer lexical scope and repeat till global, then show error in case of use strict else error
- All functions remember the Lexical Environment in which they were made.all functions have the hidden property named [[Environment]], that keeps the reference to the Lexical Environment where the function was created;
- function called -> new lexical environment created 
-  global functions and variables declared with var (not let/const!) become the property of the global object, can call it by window.varName

function is an object  we can assign properties to it. but properties are not values
- func.name - gives the name of the function (except in case of ambiguous) -> arr = [function(){}, function(){}]
- func.length - gives the number arguments except the ...rest one
- in case of function expression it is just accessible internally

case
```js
let sayHi = function(who) {
  if (who) {
    alert(`Hello, ${who}`);
  } else {
    sayHi("Guest"); // Error: sayHi is not a function
  }
};

let welcome = sayHi;
sayHi = null;

welcome();//error single sayHi is null
```

#### converting string to function 
- `new Function(arg1,arg2, ...restArgs, function)` -> `let sum = new Function('a', 'b', 'return a + b');alert( sum(1, 2) );`
- does not remember environment created just knows global variables

## scheduling functionto run
- `let timerId = setTimeout(func|code, delay, arg1, arg2, ...)`
- runs for once (write function not call it)
- cancel timeout using `cancelTimeout(timerId)`
- `let timerId = setInterval(func|code, delay, arg1, arg2, ...)`
- runs again and again
- cancel interval using `cancelInterval(timerId)`
- nested setInterval will produce a lots of thing exponential in time
- nested setTimeout can be used in place of setInterval will run then wait then run (in set interval waiting and running together)
- zero delay is not running it instantly but when free then run it instantly

## decorators
- since function retains the variables or the envinronment in which they were created can be used for extra things
```js
//caching
function cachingDecorator(func) {
  let cache = new Map();
  return function(x) {
    if (cache.has(x)) {
      return cache.get(x);
    }
    let result = func(x); // no context calling cannot be used on object functions directly
    cache.set(x, result);
    return result;
  };
}
```

### call forwarding and method borrowing
- func.call(context, …args) that allows to call a function explicitly setting this can be used for object things
- func.apply(context,arg) // only difference is have to open argument in call while array-like iterable object in apply
- apply works faster //iterable
- Passing all arguments along with the context to another function is called call forwarding.
```js
let wrapper = function() {
  return func.apply(this, arguments);
};
```
- apply is array like so we cannot call join 
```js
[].join.call(arguments);
```
Let glue be the first argument or, if no arguments, then a comma ",".
Let result be an empty string.
- Append this[0] to result.
- Append glue and this[1].
- Append glue and this[2].
…Do so until this.length items are glued.
Return result.
So, technically it takes this and joins this[0], this[1] …etc together. It’s intentionally written in a way that allows any array-like this (not a coincidence, many methods follow this practice). That’s why it also works with this=arguments.
- decorators cannot access the properties of the internal function

### function binding
- after function bind then obj.func will give this bind object not obj
- in case of setTimeouts we can loose context wrap function in another function
```js
setTimeout(() => user.sayHi(), 1000);
```

- create another function binding it
`let boundFunc = extSayHi.bind(user)` //bind any external function
- when object functions are used somewhere else then should bind function with this (all the functions ideally)
```js
for key in obj {
  if(typeof obj[key] === 'function') {
    obj[key] = obj[key].bind(obj);
  }
}
```
- `let bound = func.bind(context, arg1, arg2, ...);`
#### partial functions
```js
function mul(a, b) {
  return a * b;
}
let triple = mul.bind(null, 3);
```
- here  null is context and 3 is the first argument
##### partial function without context
```js
function partial(func, ...argsBound) {
  return function(...args) { // (*)
    return func.call(this, ...argsBound, ...args);
  }
}
```

## prototypal inheritance
- \_\_proto__ is setter or getter of [[Prototype]]
- points to another object (something like parent object)
- first searches in current object then moves in parent object and then searches ...
- cannot make circular gives error

way to make setter and getter //not called as function but directly used as properties
```js
let user = {
  name: "John",
  surname: "Smith",
  set fullName(value) {
    [this.name, this.surname] = value.split(" ");
  },
  get fullName() {
    return `${this.name} ${this.surname}`;
  }
};
let admin = {
  __proto__: user,
  isAdmin: true
};
```
- this is not affected by prototypes at all.
- No matter where the method is found: in an object or its prototype. In a method call, this is always the object before the dot.
- `Object.keys(obj)` returns its own properties
```js
for (let key in obj) {
  //return inherited keys also
}
```
- `obj.hasOwnProperty(key)` it returns true if obj has its own (not inherited) property named key

### F.prototype
- its not functional prototype but if we call function with new then the object created will have [[Prototype]] set equal to prototype
- F.prototype only used at new F time
- if we do not assign prototype of function then automatically and object with constructor property is made and assigns the constructor to the object that it makes through new
- can use constructor to make copy of that object
- if we assign function prototype without constructor then object won't have its constructor
`let obj = new Object()`
`Object.prototype.constructor = obj.constructor = Object`
```js
let arr = [1, 2, 3];
alert( arr.__proto__ === Array.prototype ); // true
alert( arr.__proto__.__proto__ === Object.prototype ); // true
alert( arr.__proto__.__proto__.__proto__ ); // null
```
- we can modify native prototype methods also //can create conflit
- `Number.prototype.func = someFunctoin`
- in case of polyfill can use it
```js 
//borrowing
let obj = {
  0: "Hello",
  1: "world!",
  length: 2,
};
obj.join = Array.prototype.join;
alert( obj.join(',') ); // Hello,world!
```
-  built-in join method only cares about the correct indexes and the length property. It doesn’t check if the object is indeed an array.

#### without __proto__
- `Object.getPrototypeOf(obj)` return [[Prototype]] of object
- `Object.setPrototypeOf(obj,proto)` sets the prototype of object as proto
while initializing if want to set prototype then
`Object.create(proto, descriptors)` where descriptor has a certain format
- `Object.getOwnPropertyDescriptors(obj)`
- ...

# class
```js
class MyClass {
  constructor() { ... }
  method1() { ... }
  method2() { ... }
  method3() { ... }
  ...
}
```
- class called without new error
- class called with new returns this even if absurd thing is returned


# promise
- The executor should call only one resolve or one reject. Any state change is final.
- All further calls of resolve and reject are ignored
```js
let promise = new Promise(function(resolve, reject) {
  resolve("done");
  reject(new Error("…")); // ignored
  setTimeout(() => resolve("…")); // ignored
});
```
```js
promise.then(
  function(result) { /* handle a successful result */ },
  function(error) { /* handle an error */ }
);
```
catch
If we’re interested only in errors, then we can use null as the first argument: .then(null, errorHandlingFunction). Or we can use .catch(errorHandlingFunction),

.finally(f) is similar to .then(f, f) ;  finally(f) isn’t exactly an alias of then(f,f) though.

A finally handler doesn’t get the outcome of the previous handler (it has no arguments). This outcome is passed through instead, to the next suitable handler.
If a finally handler returns something, it’s ignored.
When finally throws an error, then the execution goes to the nearest error handler.
For instance, here the result is passed through finally to then
```js
new Promise((resolve, reject) => {
  setTimeout(() => resolve("value"), 2000);
})
  .finally(() => alert("Promise ready")) // triggers first
  .then(result => alert(result)); // <-- .then shows "value"
```

multiple handlers for one promise.
```js
let promise = new Promise(function(resolve, reject) {
  setTimeout(() => resolve(1), 1000);
});

promise.then(function(result) {
  alert(result); // 1
  return result * 2;
});

promise.then(function(result) {
  alert(result); // 1
  return result * 2;
});

promise.then(function(result) {
  alert(result); // 1
  return result * 2;
});
```
All .then on the same promise get the same result – the result of that promise. So in the code above all alert show the same: 1.

promise handlers has an "invisible try..catch" around it

```js
new Promise((resolve, reject) => {
  throw new Error("Whoops!");
}).catch(alert); // Error: Whoops!
```
similar as
```js
new Promise((resolve, reject) => {
  reject(new Error("Whoops!"));
}).catch(alert); // Error: Whoops!
```
- programming error also goes in catch
- if you do not catch promise error then becomes global error and thrown in console.

`let promise = Promise.all(iterable);`
- waits for all the promises to resolve //execute promise in parallel
```js
let requests = urls.map(url => fetch(url));
// Promise.all waits until all jobs are resolved
Promise.all(requests)
  .then(responses => responses.forEach(
    response => alert(`${response.url}: ${response.status}`)
  ));
```
- If any of the promises is rejected, the promise returned by Promise.all immediately rejects with that error.
- In case of an error, other promises are ignored (may be they run but nothing happens with their result)
- `Promise.allSettled()` - returns all the results (as resolved) can check result.status = "fulfilled"/"rejected"
- `Promise.race`
Similar to Promise.all, but waits only for the first settled promise and gets its result (or error).
- `Promise.any` similar Promise.race, but waits only for the first fulfilled promise and gets its result. If all of the given promises are rejected, then the returned promise is rejected with AggregateError – a special error object that stores all promise errors in its errors property.
- `Promise.resolve(value)` == `let promise = new Promise(resolve => resolve(value));`
- `Promise.reject(value)` == `let promise = new Promise(reject => reject(value));`
- promisify - util.promisify
- in place of callback give a function on error rejet(error) else resolve(data) 
- `async` functions return promise only -> other values are wrapped in promise only `return Promise.resolve(data);` <-> `return data;`
- `await` on promise stops the code their when promise finishes then only continue; returns the result of promise
- cannot await in regular functions
- await can be used outside all functions
- await accepts thenable objects
- for catching error we can use try catch syntax
```js
try {
  await asynfunc();
} catch(err) {
  alert(err);
}
```

## try/catch
```js
try {
  // code...
} catch (err) {
  // error handling
}
```
- first try code is executed
- if error found stopped execution there and catch gets error and executes
- if no error the catch ignored

- **try...catch only works for runtime errors** not with syntax errors try{{{{}catch{}//won't work
-  try catch works synchronously

```js
try {
  setTimeout(function() {
    noSuchVariable; // script will die here
  }, 1000);
} catch (err) {
  alert( "won't work" );
}
```
- throwing anything `throw 1;` will be catched
- wrap try catch in function throw inside catch  then call function in try then recatch
- try catch then finally - finally always runs //just try and finally if do not want to handle errors

global error catching
```js
window.onerror = function(message, url, line, col, error) {
  // ...
};
```

#### creating self errors TODO - class
```js
class ValidationError extends Error {
  constructor(message) {
    super(message); // (1)
    this.name = "ValidationError"; // (2)
  }
}
//checking error type
if (err instanceof ValidationError ) {
  alert("validation error");
}
```




- current execution priority > microtask priority > macrotask priority
- micro - promises
- macro - setTimeouts
```js
console.log('Start');
setTimeout(() => {
  console.log('Macrotask: setTimeout');
}, 0);
Promise.resolve().then(() => {
  console.log('Microtask: Promise');
});
console.log('End');
```
# Document
## cookie
- document.cookie is setter or getter
- `document.cookie = "key=value"` just adds new key value or update never deletes anything
- domain attribute allows to make a cookie accessible at subdomains.
```js
// make the cookie accessible on any subdomain *.site.com:
document.cookie = "user=John; domain=site.com"
```
- `path=/mypath` The URL path prefix must be absolute. It makes the cookie accessible for pages under that path. By default, it’s the current path. -> If a cookie is set with path=/admin, it’s visible on pages /admin and /admin/something, but not at /home, /home/admin or /.
```js
//expires or max-age attribute. max-Age has precedence if both are set.
//expires=Tue, 19 Jan 2038 03:14:07 GMT
// cookie will die in +1 hour from now
document.cookie = "user=John; max-age=3600";//just user one rest will remain
```
- `secure` attribute makes available only on https not http by default on both
- `httpOnly` doesn't allow that cookie to be seen by javascript of the browser 
- xsrf - cross site request forgery - js used to submit to another site so from browser will send cookie 
- `samesite=strict` is never sent if the user comes from outside the same site.
- `samesite=lax` 
The HTTP method is “safe” (e.g. GET, but not POST).

The operation performs a top-level navigation (changes URL in the browser address bar).

This is usually true, but if the navigation is performed in an \<iframe>, then it is not top-level. Additionally, JavaScript methods for network requests do not perform any navigation.

### localStorage //preferences used more

iteration on localStorage
```js
for(let i=0; i<localStorage.length; i++) {
  let key = localStorage.key(i);
  alert(`${key}: ${localStorage.getItem(key)}`);
}
```
- setItem(key, value) – store key/value pair.
- getItem(key) – get the value by key.
- removeItem(key) – remove the key with its value.
- clear() – delete everything.
- key(index) – get the key on a given position.
- length – the number of stored items.

#### only stores string
- ` for key in localStorage `  shows extra things we can check it by `localStorage.hasOwnProperty(key)`
- or use `Object.keys(localStorage)`

### sessionStorage
- just exists in current tab and current url
- Survives page refresh (but not tab close)
- The important thing is: the event triggers on all window objects where the storage is accessible, except the one that caused it.
- key – the key that was changed (null if .clear() is called).
- oldValue – the old value (null if the key is newly added).
- newValue – the new value (null if the key is removed).
- url – the url of the document where the update happened.
- storageArea – either localStorage or sessionStorage object where the update happened.


##
- Document Object Model, DOM, has all page content as objects that can be modified.
- The document object is the main “entry point” to the page. create or change anything
- CSSOM - for handeling css rule and style sheet 
- CSSOM is used together with the DOM when we modify style rules
-  Browser Object Model (BOM) represents additional objects provided by the browser like navigator, location, alert(), prompt(), confirm()

### dom tree
- every tag is an object
- spaces between tags (are not important)
- Spaces and newlines before \<head> are ignored for historical reasons.
- If we put something after \</body>, then that is automatically moved inside the body, at the end

- browser correct html automatically
- tbody added automatically in table if not present
- even comments are in the tree
- document, element, text, comment
- last selected element is available as `$0`, the previously selected is `$1` etc. in the console
- \<html> = document.documentElement
- \<body> = document.body
- \<head> = document.head
- In the DOM world null means “doesn’t exist”
- inside head if js is running then till then body is not created hence will show document.body as null
- `childNodes` return iterable object also has `firstChild` and `lastChild`
-  childNodes looks like an array. But actually it’s not an array, but rather a collection
- not all array method works
- DOM collections are read only we cannot change dom by modifying collections
- childNodes we can see both text nodes, element nodes, and even comment nodes if they exist.
- For all nodes: parentNode, childNodes, firstChild, lastChild, previousSibling, nextSibling.
- For element nodes only: parentElement, children, firstElementChild, lastElementChild, previousElementSibling, nextElementSibling. //for modifying
```js
//exceptino
alert( document.documentElement.parentNode ); // document
alert( document.documentElement.parentElement ); // null
//document is not an element node, so parentNode returns it and parentElement does not.
```
- tables have more accessing methods

## searching getElement querySelector
- id should be unique
- `document.getElementById("elementId")` or `elementId` to select the element do not use elementId because may be a javascript variable with same name may be present .
```js
let elements = document.querySelectorAll('ul > li:last-child');
for (let elem of elements) {
  alert(elem.innerHTML); // "test", "passed"
}
```
- `document.querySelectorAll('any css selector')`  array of elements that have same selector
- `elem.querySelector(css)` returns the first element for the given CSS selector.
-  `elem.matches(css)` does not look for anything, it merely checks if elem matches the given CSS-selector. It returns true or false.
- these two methods return live collection of elements
- `document.getElementsByClassName('class-name')`
- `document.getElementsByTagName('tagName')`
- `document.getElementsByName(name)` returns elements with the given name attribute, document-wide. Very rarely used.
```js
alert( document.body instanceof HTMLBodyElement ); // true
alert( document.body instanceof HTMLElement ); // true
alert( document.body instanceof Element ); // true
alert( document.body instanceof Node ); // true
alert( document.body instanceof EventTarget ); // true
```
- The tagName property exists only for Element nodes.
- The nodeName is defined for any Node:
- xml mode is case sensitive
-  innerHTML property allows to get the HTML inside the element as a string. We can also modify it
- If innerHTML inserts a \<script> tag into the document – it becomes a part of HTML, but doesn’t execute.
- `innerHTML`
The HTML content of the element. Can be modified.
- “innerHTML+=” does a full overwrite everything inside it is reloaded
- `outerHTML`
The full HTML of the element. A write operation into elem.outerHTML does not touch elem itself. Instead it gets replaced with the new HTML in the outer context.
- `textContent` provides access to the text inside the element
- `element.hidden = true` makes display none in styles

- when an element has id or another standard attribute, the corresponding property gets created. But that doesn’t happen if the attribute is non-standard.
```js
//non standard properties accesed by
elem.hasAttribute(name)// – checks for existence.
elem.getAttribute(name)// – gets the value.
elem.setAttribute(name, value) //– sets the value.
elem.removeAttribute(name)// – removes the attribute
```
- When a standard attribute changes, the corresponding property is auto-updated, and (with some exceptions) vice versa. instance input.value synchronizes only from attribute → property, but not back

- `input.setAttribute('id', 'id');`
- All attributes starting with “data-” are reserved for programmers’ use. They are available in the dataset property.

- two methods to create elements of html
- `document.createElement(tag)`
- `document.createTextNode(text)`
```js
node.append(...nodes or strings)// – append nodes or strings at the end of node,
node.prepend(...nodes or strings)// – insert nodes or strings at the beginning of node,
node.before(...nodes or strings)// –- insert nodes or strings before node,
node.after(...nodes or strings)// –- insert nodes or strings after node,
node.replaceWith(...nodes or strings)// –- replaces node with the given nodes or strings.
```
- versatile method to insert
```js
elem.insertAdjacentHTML(where, html)
```
```js
"beforebegin"// – insert html immediately before elem,
"afterbegin"// – insert html into elem, at the beginning,
"beforeend"// – insert html into elem, at the end,
"afterend"// – insert html immediately after elem.
```
- `node.remove()` removes node but in case of moving no need to remove old one
```js
let div2 = div.cloneNode(true); // clone the message
  div2.querySelector('strong').innerHTML = 'Bye there!'; // change the clone
  div.after(div2);
```
- DocumentFragment is a special DOM node that serves as a wrapper to pass around lists of nodes.

```js
function getListContent() {
  let fragment = new DocumentFragment();
  for(let i=1; i<=3; i++) {
    let li = document.createElement('li');
    li.append(i);
    fragment.append(li);
  }
  return fragment;
}
ul.append(getListContent()); // (*)
```

```js
elem.classList.add/remove("class")// – adds/removes the class.
elem.classList.toggle("class")// – adds the class if it doesn’t exist, otherwise removes it.
elem.classList.contains("class")// – checks for the given class, returns true/false.
```
- setting styles to empty strings can remove the property or may be `elem.style.removeProperty('background or any styleproperty')`
- `document.body.style.display = "none"; // hide` //setting styles

- `getComputedStyle(element, pseudo)` - pseudo element may be like ::before
- `:visited` pseudo claass is hidden 
- getComputedStyle(elem).padding? Nothing, only full things are given back


### browser events

-  `click` left click
- `contextmenu` right click
- `mouseout` works even if go on child element `mouseover`
- `mouseup` `mousedown` only works if inside element

- `keydown` and `keyup` works only in input tags? TODO
- submit – when the visitor submits a `<form>`.
focus – when the visitor focuses on an element, e.g. on an `<input>`.

- `DOMContentLoaded` - when the HTML is loaded and processed, DOM is fully built. can be used inside head since dom is not loaded till header is loaded

- `transitionend` – when a CSS-animation finishes.TODO

- `<button onclick="func()">`
```js
elem.onclick = function() {
    alert('Thank you');
}; //this overrides the above
```
- these two ways only one event handler can be assigned
- `<button onclick="alert(this.innerHTML)">Click me</button>` this is element
- **setAttribute doesnot** works  because it remains string
- new DOM property overrides the previous

- options
- once: if true, then the listener is automatically removed after it triggers.
- capture: the phase where to handle the event, to be covered later in the chapter Bubbling and capturing. For historical reasons, options can also be false/true, that’s the same as {capture: false/true}.
- passive: if true, then the handler will not call preventDefault(), we’ll explain that later in Browser default actions.

- `element.removeEventListener(event, handler, [options]);` to remove handler must have same location - options same??
- There exist events that can’t be assigned via a DOM-property. Only with addEventListener like DOMContentLoaded so add event listener is more universal
- when `addEventListener` receives an object as the handler, it calls `obj.handleEvent(event)` in case of an event.
- The most deeply nested element that caused the event is called a target element, accessible as `event.target`
- `event.target` is different from `event.currentTarget` currentTarget is like this
- `event.stopPropagation()` stops the move upwards, but on the current element all other handlers will run.
- To remove the handler, `removeEventListener` needs the same phase
- not only the futher capturing is stopped, but the bubbling as well

### event delegation
- rather than assigning each child event listener just assign parent and get where the event happened 
- 

- `focus` event does not bubble


```js
//counter without blocking js
function counter(maxCount){
    let i = 0;

    let internalCounter = ()=>{
        while(i<maxCount){
            i++;
            if(i%1e5 === 0){
                console.log(i);
                break;
            }
        }
        setTimeout(internalCounter,0);
    }
    internalCounter();
}
```