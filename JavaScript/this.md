# About "This" Keyword

Four different binding of `this` keyword and about "new" keyword.

### What is "this" keyword in JavaScript

<b>`this` keyword referes to an object, that object which is executing the current bit of JavaScript code.</b>

In other words, every JavaScript function while excecuting has a reference to its current excecution context, called `this`. Excecution context means here is how the function is called.

To understand `this` keyword, we need to know how, when and from where the function is called. does not matter how and where function is declared or defined.

```javascript
function car() {
  console.log(this.name);
}

var name = 'Ninja';
var obj1 = { name: 'TOYOTA', car: car };
var obj2 = { name: 'NISSAN', car: car };

car(); // "Ninja"
obj1.car(); // "TOYOTA"
obj2.car(); // "NISSAN"
```

In the above code snippet, the job of `car()` function is printing the `this.name` which means it's trying to print the value of `name` property of the current excecution context(i.e. `this` object).

In the above code, when function `car()` gets called it prints `"Ninja"` because the context of excecution is not specofied so by default its global context and there is a variable `name` is present at global context whose value is `"Ninja"`.

In case of `obj1().car()` call, `"TOYOTA"` gets printed and the reason behind this is function `car()` gets called with the ececution context as `obj1` so `this.name` became `obj1.name`. Same with `obj2.bike()` call where the excecution context of function `car()` is `obj2`.

#### Default and Implicit binding of "this"

- If we are in _strict_ mode then the default value of `this` keyword is `undefined` otherwise `this` keyword act as <b>global object</b>, it's called default binding of `this` keyword. (default is window object in case of browser).

- When there is an object property which we are calling as a method then that object becomes `this` object or execution context object for that method, it is implicit binding of `this` keyword.

```javascript
var obj1 = {
  name: 'TOYOTA',
  car: function() {
    console.log(this.name);
  }
};
var obj2 = { name: 'NISSAN', car: obj1.car };
var name = 'Ninja';
var car = obj1.car;

car(); // "Ninja"
obj1.car(); // "TOYOTA"
obj2.car(); // "NISSAN"
```

In the above code, function call `car()` is an example of default binding. `obj1.car()` and `obj2.car()` are examples of implicit binding. Here `car` function is declared as part of `obj1` but regardless of that when we execute `obj2.bike()`, the context of execution is `obj2` so `obj2.name` gets printed.

It's important to know how, when and from where the function is called. does not matter where function is declared.

#### Explicit and Fixed Binding of "this" keyword

If we use `call` and `apply` method with calling function, both of those methods take as their first parameter as execution context. That is `this` binding.

```javascript
function car() {
  console.log(this.name);
}

var name = 'Ninja';
var obj = { name: 'TOYOTA' };

car(); // "Ninja"
car.call(obj); // "TOYOTA"
```

In this above snippet, if we call the function `car` with `call()` method passing execution context object `obj` as first argument, then `obj` gets assigned to `this` object and it prints `“TOYOTA”` which is nothing but `obj.name`. It’s called explicit binding of `this` keyword.

In Fixed binding or Hard binding, we can force the `this` object to be same always no matter from where and how it gets called.

```javascript
var car = function() {
  console.log(this.name);
};
var name = 'Ninja';
var obj1 = { name: 'TOYOTA' };
var obj2 = { name: 'NISSAN' };

var originalCarFun = car;
bike = function() {
  originalCarFun.call(obj1);
};

bike(); // "TOYOTA"
bike.call(obj2); // "TOYOTA"
```

As per above code, `car()` and `car.call(obj2)` both call prints `"TOYOTA"` which is nothing but `obj1.name` means the execution context of the function `car` is always obj1 and its because of `originalCarFun.call(obj1);` These kind of this binding is just another flavor of explicit binding called fixed binding.

### The “new” keyword in JavaScript

The _new_ keyword in front of any function turns the function call into constructor call and below things occurred when new keyword put in front of function

- A brand new empty object gets created
- new empty object gets linked to prototype property of that function
- same new empty object gets bound as this keyword for execution context of that function call
- if that function does not return anything then it implicit returns _this_ object.

```javascript
function car() {
  var name = 'Prius';
  this.maker = 'TOYOTA';
  console.log(this.name + ' ' + maker); // undefined NISSAN
}

var name = 'March';
var maker = 'NISSAN';

obj = new car();
console.log(obj.maker); // "TOYOTA"
```

In the above code, `car` function is get called with `new` keyword in front of it. So, it creates a new object then that new object gets linked to prototype chain of function `car`, after that the created new object bound to `this` object and function returns `this` object. That’s how the returned `this` object assigned to `obj` and `console.log(obj.maker)` prints `“TOYOTA”` .
In the above code, `this.name` inside function `car()` does not print `“Prius”` or `“March”` instead it prints `undefined` because the `name` variable declared inside the function `car()` and `this.name` are totally 2 different things. Same way `this.maker` and `maker` are different inside function `car()`.

#### Precedence of “this” keyword bindings

- First it checks whether the function is called with _new_ keyword.
- Second it checks whether the function is called with call or apply method means explicit binding.
- Third it checks if the function called via context object (implicit binding).
- Default global object (undefined in case of strict mode).
