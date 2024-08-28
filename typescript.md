- "strict": true in a tsconfig.json toggles them all on simultaneously
- Turning on the noImplicitAny flag will issue an error on any variables whose type is implicitly inferred as any. //infer if gets any gives error

## data types
- `string`, `number`, `boolean`, `bigint`(added es2020), 
- arrays as `number[]`, `string[]`
- `any` to skip typechecking although `noImplicitAny` gives this as error
- `let myName: string = "Alice";` variable declaration
- `function greet(name: string)` function parameter type annotation
- `function getFavoriteNumber(): number` function return type annotation
- `function printCoord(pt: { x: number; y: number })` object types
- optional properties - `obj: { first?: string; last: string }`
- in case of optional property first have to check(it is not undefined) then only use it 

### union types
- `id: number | string`
- if want to use a function of particular type first check it is of particular type
####  type narrowing
```ts
function printId(id: number | string) {
  if (typeof id === "string") {
    // In this branch, id is of type 'string'
    console.log(id.toUpperCase());
  } else {
    // Here, id is of type 'number'
    console.log(id);
  }
}
```
- union where all the members have something in common can be used directly without checking


### type alias
- can make new types or reassign the old one
- ex `type ID = number | string;`
```ts
type stringType = string;
let z: string = "abc"
let y: stringType = "afhd";
y = z; //legal
```
### interface alias
- An interface declaration is another way to name an object type.
```ts
//comparison
interface Animal {
  name: string;
}
interface Bear extends Animal {
  honey: boolean;
}
// both will do the same 
type Animal = {
  name: string;
}
type Bear = Animal & { 
  honey: boolean;
  name: number|string;
}
//here error because of duplicate identifiers
```

```ts
//adds new fields to interface
interface Window {
  title: string;
}
interface Window {
  ts: TypeScriptAPI;
}
// error duplicate identifier
type Window = {
  title: string;
}
type Window = {
  ts: TypeScriptAPI;
}
```

### literal type
`type x = "abc" | "bcd"

## type assertions
- changing type as intended
```ts
const a:number = "123"  as number; //gives error
const a:number = "123" as unknown as number; //works //do not use in sprinklr code
```

```ts
const myCanvas = document.getElementById("main_canvas") as HTMLCanvasElement;
const myCanvas = <HTMLCanvasElement>document.getElementById("main_canvas");
```
- also works with angle bracket annotation
- With strictNullChecks on, when a value is null or undefined, you will need to test for those values before using

### Non-null Assertion Operator (Postfix !)
// also works on undefined
```ts
function liveDangerously(x?: number | null) {
  // No error
  console.log(x!.toFixed());// stopping typescript to check null //do not use in code
}
```

#### literal types
- `alignment: "left" | "right" | "center"`

### enums
- if we assign type of any variable as some enum then we can only have those many values defined in enum
- default in enum is number
- numeric enums have auto incrementing behaviour
```ts
//string enums
enum Direction {
  Up = "UP",
  Down = "DOWN",
  Left = "LEFT",
  Right = "RIGHT",
}
```

```ts
//heterogeneous enums
enum BooleanLikeHeterogeneousEnum {
  No = 0,
  Yes = "YES",
}
```

- Enums are real objects that exist at runtime.
- enums maintain reverse mappings

- type null cannot be assigned to string
- **truthiness narrowing** - in if else narrow on basis of truthiness value
- **equality narrowing** - 
```ts
function example(x: string | number, y: string | boolean) {
  if (x === y) {
    // We can now call any 'string' method on 'x' or 'y'.
  }
}
```

- `== null` and `== undefined` both checks whether a value is either null or undefined.
- **in operator narrowing**
```ts
type Fish = { swim: () => void };
type Bird = { fly: () => void };
type Human = { swim?: () => void; fly?: () => void };
function move(animal: Fish | Bird | Human) {
  if ("swim" in animal) {
    animal;
(parameter) animal: Fish | Human
  } else {
    animal;
(parameter) animal: Bird | Human
  }
}
```
- **instanceof** narrowing 
- TypeScript looks at the right side of the assignment and narrows the left side appropriately.
- in case of conditionals runs only common properties
```ts
let x = true ?  "hello world!": 10; //invariant library for narrowing
x.toLowerCase();//not rn
```
- analysis of code based on reachability is called control flow analysis, and TypeScript uses this flow analysis to narrow types as it encounters type guards and assignments
```ts
function example() {
  let x: string | number | boolean;
  x = Math.random() < 0.5;
  console.log(x);
//let x: boolean
  if (Math.random() < 0.5) {
    x = "hello";
    console.log(x);
//let x: string
  } else {
    x = 100;
    console.log(x);
//let x: number
  }
  return x;
let x: string | number
}
```

```ts
function isFish(pet: Fish | Bird): pet is Fish { //is TODO type assertion
  return (pet as Fish).swim !== undefined; //why not as unknown as x
}
```
- when in doubt can call property of other if can be called


```ts
//TODO
type BaseAction<T, P  extends Record<string, any> | undefined = undefined> = P extends undefined ? { type: T } : {
    type: T,
    payload: P;
}

export type ClickEntityCard = BaseAction<'CLICK_CARD'>;

export type MoveEntityCard = BaseAction<'MOVE_CARD', {
    source: string;
    destination: string;
}>;

type Action = ClickEntityCard | MoveEntityCard;

const x: Action = {
    type: 'CLICK_CARD',
};
```
 

### never type
- removed all possibilities and have nothing left. In those cases, TypeScript will use a never type to represent a state which shouldn’t exist.
- never type is assignable to every type; however, no type is assignable to never (except never itself)
```ts
function getArea(shape: Shape) {
  switch (shape.kind) {
    case "circle":
      return Math.PI * shape.radius ** 2;
    case "square":
      return shape.sideLength ** 2;
    default:
      const _exhaustiveCheck: number = shape;
      return _exhaustiveCheck;
  }
}
```
```ts
interface Triangle {
  kind: "triangle";
  sideLength: number;
}
 
type Shape = Circle | Square | Triangle;
 
function getArea(shape: Shape) {
  switch (shape.kind) {
    case "circle":
      return Math.PI * shape.radius ** 2;
    case "square":
      return shape.sideLength ** 2;
    default:
      const _exhaustiveCheck: never = shape;
//Type 'Triangle' is not assignable to type 'never'.
      return _exhaustiveCheck;
  }
}
```

### function
```ts
type GreetFunction = (a: string) => void;
function greeter(fn: GreetFunction) {
}
```
- functions can also have properties
```ts
type DescribableFunction = {
  description: string;
  (someArg: number): boolean;
};
function doSomething(fn: DescribableFunction) {
  console.log(fn.description + " returned " + fn(6));
}
function myFunc(someArg: number) {
  return someArg > 3;
}
myFunc.description = "default description";
doSomething(myFunc);
```
- **construct signature**
```ts
type SomeConstructor = {
  new (s: string): SomeObject;
};
```
- Some objects, like JavaScript’s Date object, can be called with or without new.
```ts
interface CallOrConstruct {
  (n?: number): string;
  new (s: string): Date;
}
```
- problem is that the function promises to return the same kind of object as was passed in, not just some object matching the constraint.
```ts
function minimumLength<Type extends { length: number }>(
  obj: number,
  minimum: number
): Type {
  if (obj.length >= minimum) {
    return obj;
  } else {
    return { length: minimum }; //Type things are not here Type may have more fields
  }
}
```

#### overloading
```ts
function makeDate(timestamp: number): Date;
function makeDate(m: number, d: number, y: number): Date;
function makeDate(mOrTimestamp: number, d?: number, y?: number): Date {
  if (d !== undefined && y !== undefined) {
    return new Date(y, mOrTimestamp, d);
  } else {
    return new Date(mOrTimestamp);
  }
}
const d1 = makeDate(12345678);
const d2 = makeDate(5, 5, 5);
const d3 = makeDate(1, 3);//
// No overload expects 2 arguments, but overloads do exist that expect either 1 or 3 arguments.
```
- for `this` typescript understands that arrow function takes global  while the function have their own
```ts
interface DB {
  filterUsers(filter: (this: User) => boolean): User[];
}
const db = getDB();
const admins = db.filterUsers(function (this: User) {
  return this.admin;
});
```

- 
- `f: Function` equivalent to any take any return

#### rest arguments
```ts
// Inferred type is number[] -- "an array with zero or more numbers",
// not specifically two numbers
const args = [8, 5];
const angle = Math.atan2(...args);
```
- use `as const` to make typescript that size is fixed

- parameter destructuring below
#### void
-  literal function definition has a void return type, that function must not return anything.
```ts
function f2(): void {
  // @ts-expect-error
  return true;
}
```
- Contextual typing with a return type of void does not force functions to not return something
```ts
type voidFunc = () => void; //why TODO
const f1: voidFunc = () => {
  return true;
};
```


## Generics
```ts
function identity<Type>(arg: Type): Type {
  return arg;
}
let output = identity<string>("myString"); //either we can specifically set  Type 
let output = identity("myString"); // or we can allow compiler to set it
```
```ts
//writing type of generic functions
function identity<Type>(arg: Type): Type {
  return arg;
}
let myIdentity: <Input>(arg: Input) => Input = identity;
let myIdentity: { <Type>(arg: Type): Type } = identity;
```
- locking function for a single type
```ts
interface GenericIdentityFn<Type> {
  (arg: Type): Type;
}
function identity<Type>(arg: Type): Type {
  return arg;
}
let myIdentity: GenericIdentityFn<number> = identity;
```
- making generic having a particular property
```ts
interface Lengthwise {
  length: number;
}
function loggingIdentity<Type extends Lengthwise>(arg: Type): Type {
  console.log(arg.length); // Now we know it has a .length property, so no more error
  return arg;
}
```

there is currently no way to place type annotations within destructuring patterns. This is because the following syntax already means something different in JavaScript.
```ts
function draw({ shape: Shape, xPos: number = 100 /*...*/ }) {
  render(shape);
Cannot find name 'shape'. Did you mean 'Shape'?
  render(xPos);
Cannot find name 'xPos'.
}
```

```ts
interface SomeType {
  readonly prop: string;
}
```
- readonly modifier doesn’t necessarily imply that a value is totally immutable - or in other words, that its internal contents can’t be changed. It just means the property itself can’t be re-written to.
- readonly properties can also change via aliasing.
- `let readonlyPerson: ReadonlyPerson = writablePerson;`

#### index signature
```ts
interface StringArray {
  [index: number]: string;
}
const myArray: StringArray = getStringArray();
const secondItem = myArray[1];//gives string
```
- similar index properties should match the output
```ts
interface NumberOrStringDictionary {
  [index: string]: number | string;
  length: number; // ok, length is a number
  name: string; // ok, name is a string
}
```
- excess properties rejected by typescript
- index signature can be used for this purpose
- One final way to get around these checks, which might be a bit surprising, is to assign the object to another variable: Since assigning squareOptions won’t undergo excess property checks, the compiler won’t give you an error:
```
let squareOptions = { colour: "red", width: 100 };
let mySquare = createSquare(squareOptions);
```
- extends keyword on an interface allows us to effectively copy members from other named types, and add whatever new members we want


```ts
interface Person1 {
  name: string;
}
 
interface Person2 {
  name: number;
}
 
type Staff = Person1 & Person2
 
declare const staffer: Staff;
staffer.name;         //never both string and number not possible
```
//box type

- Array\<type> already defined same as type[]
- readonly array cannot be reassigned to normal array but opposite possible so can be changed



####  tuples types
- A tuple type is another sort of Array type that knows exactly how many elements it contains, and exactly which types it contains at specific positions.
- optional length tuple `type Either2dOr3d = [number, number, number?];`
- Tuples can also have rest elements, which have to be an array/tuple type.
```ts
type StringNumberBooleans = [string, number, ...boolean[]];
type StringBooleansNumber = [string, ...boolean[], number];
type BooleansStringNumber = [...boolean[], string, number];
```

```ts
function doSomething(pair: readonly [string, number]) {
  // ...
}
```

## keyof operator
- `type NewType = keyof Type` gives
```ts
type Arrayish = { [n: number]: unknown };
type A = keyof Arrayish;
//type A = number
type Mapish = { [k: string]: boolean };
type M = keyof Mapish;  
//type M = string | number
```

### indexed access types
- You can only use types when indexing, meaning you can’t use a const to make a variable reference
```ts
type Fruits = "mango"|"apple"|"grapes";
type Type = {"mango":number,"apple":number,"grapes":string};
type NewType = Type[Fuits];
//NewType = number|string;
```

```ts
const MyArray = [
  { name: "Alice", age: 15 },
  { name: "Bob", age: 23 },
  { name: "Eve", age: 38 },
];
type Person = typeof MyArray[number];   
type Person = {
    name: string;
    age: number;
}
type Age = typeof MyArray[number]["age"];   
//type Age = number
// Or
type Age2 = Person["age"];    
//type Age2 = number
```

## conditional type
-  `SomeType extends OtherType ? TrueType : FalseType;` - type on the left of the extends is assignable to the one on the right,
- generics with this can be used to do complex in single
```ts
type NameOrId<T extends number | string> = T extends number ? IdLabel : NameLabel;
//equivalent to
```
#### infer
- kind of type catching like generic, can catch type without using extra while declaring
```ts
type Flatten<Type> = Type extends Array<infer Item> ? Item : Type;
//this could have been done by
type Flatten<Type,Item> = Type extends Array<Item> ? Item : Type; 
```

## utilities

### Awaited<Type>
- leaves direct
```ts
type B = Awaited<Promise<Promise<TypeX>>>;
//or
type B = Awaited<TypeX>;
//type B = TypeX
```
### Partial<Type>
makes all the properties optional with undefined assignment possible
- leaves direct
```ts
type Type = Partial<{"name":string}>
//equivalent to
type Type = {
    name?: string | undefined;
}
```

### Required<Type>
- Constructs a type consisting of all properties of Type set to required.just removes ?
- leaves direct

### Readonly<Type>
- just applies readonly at front of each property 
- leaves direct

### Record<KeyType,ValueType>
- 'Keys' must satisfy the constraint 'string | number | symbol'
```ts
type Keys = "abc"|"bcd"|"cd";
type Values = "a"|"b";
type Type = Record<Keys,Values>;
//creates
type Type = {
    abc: Values;
    bcd: Values;
    cd: Values;
}
```

### Pick<Type,Keys>
- keeps the Keys from the keys of Type and just keep them and remove others

### Omit<Type,Keys>
- removes the Keys from the keys of Type and keep the rest 



