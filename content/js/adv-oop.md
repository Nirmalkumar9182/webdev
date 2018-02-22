# Object-Oriented Programming in JavaScript

## The Prototype

### Inheritance in JavaScript

  * JavaScript doesn't use classes, it uses prototypes

  * There are ways to simulate classes (even ES6 does it!)

  * The prototypal model:
      - Tends to be smaller
      - Less redundant
      - Can simulate classical inheritance as needed
      - More powerful

### Object Inheritance

![Inheriting Properties](../../diagrams/js/inheritance.dot)

### Object Inheritance

![Setting a Property](../../diagrams/js/inheritance-set.dot)

### Prototype Refresher

  * All objects have an internal link to another object called its
    *prototype* (known internally as the `__proto__` property).

  * The prototype object also has a prototype, and so on up the
    *prototype chain* (the final link in the chain is `null`).

  * Objects *delegate* properties to other objects through the
    prototype chain.

  * Only functions have a `prototype` property by default.

### Inheritance with `__proto__`

![Prototypes](../../diagrams/js/proto-simple.dot)

### Looking at `Array` Instances

![Array and Array.prototype](../../diagrams/js/array-proto.dot)

### The Prototype Chain

![Prototypal Inheritance](../../diagrams/js/proto.dot)

### Another Look at `Array` Instances

![Array and Friends](../../diagrams/js/full-array-proto.dot)

## Establishing the Prototype Chain

### Using `Object.create`

The `Object.create` function creates a new object and sets its
`__proto__` property:

~~~ {.javascript insert="../../src/examples/js/objcreate.js" token="create"}
~~~

### Using the `new` Operator

The `new` operator creates a new object and sets its `__proto__`
property.  The `new` operator takes a function as its right operand
and sets the new object's `__proto__` to the function's `prototype`
property.

~~~ {.javascript insert="../../src/examples/js/objnew.js"}
~~~

### Constructor Functions and OOP

~~~ {.javascript insert="../../src/examples/js/inheritance.js" token="rec"}
~~~

### Constructor Functions and Inheritance

~~~ {.javascript insert="../../src/examples/js/inheritance.js" token="sq"}
~~~

### Using `__proto__` in ES6

Starting in ECMAScript Edition 6, the `__proto__` property is
standardized as an accessible property.

*Warning:* Using `__proto__` directly is strongly discouraged due to
performance concerns.

### Exercise: Prototype Walking

  #. Open the debugging console

  #. Create a string and assign it to a variable

  #. Follow the `__proto__` links until you reach the root of the
     tree.

## Parasitic Inheritance

### Constructors that Aren't

Parasitic inheritance is created by:

  * Constructor or factory functions

  * They don't create their own objects

  * After having another function create an object they augment it in
    some way.

### An Example Using the `new` Operator

~~~ {.javascript insert="../../src/examples/js/parasitic.js" token="new"}
~~~
## Multiple Inheritance via Mixins

### What is a Mixin?

  * Simulates multiple inheritance

  * Properties from interesting objects are copied into the target
    object, making the target object appear to be made up of the
    interesting objects.

  * All the same problems you get with real multiple inheritance, but
    without any of the built-in solutions to resolve them.

### Using the Mixin Technique

~~~ {.javascript insert="../../src/examples/js/mixin.js" token="usage"}
~~~

### Writing the Mixin Machinery

~~~ {.javascript insert="../../src/examples/js/mixin.js" token="mixin"}
~~~

## Introspection and Reflection

### Simple Introspection Techniques


  * The `instanceof` Operator:

    <div class="notes">

    Returns `true` if the left operand was constructed with the
    function given as the right operand.

    </div>

    ~~~ {.javascript}
    // Returns `true':
    [1, 2, 3] instanceof Array;
    ~~~

  * The `isPrototypeOf` Function:

    <div class="notes">

    Returns `true` if the receiver is in the prototype (inheritance)
    chain of the argument.  In other words, returns `true` if the
    receiver is an ancestor of the argument.

    </div>

    ~~~ {.javascript}
    // Returns `true':
    Object.prototype.isPrototypeOf([1, 2, 3]);

    // Returns `false':
    String.prototype.isPrototypeOf([1, 2, 3]);
    ~~~

  * The `Object.getPrototypeOf` Function:

    <div class="notes">

    Returns the prototype (i.e. the `__proto__` property) of the
    argument.

    </div>

    ~~~ {.javascript}
    // Returns `Array.prototype':
    Object.getPrototypeOf([1, 2, 3]);
    ~~~

## Object Immutability

### `Object.freeze`

~~~ {.javascript}
Object.freeze(obj);

assert(Object.isFrozen(obj) === true);
~~~

  * Can't add new properties

  * Can't change values of existing properties

  * Can't delete properties

  * Can't change property descriptors

<div class="notes">
[More information](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/freeze)
</div>

### `Object.seal`

~~~ {.javascript}
Object.seal(obj);

assert(Object.isSealed(obj) === true);
~~~

  * Properties can't be deleted, added, or configured

  * Property values can still be changed

<div class="notes">
[More information](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/seal).
</div>

### `Object.preventExtensions`

~~~ {.javascript}
Object.preventExtensions(obj);
~~~

  * Prevent any new properties from being added

<div class="notes">
[More information](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/preventExtensions)
</div>

### `Object.defineProperty`

~~~ {.javascript}
Object.defineProperty(obj, propName, definition);
~~~

  * Define (or update) a property and its configuration

  * Some things that can be configured:
    - `enumerable`: If the property is enumerated in `for .. in` loops (Boolean)
    - `value`: The property's value
    - `writable`: If the value can change (Boolean)

<div class="notes">

[More information](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/defineProperty)

</div>