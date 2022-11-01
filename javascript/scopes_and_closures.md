# Lexical scoping

Consider the following example code:

    function init() {
        var name = 'Mozilla'; // name is a local variable created by init
        function displayName() {
            // displayName() is the inner function, a closure
            console.log(name); // use variable declared in the parent function
        }
        displayName();
    }
    init();

`init()` creates a local variable called name and a function called `displayName()`. The `displayName()` function is an inner function that is defined inside `init()` and is available only within the body of the init() function. Note that the `displayName()` function has no local variables of its own. However, since inner functions have access to the variables of outer functions, `displayName()` can access the variable name declared in the parent function, `init()`.

This is an example of lexical scoping, which describes how a parser resolves variable names when functions are nested. The word lexical refers to the fact that lexical scoping uses the location where a variable is declared within the source code to determine where that variable is available. Nested functions have access to variables declared in their outer scope.

In this particular example, the scope is called a function scope, because the variable is accessible and only accessible within the function body where it's declared.

# Scoping with let and const

Traditionally (before ES6), JavaScript only had two kinds of scopes: **function scope** and **global scope**. Variables declared with var are either function-scoped or global-scoped, depending on whether they are declared within a function or outside a function. This can be tricky, because blocks with curly braces do not create scopes:

    if (Math.random() > 0.5) {
    	var x = 1;
    } else {
    	var x = 2;
    }
    console.log(x);

For people from other languages (e.g. C, Java) where blocks create scopes, the above code should throw an error on the console.log line, because we are outside the scope of x in either block. However, because blocks don't create scopes for var, the var statements here actually create a global variable.

In ES6, JavaScript introduced the let and const declarations, which, among other things like temporal dead zones, allow you to create block-scoped variables.

    if (Math.random() > 0.5) {
    	const x = 1;
    } else {
    	const x = 2;
    }
    console.log(x);
    // ReferenceError: x is not defined

In essence, blocks are finally treated as scopes in ES6, but only if you declare variables with let or const. In addition, ES6 introduced modules, which introduced another kind of scope. Closures are able to capture variables in all these scopes, which we will introduce later.

# Closure

Consider the following code example:

    function makeFunc() {
        const name = 'Mozilla';
        function displayName() {
            console.log(name);
        }
        return displayName;
    }

    const myFunc = makeFunc();
    myFunc();

Running this code has exactly the same effect as the previous example of the `init()` function above. What's different (and interesting) is that the `displayName()` inner function is returned from the outer function before being executed.

At first glance, it might seem unintuitive that this code still works. In some programming languages, the local variables within a function exist for just the duration of that function's execution. Once `makeFunc()` finishes executing, you might expect that the name variable would no longer be accessible. However, because the code still works as expected, this is obviously not the case in JavaScript.

The reason is that functions in JavaScript form closures. **A closure is the combination of a function and the lexical environment within which that function was declared**. This environment consists of any local variables that were in-scope at the time the closure was created. In this case, myFunc is a reference to the instance of the function `displayName` that is created when `makeFunc` is run. The instance of `displayName` maintains a reference to its lexical environment, within which the variable name exists. For this reason, when `myFunc` is invoked, the variable name remains available for use, and "Mozilla" is passed to console.log.

Here's a slightly more interesting example — a makeAdder function:

    function makeAdder(x) {
        return function (y) {
            return x + y;
        };
    }

    const add5 = makeAdder(5);
    const add10 = makeAdder(10);

    console.log(add5(2)); // 7
    console.log(add10(2)); // 12

In this example, we have defined a function `makeAdder(x)`, that takes a single argument `x`, and returns a new function. The function it returns takes a single argument `y`, and returns the sum of `x` and `y`.

In essence, `makeAdder` is a **function factory**. It creates functions that can add a specific value to their argument. In the above example, the function factory creates two new functions — one that adds five to its argument, and one that adds 10.

`add5` and `add10` are both closures. They share the same function body definition, but store different lexical environments. In `add5`'s lexical environment, `x` is 5, while in the lexical environment for `add10`, `x` is 10.

# Emulating private methods with closures

Languages such as Java allow you to declare methods as private, meaning that they can be called only by other methods in the same class.

JavaScript, prior to classes, didn't have a native way of declaring private methods, but it was possible to emulate private methods using closures. Private methods aren't just useful for restricting access to code. They also provide a powerful way of managing your global namespace.

The following code illustrates how to use closures to define public functions that can access private functions and variables. Note that these closures follow the Module Design Pattern.

    const counter = (function () {
        let privateCounter = 0;
        function changeBy(val) {
            privateCounter += val;
        }

        return {
            increment() {
                changeBy(1);
            },

            decrement() {
                changeBy(-1);
            },

            value() {
                return privateCounter;
            },
        };
    })();

    console.log(counter.value()); // 0.

    counter.increment();
    counter.increment();
    console.log(counter.value()); // 2.

    counter.decrement();
    console.log(counter.value()); // 1.

In previous examples, each closure had its own lexical environment. Here though, there is a single lexical environment that is shared by the three functions: counter.increment, counter.decrement, and counter.value.

The shared lexical environment is created in the body of an anonymous function, which is executed as soon as it has been defined (also known as an IIFE). The lexical environment contains two private items: a variable called privateCounter, and a function called changeBy. You can't access either of these private members from outside the anonymous function. Instead, you can access them using the three public functions that are returned from the anonymous wrapper.

Those three public functions are closures that share the same lexical environment. Thanks to JavaScript's lexical scoping, they each have access to the privateCounter variable and the changeBy function.

    const makeCounter = function () {
        let privateCounter = 0;
        function changeBy(val) {
            privateCounter += val;
        }
        return {
            increment() {
                changeBy(1);
            },

            decrement() {
                changeBy(-1);
            },

            value() {
                return privateCounter;
            },
        };
    };

    const counter1 = makeCounter();
    const counter2 = makeCounter();

    console.log(counter1.value()); // 0.

    counter1.increment();
    counter1.increment();
    console.log(counter1.value()); // 2.

    counter1.decrement();
    console.log(counter1.value()); // 1.
    console.log(counter2.value()); // 0.

Notice how the two counters maintain their independence from one another. Each closure references a different version of the privateCounter variable through its own closure. Each time one of the counters is called, its lexical environment changes by changing the value of this variable. Changes to the variable value in one closure don't affect the value in the other closure.
