# Go

## Arrays
There are 4 array-like constructs in Go
- array
- slice
- map
- struct

### Array
```go
// initialize an array of 2 ints
var arr[2] int
arr[0] = 20
arr[1] = 30
```

### Structs
Structs are collections of properties that can have different types. 
They are like tuples in other languages, but you can think of them as being the data side of a class. 
There will be a fixed number of fields that typically define a concept, e.g. a user. In the case of a user,
the struct might have fields for id, name, email, etc.
