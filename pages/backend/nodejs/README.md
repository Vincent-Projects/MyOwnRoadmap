# NodeJS

This is the place of my knowledge about NodeJS. The first thing to understand is that NodeJS is a Javascript runtime environement which means that it allows use to run Javascript outside the browser, that is why it uses the chrome Javascript engine, named V8.

An important tool that comes with the installation of NodeJS is npm, its package manager. It allows us to manage which node package will be install on our machine, or inside a project. The difference is that package installed on our machine ( say globally ) can be used and executed anywhere on the computer. Instead, packages that are installed inside a project can only be used inside that project, that is why a folder named "node_modules" is created when we install package for that project.

NodeJS comes with multiple useful [core modules](https://nodejs.org/docs/latest-v13.x/api/) such as `http`, `fs`, `path` and `crypto`. Those don't need to be installed and can be used ( imported ) directly inside a project.

Here is a simple exemple of use of `http` module to create a very simple server. 

```javascript
const http = require('http'); // Here we import http module ( no need to install )

// The http object has a method called createServer which return a server configured with the passed function. Here we used ES6 syntax but in the end it takes a function
const server = http.createServer((req, res) => {
  // No need to explain those lignes
  res.statusCode = 200;
  res.setHeader('Content-Type', 'text/html');
  res.end('<h1>Hello World!</h1>');
});

server.listen(3000); // Here we 'activate' the server asking to listen of the specific port ( reminder : http://<IP / DOMAIN>:<PORT> => http://127.0.0.1:3000 or http://localhost:3000 );
```

To run this script ( let say index.js ), we need to run the command `$ node index.js`. 

As i said NodeJS is a runtime environement that is able to run Javascript code outside the browser and i'll prove it to you with the following. 

```javascript
let name = "Vincent";

console.log(`My name is ${name}`);
```

This is simple Javascript. If you put this code in a file named `file.js` and run `$ node file.js`, what will it output to you ?

> Precision : This is important to understand Javascript language and understand the separation between the Javascript programming language and features and API added on the browser.

```javascript
let paragraph = document.createElement('p');
paragraph.textContent = "Hello World!";
console.log(paragraph.textContent);
```

This code for exemple won't work, because document is an object avaible on browser that represent the page.

## Prerequisites

As the NodeJS documentation suggest, there are some prerequisites before jumping into the learning. I'll put a list below and link them to the explanation i made. 

Javascript:
- <a href="../../deeper-dive-master/javascript/lexical-structure">Lexical Structure</a>
- <a href="../../deeper-dive-master/javascript/expression-statement">Expressions</a>
- <a href="../../deeper-dive-master/javascript/Types">Types</a>
- <a href="../../deeper-dive-master/javascript/variables">Variables</a>
- <a href="../../deeper-dive-master/javascript/function">Function</a>
- <a href="../../deeper-dive-master/javascript/this">this</a>
- <a href="../../deeper-dive-master/es6/arrow-function">Arrow Function</a>
- <a href="../../deeper-dive-master/javascript/loops">Loops</a>
- <a href="../../deeper-dive-master/javascript/scope">Scope</a>
- <a href="../../deeper-dive-master/javascript/arrays">Arrays</a>
- <a href="../../deeper-dive-master/es6/template-literal">Template literal</a>
- <a href="../../deeper-dive-master/javascript/lexical-structure">Semicolons</a>
- <a href="../../deeper-dive-master/javascript/strict-mode">Strict Mode</a>
- <a href="../../deeper-dive-master/es6">ES6</a>

Concepts:
- <a href="../../deeper-dive-master/javascript/asynchronous">Asynchronous programming and callback</a>
- <a href="../../deeper-dive-master/javascript/timers">Timers</a>
- <a href="../../deeper-dive-master/es6/promises">Promises</a>
- <a href="../../deeper-dive-master/es6/promises">Async / Await</a>
- <a href="../../deeper-dive-master/javascript/closures">Closures</a>
- <a href="../../deeper-dive-master/javascript/event-loop">The Event Loop</a>