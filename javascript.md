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
function showMessage(from, text = "no text given") {// just incase of undefined in case of null use ??
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
- `Boolean(anything)` 0,"",null,undefined becomes false; rest true

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




