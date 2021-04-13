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

## Post-introduction

Now there is some little things to understand before diving deeper into NodeJS. The NodeJS environement comes with some things by default when you run a NodeJS app or program. 

`process`, for example is an object that gather some information about the runnning program.

```javascript
console.log(process.env);
```

The code above will show you some information about the environement in which your program is running. If you are failiar with the linux environement ( if you are running on linux ), you can see the PWD property. You can see the shell path, the username and your log name and some other information. To exit a node program, put the following line into your code :

```javascript
process.exit(1);
```

There is also modules. Modules is an object that contains all the 'export' on a file that will be accessible on another file. Actually there is two object but the second is just a reference pointing to one entry in the first. To make things clear here is an example: 

```javascript
// file1.js
function hello() {
  console.log('Hello World!');
}

module.exports = hello;

// ---

//file2.js
const hello = require('./file1.js');

hello();
```

As you can see you can write code in one file and use some part of your code inside another file. Let's dimistify the most important things to understand here. First the export. You have to assign `module.exports` what you want to use inside the other file(s). When you use `module.exports` you set a 'default' export which means that when you will later `require` the content of the file, the value of that variable will contains what is inside `module.exports`. 

```javascript
// file1.js
function hello() {
  console.log('Hello World!');
}

module.exports = hello; // Here i export the 'hello' function

// ---

//file2.js
const hello = require('./file1.js'); // So there 'hello' will contain the 'hello' function from the first file

hello();
```

Ok, but why that precision ? Because you can exports more that one things, but only one 'default'. We see that exporting a 'default' value from a file is done using `module.exports`. But for any other exports you need to use `exports.<NAME>`. See the following code :

```javascript
// file1.js
function helloEnglish() {
  console.log('Hello World!');
}

function helloFrench() {
  console.log('Bonjour tous le monde!');
}

exports.helloEN = helloEnglish;
exports.helloFR = helloFrench;

// ---

//file2.js
const hello = require('./file1.js'); // what's in here ?
```

So what is inside hello from file2 ? An object that contains both exports like so :

```javascript
const hello = require('./file1.js');

hello.helloEN();
hello.helloFR();
```

You can also use only one of the thing you exported doing this :

```javascript
const helloFR = require('./file1.js').helloFR;
```

Here what you are doing is just simple javascript you create a variable and you assign it the function. It is the same as doing this :

```javascript
const myExports = {
  helloEN: function() {
    console.log("Hello World!");
  }
};

const helloFR = myExports.helloFR;
```

If you struggled understanding this, maybe head to <a href="../../deeper-dive-master/javascript/function">javascript function</a> section where i dimistify all of this.