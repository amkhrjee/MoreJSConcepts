# Objects and Primitive Types 

Objects are passed by memory reference to function params whereas Primitive values are passed by value. 

```js
let num = 1; 
let obj ={a :1}

function addTwo(num, obj){
    num = num +2;
    console.log(num)
    obj.a = 5;
    console.log(obj.a)
}
addTwo(num, obj) // num -> 3 &  obj.a -> 5
console.log(num) //1 num in the global scope remains unchanged
console.log(obj.a) //5 the obj actually changes
```

## But if primitives are not objects, how do we dot into them and use methods? 

Well, it's the prototype object bound to the primitive type that gives us access to all these in-built method. When 
dotting into a primitive type, JS wraps the primitive into an object.

This is called **Autoboxing**, where we treat primitive types like an object. 

## Autoboxing ([taken from SO](https://stackoverflow.com/a/17217024/12404524))
Wikipedia puts it this way: 
> Autoboxing is the term for getting a reference type out of a value type just through type conversion (either implicit or explicit). The compiler automatically supplies the extra source code that creates the object.

### Difference between Value Type and Reference Type

| Value Type                                                                                                   | Reference Type                                                                                                           |
|--------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------|
| Data stored in **stack** memory                                                                              | Data stored in **heap** memory                                                                                           |
| When passed as value type new copy is created and passed so changes to variable does not get reflected back. | When passed as Reference type then reference of that variable is passed so changes to variables does get reflected back. |
| Value types are faster in access                                                                             | Reference types are slower in access                                                                                     |
### Passing Reference Type Variables ([read this](https://www.tutorialsteacher.com/csharp/csharp-value-type-and-reference-type))
When you pass a reference type variable from one method to another, it doesn't create a new copy; instead, it passes the variable's address. So, If we change the value of a variable in a method, it will also be reflected in the calling method.

### Stack Overflow answer to question - [Does javascript autobox?](https://stackoverflow.com/questions/17216847/does-javascript-autobox)

First of all I assume you are talking about automatic conversion of primitive values to objects. This happens in two cases in JavaScript:

1. When you pass a primitive value as the `this` value to `.call` or `.apply` (not in strict mode though).
2. When you are trying to access a "property" of a primitive value, e.g. `"foo bar".split()`. (⭐This is our main 
   concern here.)

### 1. Primitive value as `this`
When a function is executed and its `this` value is not an object, it is converted to one, at least in non-strict 
mode. This described in [§10.4.3 Entering Function Code<sup>_[spec]_</sup> ](http://es5.github.io/#x10.4.3) in the ECMAScript 5.1 documentation:

> #### 10.4.3 Entering Function Code 
> The following steps are performed when control enters the execution context for function code contained in function object `F`, a caller provided `thisArg`, and a caller provided ``argumentsList``:
>1. If the function code is strict code, set the `ThisBinding` to `thisArg`. 
>2. Else if `thisArg` is `null` or `undefined`, set `ThisBidning` to the global object. 
>3. Else if `Type(thisArg)` is not `Object`, set the `ThisBinding` to `ToObject(thisArg)`
>4. Else set the `ThisBinding` to `thisArg`.
>5. Let `localEnv` be the result of calling `NewDeclarativeEnvironment` passing the value of the `[[Scope]]` 
    > internal property of `F` as the argument.
>6. Set the `LexicalEnvironment` to `localEnv`.
>7. Set the `VariableEnvironment` to `localEnv`.
>8. Let code be the value of `F`’s `[[Code]]` internal property.
>9. Perform Declaration Binding Instantiation using the function code `code` and `argumentList` as described in [10.
    > 5](http://es5.github.io/#x10.5).

As you can see in step three the value is converted to an object by calling `ToObject`.

### 2. Property Access 
Something similar happens when you are trying to access properties ([§11.2.1 Property Accessors <sup>_[spec]_</sup>]
(http://es5.github.io/#x11.2.1)). The quoted part here explains how the expression `foo[bar]` is evaluated, i.e. how property access with the bracket notation is evaluated. The part we are interested in applies to dot notation as well.

> The production `MemberExpression: MemberExpression[Expression]` is evaluated as follows: 
>- Let `baseReference` be the result of evaluating `MemberExpression`. 
>- Let `baseValue` be `GetValue(baseReference)`. 
>- [...]
>- Return a value of type `Reference` whose `base` value is `baseValue` and whose referenced name is 
   `propertyNameString`, and whose `strict` mode flag is `strict`. 

The important step is teh lsat one: No matter what `MemberExpression` evaluates, it is converted to a value of type 
   `Reference`. This is a datatype only used in the specification and contains additional information about how 
   the actual value should be received from the reference(not to be confused with object references in actual JS 
   code!)







 
