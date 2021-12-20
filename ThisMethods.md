## `Function.prototype.call()`

The `call()` method calls a function with a given `this` value and arguments provided individually.

```js
function Product(name, price) {
  this.name = name;
  this.price = price;
}

function Food(name, price) {
  Product.call(this, name, price); //sets this of Product to the this of Food
  this.category = "food";
}

console.log(new Food("cheese", 5).name);
//"cheese"
```

## `Function.prototype.apply()`

The `apply()` method calls a function with a given `this` value, and `arguments` provided as an array (or an array-like object).

## `Function.prototype.bind()`

The `bind()` method creates a new function that, when called, has its `this` keyword set to the provided value, with a given sequence of arguments preceding any provided when the new function is called.

This mechanism is often called _"hard binding"_.
