# Front End Masters JS The Hard Parts

### JavaScript overview

Javascript is comprised of three parts
- Memory (local, global)
- Thread of execution (single threaded, synchronous)
- Call Stack (LIFO)

There's another part called the `callback queue` that functions a bit like the call stack, but for functions that are called from the browser, such as with setTimeout. 

How then do we do things like network calls? DOM manipulation? Set timers?
JavaScript needs to work with the browser or with modules provided by node and the like. 

**Browser/JS relationship**
| Browser      | JavaScript |
| ----------- | ----------- |
| HTML DOM      | Document       |
| Timer   | setTimeout        |
| fetch/xhr | network requests |

### Event Loop

There are three main lists of operation in JavaScript:
- the main synchronous thread, which includes the call stack
- a microtask queue, which is a list of things to do based on asynchronous events (e.g. promises)
- a task queue or callback queue, which handles functions called back from setTimer or setInterval

The event loop has these rules
1. Handle things in the main thread first
2. Handle things in the `microtask queue` next
3. Handle things in the callback queue aka `task queue` only once main thread is complete.
