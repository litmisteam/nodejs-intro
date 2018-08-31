# Step 4: Javascript, A Quick Intro

Node.js is a collection of Javascript APIs built on top of Google's V8 interpreter - the same Javascript engine that runs the Chrome web browser. This effectively means Node.js _is_ Javascript and all Node.js programs are _written in_ Javascript.

Javascript has some phenomenal capabilities when it comes to running code concurrently. With that said, I will not be teaching introductory Javascript\*\* and instead focus on areas that aren't as obvious to a person coming from a traditional IBM i background \(i.e. an RPG programmer, like me\).

\*\* You can learn intro to Javascript at [w3schools.com](http://www.w3schools.com/js/default.asp).

## Syntax

### Dynamic Types

Javascript has dynamic types. This means a couple things. First, you don't declare a datatype when you declare a variable. Instead, a variable gets its data type when it is first assigned. Not only that, but a Javascript variable can have its data type changed simply by placing a different value in it. To test this concept paste the below code into a REPL session \(type `node` in the shell and press the `Enter` key to start a REPL session\).

```javascript
var x
typeof x
x = 4
typeof x
x = "Harry"
typeof x
x = true
typeof x
```

The first line is declaring a variable of `x`. Then the [`typeof`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/typeof) operator conveys the current data type of the variable. The subsequent lines are all setting the variable to a different data type and then using typeof to display the change.

You should see results in your console similar to the following after pasting into the REPL.

**NOTE:** The below is output, not something you should copy and paste into the Node.js REPL sesison.

```bash
% node
> var x
undefined
> typeof x
'undefined'
> x = 4
4
> typeof x
'number'
> x = "Harry"
'Harry'
> typeof x
'string'
> x = true
true
> typeof x
'boolean'
```

Notice there aren't errors when assigning various different data types to the same variable? The `x` variable has its data type changed when a new type of data is assigned to it.

**NOTE:** Semicolons are optional in Javascript, although there's a catch with that. Depending on the Javascript runtime processing the code you may get different results. It is for that reason most people include semicolons on all of their code even when they control the runtime \(which you can only really control the runtime on the server-side\).

## Modular Code

Node.js has a simple mechanism for modularizing code: [Modules](https://nodejs.org/api/modules.html). To learn about modules, first create a file named `funcs.js` in the `hello` directory and occupy it with the below contents.

```javascript
function func1(p1, p2){
  return p1 + p2
}

exports.func1 = func1
```

The first three lines in `funcs.js` declare a function named `func1`. Functions are similar to sub procedures in RPG. The fourth line is exporting `func1`. To accomplish the same in RPG we place the `EXPORT` keyword on the P-spec of a sub procedure definition. Next create file `funcstest.js` so we can test our newly created module, as shown below.

```javascript
var f = require('./funcs')
var result = f.func1(2, 3)
console.log('result:' + result)
```

Now go back to your shell and run `funcstest.js`, as shown below.

```bash
% node funcstest.js
result:5
```

Javascript functions have many more features but this at least gives you an idea of how the `require()` capabilities work.

## Functions

At a high level, [Javascript functions](http://www.w3schools.com/js/js_function_definition.asp) are synonymous with RPG sub procedures. Below is a function named `func1` that receives in two parameters, adds them together, and returns the result.

```javascript
function func1(p1, p2) {
  return p1 + p2
}

var total = func1(2, 3)
console.log(total)
```

Paste \(`Ctrl+Shift+V`\) the above code into the REPL to see it run. After `func1` is declared we see it being invoked and display the total variable via `console.log(...)`. Exit the Node.js REPL by typing `.exit`

Start the Node.js REPL again and paste \(`Ctrl+Shift+V`\) the below code into it. Notice the `func1()` function is being invoked _**before**_ it is declared.

```javascript
var total = func1(2, 3)
console.log(total)

function func1(p1, p2) {
  return p1 + p2
}
```

You should end up with an error like the following that declares the function was not found. This is because of how Javascript is parsed - top down - and a function must be defined before it can be used.

```text
ReferenceError: func1 is not defined
    at repl:1:13
    at REPLServer.defaultEval (repl.js:132:27)
    at bound (domain.js:284:14)
    at REPLServer.runBound [as eval] (domain.js:297:12)
    at REPLServer.<anonymous> (repl.js:279:12)
    at REPLServer.emit (events.js:107:17)
    at REPLServer.Interface._onLine (readline.js:214:10)
    at REPLServer.Interface._line (readline.js:553:8)
    at REPLServer.Interface._ttyWrite (readline.js:830:14)
    at ReadStream.onkeypress (readline.js:109:10)
```

The above is one way to define a function, but there are many more. Let's go back to the hello world program, shown below.

```javascript
http.createServer(function(req, res) {
  res.writeHead(200, {'Content-Type': 'text/plain'})
  res.end('Hello World')
}).listen(port, '0.0.0.0')
```

Notice the parameter on the call to `http.createServer(...)`. This is an **inline anonymous function**, literally a chunk of code being passed as a parameter. The function could also have been separately declared and then reference the name on the call to `http.createServer(...)`, as shown below.

```javascript
function process_get(req, res) {
  res.writeHead(200, {'Content-Type': 'text/plain'})
  res.end('Hello World')
}

http.createServer(process_get).listen(port, '0.0.0.0')
```

What's the difference?

For the most part they are functionally the same. What's significant is the concept behind it. When a request is made to the root of the website, the function specified on `http.createServer(...)` will be invoked, **eventually**. What do I mean by "eventually"? Well, first the code within `http.createServer(...)` will run a bunch of other code, including parsing the query string or reading in HTML form variables, _before_ it invokes the function passed as the second parameter. This is the "call back" concept, where a called function will "call back" into a function that was passed to it. Many times the callback will have parameters defined to receive input, in this case the `req` and `res` variables. RPG has a similar concept with [procedure pointers](http://www.ibm.com/developerworks/ibmi/library/i-rpg-pointers/).

### Proceed to [Step 5: REPL Intro](step-5-npm-the-package-manager.md)