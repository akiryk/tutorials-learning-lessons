# Front End Masters JS The Hard Parts

### Random notes

Javascript is comprised of three parts
- Memory (local, global)
- Thread of execution (single threaded, synchronous)
- Call Stack (LIFO)

How then do we do things like network calls? DOM manipulation? Set timers?
JavaScript needs to work with the browser or with modules provided by node and the like. 

**Browser/JS relationship**
| Browser      | JavaScript |
| ----------- | ----------- |
| HTML DOM      | Document       |
| Timer   | setTimeout        |
| fetch/xhr | network requests |
