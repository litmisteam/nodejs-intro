# Step 6: Modular Code

Node.js has a simple mechanism for modularizing code: [Modules](https://nodejs.org/api/modules.html).  To learn about modules, first create a file named funcs.js in the hello directory and occupy it with the below contents. 

```js
function func1(p1, p2){
  return p1 + p2
}

exports.func1 = func1
```

The first three lines in funcs.js declare a function named func1. Functions are similar to sub procedures in RPG.  The fourth line is exporting func1.  To accomplish the same in RPG we place the EXPORT keyword on the P-spec of a sub procedure definition.  Next create file funcstest.js so we can test our newly created module, as shown below.

```js 
var f = require('./funcs')
var result = f.func1(2, 3)
console.log('result:' + result)
```

Now go back to your shell and run funcstest.js, as shown below.

```sh
% node funcstest.js
result:5
```

Javascript functions have many more features but this at least gives you an idea of how the require() capabilities work.