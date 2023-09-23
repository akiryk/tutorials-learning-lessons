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

To be specific:

```js
function display(data) { console.log(data) }
function printHello() { console.log('Hello') }
function blockFor300ms() { // block for 300ms }

setTimeout(printHello, 0);

const tweets = fetch("www.twitter.com/tweets/idNameBill1221/1"); // say it takes 200ms to return
tweets.then(display);

blockFor300ms();

console.log("hi there!");
```
What happens when?
1. We log "hi there!"
2. We log the data returned from fetch
3. We print "Hello" 

```
## Closures
A function creates a variable environment. If it's returned from within another function, it brings with it a hidden property called `[[scope]]` that includes the variable environment. This collection of variables is something we call "closure", but perhaps a more precise name is Persistent Static/Lexically Scoped Reference Data. This is data that will stick around; it's statically scoped as opposed to dynamically scoped, meaning it's determined when the function is created, not based on where it's invoked. And it's data.

