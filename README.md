# Presentation transcript
Hello everybody! This is the introduction to Node.js.

Node.js is an opensourse cross-platform project. Which is built on  Chrome’s JavaScript runtime environment. It uses an event-driven, non-blocking I/O model which is perfect for real-time applications that run across distributed devices. All clients in application use the same thread. I/O operations are event based, they don’t block the main thread cycle of application. Also Node.js has an ability to run JavaScript on server and acts as a webserver.
  
In the traditional web application most of the time the main process waits for input/output (memory, disk, network).In this case multi-threading is used. It takes:  
•	high memory usage;  
•	have to manage concurrency;  
•	always waiting for I/O which blocks working process of application.  
Node.js tackled this problems using asynchronous approach with Event Loop capabilities. This approach is perfect for games, chats, streams – something that require intensive requests and interactions of users or clients.

Let’s take a look to the architecture of Node.js. This is basically C++ application which uses V8 engine to execute JavaScript code. V8 engine compiles JavaScript directly into machine code before executing it. The second main part is Libuv, which is responsible for Event Loop with Asynchronous I/O. There are several other modules within NodeJS to perform different functions. These utilities include:  
•	c-ares  –  for DNS Operations  
•	other add-ons such as (http-parser, crypto and zlib)

Let’s take a look to the Event Loop. Instead of threads, Node uses an Event Loop with a stack. Event loop process each request as event. E.g., HTTP server don’t have to wait for the IO operation to complete while it can handle other request at the same time. To avoid blocking, it makes use of the event driven nature of JavaScript by attaching callbacks to I/O requests.

Node.js is a single threaded language which in background uses multiple threads to execute asynchronous code.
Node.js is non-blocking which means that all functions ( callbacks ) are delegated to the event loop and they are ( or can be ) executed by different threads. Event loop don’t have to wait for the answer form this threads. It just keep going to the next loop checking for a new incoming requests and responding to the users with already completed answers.

The following diagram shows a simplified overview of the event loop's order of operations. Event Loop repeatedly fetches new events. On each stage there is queue. Ehen the event loop enters a given phase, it will perform any operations specific to that phase, then execute callbacks in that phase's queue until the queue has been exhausted or the maximum number of callbacks has executed. When the queue has been exhausted or the callback limit is reached, the event loop will move to the next phase, and so on.

There are queue of timers: set Timeout, setInterval, set Immediate – methods which are used for scheduling operations. Also we have close handlers queue: some close callbacks, e.g. socket.on('close', ...);
Between each run of the event loop, Node.js checks if it is waiting for any asynchronous I/O or timers and shuts down cleanly if there are not any.

The Node.js API provides several ways of scheduling code to execute at some point after the present moment.
 setTimeout() accepts a function to execute as its first argument and the millisecond delay defined as a number as the second argument. Additional arguments may also be included and these will be passed on to the function. Here is an example of that:
The above function myTimeout() will execute as close to 1500 milliseconds (or 1.5 seconds) as possible due to the call of setTimeout().
The timeout interval that is set cannot be relied upon to execute after that exact number of milliseconds. This is because other executing code that blocks or holds onto the event loop will push the execution of the timeout back. The only guarantee is that the timeout will not execute sooner than the declared timeout interval.

If there is a block of code that should execute multiple times, setInterval() can be used to execute that code. setInterval() takes a function argument that will run an infinite number of times with a given millisecond delay as the second argument. Just like setTimeout(), additional arguments can be added beyond the delay, and these will be passed on to the function call. Also like setTimeout(), the delay cannot be guaranteed because of operations that may hold on to the event loop, and therefore should be treated as an approximate delay. See the below example. In the above example, intervalFunc() will execute about every 1500 milliseconds, or 1.5 seconds, until it is stopped (see below).

setImmediate() will execute code at the end of the current event loop cycle. This code will execute after any I/O operations in the current event loop and before any timers scheduled for the next event loop. This code execution could be thought of as happening "right after this", meaning any code following the setImmediate() function call will execute before the setImmediate() function argument. The first argument to setImmediate() will be the function to execute. Any subsequent arguments will be passed to the function when it is executed. Here's an example:
The above function passed to setImmediate() will execute after all runnable code has executed, and the console output will be:  
```
before immediate  
after immediate  
executing immediate: so immediate
```

Don't get setImmediate() confused with process.nextTick(). There are some major ways they differ. The first is that process.nextTick() will run before any Immediates that are set as well as before any scheduled I/O. The second is that process.nextTick() is non-clearable, meaning once code has been scheduled to execute with process.nextTick(), the execution cannot be stopped, just like with a normal function.
By placing the callback in a process.nextTick(), the script still has the ability to run to completion, allowing all the variables, functions, etc., to be initialized prior to the callback being called. It also has the advantage of not allowing the event loop to continue. It may be useful for the user to be alerted to an error before the event loop is allowed to continue.

NPM is the default package manager for Node.js. It manages dependencies for an application. It allows users to install Node.js applications that are available on the NPM registry. Benefits of NPM are:  
•	One development language JS on client and server side;  
•	Open source technology;  
•	It saves space, as packages don't have to be installed multiple times for multiple projects;  
•	Global or local installation.  
In local installation, the packages are installed into a directory called `npm_modules` inside the current (i.e. your app's) directory. Node automatically makes all locally installed packages available to a running app, so there are no conflicts with other apps' packages.

To launch npm type `npm init –yes`. After this package.json will be created. It contains some fields:
Version – first number – major, middle – minor and the third – patch. You can change patch if there has been corrected some bugs, minor – when adding new features and major when change functionality of your code. Main – it’s the entrance point for other applications to your module.
To install dependencies type `npm install “module name”`. You can install module globally using `–g` and locally using flag `–save-dev`.

There are some useful modules: live-server – to live stream your code in browser without refreshing it, eslint – to check your code, webpack – to connect your modules in one file to execute it in browser, express – framework to create web server.

Http module has method “createServer()” which takes function with request and response arguments. Object ‘request’ describes incoming request with different headers, path and method. ‘Respose’ is the object which is used for responding. For example we can use method ‘write(‘Hello World!’)’ to invoke ‘Hello World!’ in browser. Then we need to type response.end() to finish response. In order to make server available on the internet we have to assign a port using ‘listen()’ method.
In order to use express framework we have to install it using NPM. This is an extended approach to creating server in Node.js with additional functionality.

Many methods in Node.js can be used in blocking (synchronous) or non-blocking asynchronous way.For reading a file you can use the readFileSync method of the fs class so that Node.js have to wait until file reading is finished.The "normal" way in Node.js is to read in the content of a file in a non-blocking, asynchronous way. That is, to tell Node to read in the file, and then to get a callback when the file reading has been finished.

There were some tips of Node.js. Thank you for attention!
