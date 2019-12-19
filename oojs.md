---
theme: "night"
customTheme : "me"
transition: "slide"
highlightTheme: "darkula"
title: "oojs"
---

# oojs

the principles of oojs

---

## primitive & reference types

---

### primitive

```js
// strings
var name = "Nicholas";
var selection = "a";

// numbers
var count = 25;
var cost = 1.51;

// boolean
var found = true;

// null
var object = null;

// undefined
var flag = undefined;
var ref; // assigned undefined automatically
```

--

#### identifying primitive

```js
typeof "Nicholas"; // "string"
typeof 10; // "number"
typeof 5.1; // "number"
typeof true; // "boolean"
typeof undefined; // "undefined"
```

--

#### == vs ===

```js
"5" == 5; // true
"5" === 5; // false
undefined == null; // true
undefined === null; // false
```

--

#### primitive methods

```js
var name = "Nicholas";
var lowercaseName = name.toLowerCase(); // convert to lowercase
var firstLetter = name.charAt(0); // get first character
var middleOfName = name.substring(2, 5); // get characters 2-4

var count = 10;
var fixedCount = count.toFixed(2); // convert to "10.00"
var hexCount = count.toString(16); // convert to "a"

var flag = true;
var stringFlag = flag.toString(); // convert to "true"
```

---

### reference types

reference types represent objects. Reference values are instances of reference types and are synonymous with objects. An object is an unordered list of properties consisting of a name and a value. When the value of a property is a function, it is called a method.

--

#### referencing

```js
var object1 = new Object();
var object2 = object1; //both refers to same value
```

--

#### dereferencing

```js
var object1 = new Object();
// do something
object1 = null; // dereference
```

--

#### add / remove properties

```js
var object1 = new Object();
object1.myCustomProperty = "Awesome!";
```

>can modify objects whenever you want, even if you didn’t define them in the first place.

---

### built-in types

```js
var items = new Array();
var now = new Date();
var error = new Error("Something bad happened.");
var func = new Function("console.log('Hi');"); //don't use this
var object = new Object();
var re = new RegExp("\\d+");
```

--

#### built-in types -> literal forms

```js
var items = ['red','blue','green']; //Array
var object = {'user name':'test user'}; //Object
var re = /\d+/; //Regex
function func(){"console.log('Hi');"}; //Function
```

---

### property access

```js
var method = 'push';
var array = []; //[]
array.push(12); //[12]
array['push'](34);//[12,34]
array[method](56); //[12,34,56]
```

---

### identifying reference types

```js
var items = [];
var object = {};
function reflect() {}

items instanceof Array; // true
items instanceof Object; // true

object instanceof Object; // true
object instanceof Array; // false

reflect instanceof Function; // true
reflect instanceof Object; // true
```

--

#### identifying arrays

```js
var items = [];
Array.isArray(items); // true
```

---

### primitive wrapper types

primitive wrapper types are reference types that are automatically created behind the scenes whenever strings, numbers, or Booleans are **read**

--

#### behind the scenes

```js
var name = "Nicholas";
var firstChar = name.charAt(0);
console.log(firstChar); // "N"
```

<small>what the JavaScript engine does</small>

```js
var name = "Nicholas";
var temp = new String(name);
var firstChar = temp.charAt(0);
temp = null;
console.log(firstChar);
```

---

## Functions

---

### first-class functions

- can use as any other objects
- assign to variables
- add to objects
- pass to other functions as arguments
- return from functions

---

### declarations vs expressions

```js
// function declaration
function add(num1, num2) {
    return num1 + num2;
}
```

```js
// function expression
var add = function(num1, num2) {
    return num1 + num2;
};
```

<small>*function declaration* hoists but not the *function expressions*</small>

---

### function as value

```js
function sayHi() { console.log("Hi!"); }

var sayHi2 = sayHi;

sayHi(); // outputs "Hi!"
sayHi2(); // outputs "Hi!"
```

same function created using constructor

```js
var sayHi = new Function( "console.log(\"Hi!\");" );
var sayHi2 = sayHi;

sayHi(); // outputs "Hi!"
sayHi2(); // outputs "Hi!"
```

--

```js
var numbers = [ 1, 5, 8, 4, 7, 10, 2, 6 ];

numbers.sort( function( first, second ) {
    return first - second;
    }); // "[1, 2, 4, 5, 6, 7, 8, 10]"

numbers.sort(); // "[1, 10, 2, 4, 5, 6, 7, 8]"
```

---

### parameters

- can pass **any number** of parameters to any function without causing an error
- parameters are actually stored as an **array-like** structure called arguments

--

#### named / unnamed parameters

```js
function reflect(value) {
    return value;
}
console.log(reflect("Hi!")); // "Hi!"
console.log(reflect("Hi!", 25)); // "Hi!"
console.log(reflect.length); // 1
```

same function without named parameters

```js
reflect = function() {
    return arguments[0];
};
console.log(reflect("Hi!")); // "Hi!"
console.log(reflect("Hi!", 25)); // "Hi!"
console.log(reflect.length); // 0
```

--

#### n arguments

```js
function sum() {
    var result = 0,
    i = 0,
    len = arguments.length;

    while (i < len) {
        result += arguments[i];
        i++;
    }
    return result;
}
console.log(sum(1, 2)); // 3
console.log(sum(3, 4, 5, 6)); // 18
console.log(sum(50)); // 50
console.log(sum()); // 0

```

---

### overloading

>ability of a single function to have multiple signatures

- function signature is function name, number and type of parameters that expects

- Js functions can accept n number of parameters, and the types of parameters aren’t specified
- so, Js don’t have signatures and due to that there is lack of function overloading

--

```js
function sayMessage(message) {
    console.log(message);
}

function sayMessage() {
    console.log("Default message");
}

sayMessage("Hello!"); // outputs "Default message"
```

--

#### overload mimic

```js
function sayMessage(message) {
    if (arguments.length === 0) {
        message = "Default message";
    }
    console.log(message);
}
sayMessage("Hello!"); // outputs "Hello!"
```

<small>checking the named parameter against `undefined` is more common than relying on `arguments.length`</small>

---

### object Methods

if a object property value is a **function**, the property is considered a **method**

```js
var person = {
    name: "Nicholas",
    sayName: function() {
        console.log(person.name);
    }
};
person.sayName(); // outputs "Nicholas"
```

---

### `this` object

all scope in Js has a `this` object that represents the calling object for the function.

- global scope, `this` represents the global object
- function scope attached to an object, the value of `this` is equal to that object by default

--

```js
var person = {
    name: "Nicholas",
    sayName: function() {
        console.log(this.name);
    }
};
person.sayName(); // outputs "Nicholas"
```

--

```js
function sayNameForAll() {
    console.log(this.name);
}

var person1 = {
    name: "Nicholas",
    sayName: sayNameForAll
};

var name = "Michael";

person1.sayName(); // outputs "Nicholas"
sayNameForAll(); // outputs "Michael"
```

--

#### changing `this`

three function methods that allow you to change the value of `this`.

- `call()`
- `apply()`
- `bind()`

--

##### `call()`

```js
function sayNameForAll(label) {
    console.log(label + ":" + this.name);
}
var person1 = {
    name: "Nicholas"
};

var name = "Michael";
sayNameForAll.call(this, "global"); // outputs "global:Michael"
sayNameForAll.call(person1, "person1"); // outputs "person1:Nicholas"
```

--

##### `apply()`

```js
function sayNameForAll(label) {
    console.log(label + ":" + this.name);
}

var person1 = {
    name: "Nicholas"
};

var name = "Michael";
sayNameForAll.apply(this, ["global"]); // outputs "global:Michael"
sayNameForAll.apply(person1, ["person1"]); // outputs "person1:Nicholas"
```

<small> it behaves exactly as `call()` except it accepts `this` and `array` like parameters to avoid multiple named parameters </small>

--

##### `bind()`

```js
// same as previous example
// create a function just for person1
var sayNameForPerson1 = sayNameForAll.bind(person1);
sayNameForPerson1("person1"); // outputs "person1:Nicholas"

// create a function just for person2
var sayNameForPerson2 = sayNameForAll.bind(person2, "person2");
sayNameForPerson2(); // outputs "person2:Greg"

// attaching a method to an object doesn't change 'this'
person2.sayName = sayNameForPerson1;
person2.sayName("person2"); // outputs "person2:Nicholas"
```

---

## objecs

internal operators

`[[put]], [[get]], [[set]], [[delete]]`

---

### detecting properties

```js
// unreliable
if (person1.age) {
// do something with age
}
```

The `if` condition evaluates,

- to true if the value is **truthy** *(an object, a nonempty string, a nonzero number, or true)*
- to false if the value is **falsy** *(null, undefined, 0, false, NaN, or an empty string)*

--

#### `in` operator

```js
// reliable
var person1 = {
    name: "Nicholas",
    sayName: function() {console.log(this.name);}
};
console.log("name" in person1); // true
console.log("sayName" in person1); // true
console.log("title" in person1); // false
```

but `in` operator checks both own and prototype properties

--

#### `hasOwnProperty()`

```js
var person1 = {
    name: "Nicholas",
    sayName: function() {
        console.log(this.name);
    }
};
console.log("name" in person1); // true
console.log(person1.hasOwnProperty("name")); // true
console.log("toString" in person1); // true
console.log(person1.hasOwnProperty("toString")); // false
```

---

### removing properties

```js
var person1 = {
    name: "Nicholas"
};

delete person1.name;
console.log("name" in person1); // false
console.log(person1.name); // undefined
```

---

### enumeration

By default, all properties that you add to an object are enumerable, which means that you can iterate over them using a `for-in` loop.

--

#### `for-in` loop

```js
for (property in object) {
    console.log("Name: " + property );
    console.log("Value: " + object[property]);
}
```

--

#### `Object.keys()`

```js
var properties = Object.keys(object);
// if you want to mimic for-in behavior
var i, len;
for (i=0, len=properties.length; i < len; i++){
    console.log("Name: " + properties[i]);
    console.log("Value: " + object[properties[i]]);
}
```

- `Object.keys()` returns only own (instance) properties
- `for-in` loop also enumerates prototype properties

---

### type of properties

--

#### Data Properties

```js
var person1 = {};
Object.defineProperties(person1, {
    // data property to store data
    _name: {
        value: "Nicholas",
        enumerable: true,
        configurable: true,
        writable: true
    }
```

--

#### Accessor Properties

```js
    // accessor property
    name: {
        get: function() {
            console.log("Reading name");
            return this._name;
        },
        set: function(value) {
            console.log("Setting name to %s", value);
            this._name = value;
        },
        enumerable: true,
        configurable: true
    }
});
```

---

### retrieving property attributes

```js
var person1 = {
    name: "Nicholas"
};

var descriptor =
Object.getOwnPropertyDescriptor(person1, "name");

console.log(descriptor.enumerable); // true
console.log(descriptor.configurable); // true
console.log(descriptor.writable); // true
console.log(descriptor.value); // "Nicholas"
```

---

### preventing object modification

```js
// 1. prevent to add new properties
Object.preventExtensions(obj1);

// 1 & 2. set all [configurable] attribute to 'false'
Object.seal(obj1);

// 1, 2 & 3. can't change types and any data properties
Object.freeze(obj1);
```

always use strict mode. attempting to alter a non-extensible or sealed object will throw an `error` in `strict mode`. In non-strict mode, the operation fails silently.

--

#### `Object.preventExtensions()`

method makes an object non-extensible. Once used, never be able to add any new properties to the object again.

```js
var person1 = {
    name: "Nicholas"
};

console.log(Object.isExtensible(person1)); // true

Object.preventExtensions(person1);
console.log(Object.isExtensible(person1)); // false

person1.age = 80;
console.log("age" in person1); // false
```

--

#### `Object.seal()`

method on an object to seal it. [[Extensible]] and all properties [[Configurable]] attribute set to false.

```js
Object.seal(person1);
console.log(Object.isExtensible(person1)); // false
console.log(Object.isSealed(person1)); // true

person1.age = 80; console.log("age" in person1); // false

person1.name = "Greg";
console.log(person1.name); // "Greg"

var descriptor =
Object.getOwnPropertyDescriptor(person1, "name");
console.log(descriptor.configurable); // false
```

--

#### `Object.freeze()`

method make an object can’t change properties, properties’ types, and  write to any data properties

```js
Object.freeze(person1);
console.log(Object.isExtensible(person1)); // false
console.log(Object.isSealed(person1)); // true
console.log(Object.isFrozen(person1)); // true

person1.age = 80; console.log("age" in person1); // false
person1.name = "Greg";
console.log(person1.name); // "Nicholas"

var descriptor =
Object.getOwnPropertyDescriptor(person1, "name");
console.log(descriptor.configurable); // false
console.log(descriptor.writable); // false

```

---

## constructors & prototypes

---

