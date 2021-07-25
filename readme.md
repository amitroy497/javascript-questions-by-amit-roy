# JavaScript Questions

## Possible ways to create object in JavaScript

#### Object Constructor :-

The simplest way to create an empty object is using the Object constructor.

![object-constructor](./readme-images/ways-to-create-objects/object-constructor.PNG)

#### Object's create method :-

The create method of Object creates a new object by passing the prototype object as a parameter.

![object-create-method](./readme-images/ways-to-create-objects/object-create-method.PNG)

#### Function constructor :-

Create any function and apply the new operator to create object instances.

![function-constructor](./readme-images/ways-to-create-objects/function-constructor.PNG)

#### Function constructor with prototype :-

This is similar to function constructor but it uses prototype for their properties and methods.

![function-constructor-with-prototype](./readme-images/ways-to-create-objects/function-constructor-with-prototype.PNG)

This is equivalent to an instance created with an object create method with a function prototype and then call that function with an instance and parameters as arguments.

![function-constructor-with-prototype-2](./readme-images/ways-to-create-objects/function-constructor-with-prototype-2.PNG)

##### (OR)

![function-constructor-with-prototype-3](./readme-images/ways-to-create-objects/function-constructor-with-prototype-3.PNG)

#### ES6 class syntax :-

ES6 introduces class feature to create the objects.

![es6-class-syntax](./readme-images/ways-to-create-objects/es6-class-syntax.PNG)

#### Singleton pattern :-

A Singleton is an object which can only be instantiated one time. Repeated calls to its constructor return the same instance and this way one can ensure that they don't accidentally create multiple instances.

```javascript
var object = new (function () {
  this.name = 'Amit'
})()
```

## Prototype chain

**Prototype chaining** is used to build new types of objects based on existing ones. It is similar to inheritance in a class based language.

The prototype on object instance is available through **Object.getPrototypeOf(object)** or **_proto_** property whereas prototype on constructors function is available through Object.prototype.
