# class
- ES6  inheritance preferred over protypal inheritance
- return this to make chaining possible
- prefer composition over inheritance (User , UserTaxData)

# functions
- limit number of arguments to 2 max 3
- use object and destructuring pattern while passing and receiving arguments
- function should do one thing name should be given accordingly
- only one level abstraction
- side effects should be avoided by making a separate service
- do not write global function might conflict
```js
//Bad
Array.prototype.diff = function diff(comparisonArray) {
  const hash = new Set(comparisonArray);
  return this.filter(elem => !hash.has(elem));
};

//Good
class SuperArray extends Array {
  diff(comparisonArray) {
    const hash = new Set(comparisonArray);
    return this.filter(elem => !hash.has(elem));
  }
}
```
# variables
- Use default parameters instead of short-circuiting or conditionals
- make setters and getters instead of opening direct variable
- `Object.freeze(obj)` to make constant object

# comments 
- do not leave commented code 
- just write for which the code is clumsy
- write about input arguments and output (usage of the function)

# Formatting
```ts
const DAYS_IN_WEEK = 7;
const DAYS_IN_MONTH = 30;

const SONGS = ["Back In Black", "Stairway to Heaven", "Hey Jude"];
const ARTISTS = ["ACDC", "Led Zeppelin", "The Beatles"];

function eraseDatabase() {}
function restoreDatabase() {}

class Animal {}
class Alpaca {}
```
- keep lines under 80–120 characters long in our codebase we have a ESLint rule for 200 char limit, but for better readability we should try to keep it under 120 characters

```ts
// Bad line length
const result = doSomething(veryLongParameterOne, veryLongParameterTwo, veryLongParameterThree, veryLongParameterFour);

// Good line length
const result = doSomething(
    veryLongParameterOne, veryLongParameterTwo,
    veryLongParameterThree, veryLongParameterFour
);
```
-  incorporate blank lines to improve the code formatting
- Function callers and callees should be close


