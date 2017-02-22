# Step 8: Functions

At a high level [Javascript functions](http://www.w3schools.com/js/js_function_definition.asp) are synonymous with RPG subprocedures.  Below is a function named func1 that receives in two parameters, adds them together, and returns the result.

```js
function func1(p1, p2) {
  return p1 + p2
}

var total = func1(2, 3)
console.log(total)
```

Paste *(Ctrl+Shift+V)* the above code into the REPL to see it run.  After func1 is declared we see it being invoked and display the total variable via console.log(...).  Exit the Node.js REPL by typing .exit

Start the Node.js REPL again and paste *(Ctrl+Shift+V) *the below code into it.  Notice the func1() function is being invoked *before* it is declared.

```js
var total = func1(2, 3)
console.log(total)

function func1(p1, p2) {
  return p1 + p2
}
```

You should end up with an error like the following that declares the function was not found.  This is because of how Javascript is parsed - top down - and a function must be defined before it can be used.

```
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

The above is one way to define a function, but there are many more.  Let's go back to the Express hello world program, shown below.

```js
app.get('/', function(req, res) {
  res.send('Hello World!')
})
```

Notice the second parameter on the call to apt.get(...).  This is an **inline anonymous function**, literally a chunk of code being passed as a parameter.  The function could also have been separately declared and then reference the name on the call to app.get(...), as shown below.

```js
function process_get(req, res) {
  res.send('Hello World!')
}

app.get('/', process_get)
```

What's the difference?  

For the most part they are functionally the same.  What's significant is the concept behind it.  When a request is made to the root of the website, the function specified on `app.get(...)` will be invoked, eventually.  What do I mean by "eventually"?  Well, first the code within `app.get(...)` will run a bunch of other code, including parsing the query string or reading in HTML form variables, *before* it invokes the function passed as the second parameter.  This is the "call back" concept, where a called function will "call back" into a function that was passed to it.  Many times the callback will have parameters defined on it to receive input, in this case the req and res variables.  RPG has a similar concept with [procedure pointers](http://www.ibm.com/developerworks/ibmi/library/i-rpg-pointers/).

Now it's time to take the hello world app to new heights by introducing a connection to DB2.
