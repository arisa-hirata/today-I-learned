# Apply vs. Call vs. Bind

`apply`, `call`, and `bind` allows you to change the value of `this` for a given function.

### Function.prototype.call()

The methos `Call` invokes the function and allows you to pass in arguments one by one using commas.

```javascript
let customer1 = { name: 'Jack', email: 'jack@gmail.com' };
let customer2 = { name: 'Mary', email: 'mary@hotmail.com' };

function greeting(text) {
  console.log(`${text} ${this.name}`);
}

greeting.call(customer1, 'Hello'); // Hello Jack
greeting.call(customer2, 'Hello'); // Hello Mary
```

### Function.prototype.apply()

The method `Apply` invokes the function and allows you to pass in arguments as an array.

```javascript
let customer1 = { name: 'Jack', email: 'jack@gmail.com' };
let customer2 = { name: 'Mary', email: 'mary@hotmail.com' };

function greeting(text, text2) {
  console.log(`${text} ${this.name}, ${text2}`);
}

greeting.apply(customer1, ['Hello', 'How are you?']);
// Hello Jack, How are you?
greeting.apply(customer2, ['Hello', 'How are you?']);
// Hello Mary, How are you?
```

### Function.prototype.bind()

The `Bind` method returns a new function, allowing you to pass in this array and any number of arguments. Use it when you want that function to later be called with a certain context like events.

```javascript
let customer1 = { name: 'Jack', email: 'jack@gmail.com' };
let customer2 = { name: 'Mary', email: 'mary@hotmail.com' };

function greeting(text) {
  console.log(`${text} ${this.name}`);

  let helloJack = greeting.bind(customer1);
  let helloMary = greeting.bind(customer2);

  helloJack('Hello'); // Hello Jack
  helloMary('Hello'); // Hello Mary
}
```

The `Bind` implementation would be like this:

```javascript
Function.prototype.bond = function(context) {
  var fn = this;
  return function() {
    fn.apply(context, arguments);
  };
};
```

`Call` and `Apply` are interchangeble. You can decide whether it's easier to send in an array or comma separated list of arguments. `Bind` is different. It always returns a new function.

We can use `Bind` to curry functions like in the example. We can take a simple hello function and turn it into helloJhon or helloKelly. You can use it for events where we don't know when they'll be fired but know what context is.

### References

- [.call()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/call?source=post_page-----d738a9e8b4e1----------------------)
- [.apply()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/apply?source=post_page-----d738a9e8b4e1----------------------)
- [.bind()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_objects/Function/bind?source=post_page-----d738a9e8b4e1----------------------)
