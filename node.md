# Node

This is a good course: [front-end-masters-node](https://frontendmasters.com/courses/digging-into-node/file-handling-with-streams/)

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
