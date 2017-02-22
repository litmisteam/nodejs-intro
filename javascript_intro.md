# Step 5: Javascript, a quick intro

Node.js is a collection of Javascript APIs built on top of Google's V8 interpreter - the same Javascript engine that runs the Chrome web browser.  This effectively means Node.js _is_ Javascript and all Node.js programs are _written in_ Javascript.

Javascript has some phenomenal capabilities when it comes to running code concurrently.  With that said, I will not be teaching introductory Javascript\*\* and instead focus on areas that aren't as obvious to a person coming from a traditional IBM i background \(i.e. an RPG programmer, like me\).

\*\* You can learn intro to Javascript at [w3schools.com](http://www.w3schools.com/js/default.asp).

## Syntax

### Dynamic Types

Javascript has dynamic types.  This means a couple things.  First, you don't declare a datatype when you declare a variable.  Instead, a variable gets its data type when it is first assigned.  Not only that, but a Javascript variable can have its data type changed simply by placing a different value in it.  To test this concept paste the below code into a REPL session \(type node in the shell and press the Enter key\).

```js
var x

typeof x

x = 4

typeof x

x = "Harry"

typeof x

x = true

typeof x
```

The first line is declaring a variable of `x`.  Then the [`typeof`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/typeof) operator conveys the current data type of the variable.  The subsequent lines are all setting the variable to a different data type and then using typeof to display the change.

You should see results in your console similar to the following after pasting into the REPL.

```sh
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

Notice there aren't errors when assigning various different data types to the same variable?  The `x` variable has its data type changed when a new type of data is assigned to it.

**NOTE:** Semicolons are optional in Javascript, although there's a catch with that.  Depending on the Javascript runtime processing the code you may get different results.  It is for that reason most people include semicolons on all of their code even when they control the runtime \(which you can only really control the runtime on the server-side\).

