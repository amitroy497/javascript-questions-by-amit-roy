# JavaScript Questions

## Possible ways to create object in JavaScript

#### Object Constructor :-

The simplest way to create an empty object is using the Object constructor.

```javascript
var object = new Object()
```

#### Object's create method :-

The create method of Object creates a new object by passing the prototype object as a parameter.

```javascript
var obj = Object.create(null)
```

#### Function constructor :-

Create any function and apply the new operator to create object instances.

```javascript
function Person(name) {
  var obj = {}
  obj.name = name
  obj.age = 28
  return obj
}

var obj = new Person('Amit')
```

#### Function constructor with prototype :-

This is similar to function constructor but it uses prototype for their properties and methods.

```javascript
function Person() {}
Person.prototype.name = 'Amit'
var obj = new Person()
```

This is equivalent to an instance created with an object create method with a function prototype and then call that function with an instance and parameters as arguments.

```javascript
function func {}

new func(x, y, z)
```

**(OR)**

```javascript
// Create a new instance using function prototype
var newInstance = Object.create(func.prototype)

// Call the function
var result = func.call(newInstance, x, y, z)

// If the result is a non-null object then use it otherwise just use the new instance.
console.log(result && typeof result === 'object' ? result : newInstance)
```

#### ES6 class syntax :-

ES6 introduces class feature to create the objects.

```javascript
class Person {
  constructor(name) {
    this.name = name
  }
}

var obj = new Person('Amit')
```

#### Singleton pattern :-

A Singleton is an object which can only be instantiated one time. Repeated calls to its constructor return the same instance and this way one can ensure that they don't accidentally create multiple instances.

```javascript
var object = new (function () {
  this.name = 'Amit'
})()
```

## Prototype chain

**Prototype chaining** is used to build new types of objects based on existing ones. It is similar to inheritance in a class based language.

The prototype on object instance is available through **Object.getPrototypeOf(object)** or **_proto_** property whereas prototype on constructors function is available through **Object.prototype**.

Whenever we create an object. JS engine automatically attaches an object to our object, and by this way we get access to the default properties and methods.

```javascript
let arr = ['Amit', 'Roy']
arr._proto_._proto_
```

![array-prototype](./readme-images/prototype-chain/array-prototype.PNG)

**arr.\_proto\_** is same as **Array.prototype**.

**arr.\_proto\_._proto\_** is same as **Object.prototype**.

**arr.\_proto\_._proto\_._proto\_** is **null**.

![prototype-chain](./readme-images/prototype-chain/prototype-chain.png)

## Call, Apply and Bind

![call-apply-bind](./readme-images/call-apply-bind/call-apply-bind.jpg)

**Call** invokes the function with a given **this** value and allow us to pass the arguments one by one.

**Apply** invokes the function with a given **this** value and allow us to pass in arguments as an array.

**Bind** returns a function allowing us to pass any number of arguments.

```javascript
let employee1 = { firstName: 'Jack', lastName: 'Sparrow' }
let employee2 = { firstName: 'John', lastName: 'Carter' }

function invite(greeting1, greeting2) {
  console.log(`${greeting1} ${this.firstName} ${this.lastName}, ${greeting2}`)
}
```

### Call

```javascript
invite.call(employee1, 'Hello', 'How are you?')
invite.call(employee2, 'Hello', 'How are you?')
```

### Apply

```javascript
invite.apply(employee1, ['Hello', 'How are you?'])
invite.apply(employee2, ['Hello', 'How are you?'])
```

### Bind

```javascript
let inviteEmployee1 = invite.bind(employee1)
let inviteEmployee2 = invite.bind(employee2)

inviteEmployee1('Hello', 'How are you?')
inviteEmployee2('Hello', 'How are you?')
```

## Difference between Slice and Splice

| Slice                                        | Splice                                          |
| -------------------------------------------- | ----------------------------------------------- |
| Doesn't modify the original array(immutable) | Modifies the original array(mutable)            |
| Returns the subset of original array         | Returns the deleted elements as array           |
| Used to pick the elements from array         | Used to insert or delete elements to/from array |

## How arrow functions are different from lambda functions

An arrow function is a shorter syntax for a function expression and does not have its own **this**, **arguments**, **super**, or **new.target**.

These functions are best suited for non-method functions, and they cannot be used as constructors.

## First class function

In Javascript, functions are first class objects.

First-class functions means when **functions in that language are treated like any other variable**.

For example, a function can be passed as an argument to other functions, can be returned by another function and can be assigned as a value to a variable, etc.

## First order function

First-order function is a function that **doesn’t accept another function as an argument** and **doesn’t return a function as its return value**.

```javascript
const firstOrder = () => console.log('I am a First Order Function.')
```

## High order function

Higher-order function is a **function that accepts another function as an argument or returns a function as a return value or both**.

```javascript
const firstOrderFunc = () => console.log('I am a First Order Function')

const higherOrder = (returnFirstOrderFunc) => {
  returnFirstOrderFunc()
}

higherOrder(firstOrderFunc)
```

## Unary function

Unary function (i.e. monadic) is a **function that accepts exactly one argument**.

It stands for a single argument accepted by a function.

```javascript
const unaryFunction = (a) => {
  console.log(a + 10)
}
```

## Currying function

Currying is the **process of taking a function with multiple arguments and turning it into a sequence of functions each with only a single argument**.

Currying is named after a mathematician **Haskell Curry**.

By applying currying, a n-ary function turns it into a unary function.

```javascript
const multiArgFunction = (a, b, c) => {
  a + b + c
}

console.log(multiArgFunction(1, 2, 3)) // 6

const curryUnaryFunction = (a) => (b) => (c) => {
  a + b + c
}

curryUnaryFunction(1) // returns a function: b => c =>  1 + b + c

curryUnaryFunction(1)(2) // returns a function: c => 3 + c

curryUnaryFunction(1)(2)(3) // returns the number 6
```

Curried functions are great to improve **code reusability** and **functional composition**.

## Pure function

A **Pure function** is a function where the return value is only determined by its arguments without any side effects.

i.e, If we call a function with the same arguments 'n' number of times and 'n' number of places in the application then it will always return the same value.

```javascript
//Impure
let numberArray = []
const impureAddNumber = (number) => {
  numberArray.push(number)
}

//Pure
const pureAddNumber = (number) => (argNumberArray) => {
  argNumberArray.concat([number])
}

//Display the results
console.log(impureAddNumber(6)) // returns 1
console.log(numberArray) // returns [6]

console.log(pureAddNumber(7)(numberArray)) // returns [6, 7]
console.log(numberArray) // returns [6]
```

As per above code snippets, **Push** function is impure itself by altering the array and returning an push number index which is independent of parameter value.

Whereas **Concat** on the other hand takes the array and concatenates it with the other array producing a whole new array without side effects. Also, the return value is a concatenation of the previous array.

Pure functions are important as they simplify unit testing without any side effects and no need for dependency injection.

They also avoid tight coupling and make it harder to break your application by not having any side effects.

These principles are coming together with **Immutability** concept of ES6 by giving preference to **const** over **let** usage.

## Memorization

Memoization is a programming technique which attempts to **increase a function’s performance by caching its previously computed results**.

Each time a memoized function is called, its parameters are used to index the cache.

If the data is present, then it can be returned, without executing the entire function. Otherwise the function is executed and then the result is added to the cache.

```javascript
const memorizeAddition = () => {
  let cache = {}
  return (value) => {
    if (value in cache) {
      console.log('Fetching from cache')
      return cache[value]
      // Here, cache.value cannot be used as property name starts with the number which is not a valid JavaScript  identifier. Hence, can only be accessed using the square bracket notation.
    } else {
      console.log('Calculating result')
      let result = value + 20
      cache[value] = result
      return result
    }
  }
}

// returned function from memorizeAddition
const addition = memorizeAddition()

console.log(addition(20)) //output: 40 calculated
console.log(addition(20)) //output: 40 cached
```

## React.memo vs. useMemo Hooks

React.memo is a **higher-order component (HOC) which accepts a react component and an optional function that uses props to conditionally update the component using memoization**.

Whereas useMemo is a react hook that will **accept a function and a dependency array and then memoize the value returned from the function passed into it**.

In useMemo it **remembers the value returned between renders**.

In React.memo it **remembers the react component between renders**.

## How do dependencies get managed with React.memo vs useMemo?

Dependencies here mean the values/variables that will cause our memoized function or component to re-render or re-run when new values are passed in.

### Dependencies with React.memo

In React.memo we need to provide our react component as well as an optional function to handle when it should be updated.

If we don’t provide the optional function React.memo will automatically shallowly compare our props and re-render whenever they change.

The function we provide will handle the dependencies by accepting 2 parameters which are the previous and the next props.

It is then our job to use the previous and next props to decide if our component needs to be re-rendered by returning a boolean of either true or false.

React.memo’s dependency function expects to have the question of _"Are the props still the same?"_ answered.

With that in mind, if we return true we are saying that, _"Yes, the props are the same, please don't re-render this component"_.

If we return false, we are saying _"No, these props are not the same, please re-render my component"_.

### Dependencies with useMemo

useMemo handles dependencies slightly differently than React.memo.

useMemo, instead of a function with props, it accepts a dependency array for the second argument.

The dependency array in useMemo, will check for changes in the array between renders, if any of the values have changed then it will re-run our function to get a new memoized value.

## Temporal Dead Zone

The Temporal Dead Zone is a behavior in JavaScript that occurs when declaring a variable with the let and const keywords, but not with var.

In ECMAScript 6, accessing a `let` or `const` variable before its declaration (within its scope) causes a _ReferenceError_.

**The time span when that happens, between the creation of a variable’s binding and its declaration**, is called the temporal dead zone.

```javascript
function someMethod() {
  console.log(counter1) // undefined
  console.log(counter2) // ReferenceError
  var counter1 = 1
  let counter2 = 2
}
```

## Closures

A closure is the combination of a function and the lexical environment within which that function was declared. i.e, It is an inner function that has access to the outer or enclosing function’s variables. The closure has three scope chains

1. Own scope where variables defined between its curly brackets
2. Outer function’s variables
3. Global variables

```javascript
function Welcome(name) {
  var greetingInfo = function (message) {
    console.log(message + ' ' + name)
  }
  return greetingInfo
}
var myFunction = Welcome('John')
myFunction('Welcome ') //Output: Welcome John
myFunction('Hello Mr.') //output: Hello Mr.John
```

As per the above code, the inner function(i.e, greetingInfo) has access to the variables in the outer function scope(i.e, Welcome) even after the outer function has returned.
