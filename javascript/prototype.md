# Inheritance and the prototype chain

JavaScript is a bit confusing for developers experienced in class-based languages (like Java or C++), as it is dynamic and does not have static types.

When it comes to inheritance, JavaScript only has one construct: objects. Each object has a private property which holds a link to another object called its **prototype**. That prototype object has a prototype of its own, and so on until an object is reached with null as its prototype. **By definition, null has no prototype**, and acts as the final link in this prototype chain. It is possible to mutate any member of the prototype chain or even swap out the prototype at runtime, so concepts like static dispatching do not exist in JavaScript.

In JavaScript, objects can inherit features from one another via **prototypes**. Every object has its own property called prototype.

Because a prototype itself is also another object, the prototype has its own prototype. This creates a something called **prototype chain**. The prototype chain ends when a prototype has null for its own prototype.

When you access a property of an object, if the object has that property, it’ll return the property value. The following example accesses the name property of the person object:

    person.name

It returns the value of the name property as expected.

However, if you access a property that doesn’t exist in an object, the JavaScript engine will search in the prototype of the object.

If the JavaScript engine cannot find the property in the object’s prototype, it’ll search in the prototype’s prototype until either it finds the property or reaches the end of the prototype chain.

For example, you can call the toString() method of the `person` object like this:

    person.toString();

The `toString()` method returns the string representation of the `person` object. By default, it’s `[object Object]` which is not obvious.

    Note that when a function is a value of an object’s property, it’s called a method. Therefore, a method is a property with value as a function.

**In conclusion, when you define a method on the prototype object, this method is shared by all instances.**
