# Javascript Understanding the Weird Parts Notes

## 7. CONCEPTUAL ASIDE: SYNTAX PARSERS, EXECUTION CONTEXT AND LEXICAL ENVIRONMENTS

### 7.1 SYNTAX PARSER
A program that reads your code and determines what it does and if its grammar is valid.

### 7.2 Lexical Environment
Where Something physically in the code you write.
Every Lexical Environment consists of:

Environment Record → Stores all variables and functions declared in the current scope.
Reference to the Outer Lexical Environment → A link to the surrounding (parent) scope.

*Example 1:*

```js
function outer() {
  let a = 10;

  function inner() {
    let b = 20;
    console.log(a); // 10 (accesses 'a' from outer scope)
  }
  inner();
}

outer();
```

**Explanation:**

outer() creates a Lexical Environment that stores a = 10.
Inside outer(), inner() is defined. It remembers the outer environment.

When inner() runs, it:
1 - Looks for a inside its own scope (not found).
2 - Goes to the outer lexical environment (finds a = 10).
JavaScript resolves variables by climbing up the lexical scope chain.


*Example 2: Closures & Lexical Environment*

```js
function counter() {
  let count = 0;

  return function () {
    count++;
    console.log(count);
  };
}

const increment = counter();
increment(); // 1
increment(); // 2
increment(); // 3

```

**How Lexical Environment Works Here:**
counter() runs, creating a Lexical Environment where count = 0.
It returns an inner function that remembers this environment.
Even after counter() finishes, the inner function retains access to count (closure).
Calling increment() modifies the preserved count variable.



### 7.3 Execution Context
A Wrapper to help manage the code that is running.
There are a lot of lexical environments, Which one is currently running is managed via execution contexts. It can contain things beyond what you've written in the code.

## 8. Conceptual Aside: Name/Value Pairs and Objects
A Name which maps to a unique value.
The name may be defined more than once, but only can have one value in any given context. That value may be more name/value pairs.

**Example**
```js
Adress = '100 Main St,'
```
An **Object** is a colection of name/value pairs.


## 10. The Global Environment and The Global Object:
The execution context is created when you run javascript. This can be checked by running `this` on the console. This is the global object inside the browser.

In the case of the browsers is the `window` object.

**GLOBAL** - Not inside a function basically.
**Outter Environment** If you're running code inside a function, it's the code that is in the outside layer.

![Code Context](Images/image.png)



## 11. The Execution Context - Creation and Hoisting

**Hoisting** 

```js
var a = 'Hello World'

function b() {
  console.log('Called b');
}

b();
console.log(a);

// this will print
// Called b
// Hello world
```

```js
b();
console.log(a)

var a = 'Hello World'

function b() {
  console.log('Called b');
}


// this will print
// Hello world
// undefined

```

Hoisting will see that the variable is declared and create "space" for it, but will not have the declared variables that comes bellow - the `Hello World`.

If we remove the `var a = 'Hello World'` line, it will trigger an uncaught error because the variable is not declared.

### How the execution context is created (CREATION PHASE)

![alt text](Images/hoisting.png.png)





