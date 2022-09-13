# Go

## Arrays
There are 4 array-like constructs in Go
- array
- slice
- map
- struct

### Array
```go
// Longform initialization (an array of 2 strings)
var names [2]string
names[0] = "Carlos"
names[1] = "Sandra"

// Short form initialization
names := [2]string{"Carlos", "Sandra"}
```
### Slice
A slice is built on top of the array construct. It's flexible; Go assigns memory for you and then copies to a different memory location if the array gets too big
```go
slice := []int{1,2,3}
slice = append(slice, 4, 5, 6, 7) // 1 2 3 4 5 6 7
slice = slice[2:]                 // 3 4 5 6 7
slice = slice[:3]                 // 3 4 5
slice = slice[1:2]                // 4
```

### Structs
Structs are collections of properties that can have different types. 
They are like tuples in other languages, but you can think of them as being the data side of a class. 
There will be a fixed number of fields that typically define a concept, e.g. a user. In the case of a user,
the struct might have fields for id, name, email, etc.
