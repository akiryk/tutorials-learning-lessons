# Node

This is a good course: [front-end-masters-node](https://frontendmasters.com/courses/digging-into-node/file-handling-with-streams/)

## Exports / Module.exports
`module` is a plain javascript object representing the current module.
It has an `exports` property.
`exports` = `module.exports`.
- If you want to export a single class/variable/function, as in `export default`, we can use `module.exports`
- if you want to export multiple variables/function, use `exports`

## Event loop
The node event loop is more involved than the Javascript event loop. There are 5 different queues. In order of precedence:

1a. microtask queue: functions called with `process.nextTick()`, which you shouldn't use anyway
1b. functions invoked by promises
2. timer queue handles timers
3. i/o callback queue for all callbacks associated with node i/o functions (e.g. `on('data', ioCallback)`)
4. Check queue: anything called with `setImmediate()`
5. Close queue: functions called by the `close()` callback

The precise sequence of the loop is like this:
- check if there's anything in 1a/1b.
- now check 2
- now check 1a/b again
- check 3
- check 1a/b
- check 4
- check 1a/b
- check 5
- repeat from beginning


## Streams
Rather than loading entire files into the buffer, use streams, which are well explained in [the streams handbook](https://github.com/substack/stream-handbook)
There is also a [front-end-masters-course](https://frontendmasters.com/courses/networking-streams/) on streams

### Piping
`const stream 3 = stream1.pipe(stream2)`

The pattern here is:

READABLE = READABLE.pipe(WRITEABLE);
Think of it like a `then()` function. 
```
const stream3 = stream1.pipe(result => stream2(result));
```
When you want to execute a node file, you can just say `node myfile.js`. But if you want to add some input to a node file for it to operate on — e.g. hello.txt should be processed by processor.js — then you need to pipe it like so:
```
cat hello.txt | processor.js
```
Note, too, that you can eliminate the `node` command if you make your file executable: `chmod u+x processor.js`
