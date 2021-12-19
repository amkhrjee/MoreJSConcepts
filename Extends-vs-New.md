## The `extends` keyword

JS uses the prototype chain to implement classification.

```js
class Rectangle {}

class Square extends Rectangle {}

console.log(Object.getPrototypeOf(Square)) //Rectangle
```
The `extends` keyword just sets the prototype of a class object to the other class object. 

De-sugaring this code with objects would look like this: 
```js
function Rectangle() {}

function Square() {}

Object.setPrototypeOf(Square, Rectangle);

console.log(Object.getPrototypeOf(Square)) //Rectangle
```