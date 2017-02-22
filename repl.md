# Step 4: REPL Intro

Included with Node.js is the [REPL tool](https://nodejs.org/api/repl.html).  REPL stands for **R**ead, **E**val, **P**rint, and **L**oop and is a way to interactively run Javascript and see the results immediately.  I use the Node.js REPL on a regular basis to test small snippets of code.

To start a REPL you invoke the node command without any parameters, as shown below.  If your web application is still running from the previous hello world example, end it with Ctrl+C.

![image alt text](image_11.png)

Once inside a REPL you can enter other Node.js (and Javascript) statements.  Shown above we use console.log(...) to write a message to the terminal.  The red arrows signify being in the PASE shell.  Green arrows signify being in the Node REPL.  Use .exit to return to the PASE shell.

Taking that example further, you can actually paste *(Ctrl+Shift+V) *the entire contents of the hello/app.js program into a Node.js REPL and it will execute all the code and run your web app, as shown below.

![image alt text](image_12.png)

Now if you bring up your browser again you can see the same results as if you had run node app.js from the shell.  To end this Node.js REPL session select Ctrl+C twice.

There will be more examples of how to use the Node.js REPL later on.