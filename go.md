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
### Maps
Maps are key/value pairs known in other languages as dictionaries or hashes. They are restricted to a single type
```go
m := map[string]string{"firstname": "Bilbo", "lastlame": "Baggins", "home": "The Shire"}
// add to an existing map
m["favorite color"] = "purple"

```

### Structs
Structs are collections of properties that can have different types. 
They are like tuples in other languages, but you can think of them as being the data side of a class. 
There will be a fixed number of fields that typically define a concept, e.g. a user. In the case of a user,
the struct might have fields for id, name, email, etc.

```go
// First, you must define the struct with type keyword
type Person struct {
	name    string
	age     int
	hobbies []string
}
  
// you can initialize the struct without populating it at all
var janet Person
fmt.Println(janet) // will use zero-values for name, age, and hobbies, 0 []
// populate one field at a time
janet.name = "Janet"
janet.age = 38
janet.hobbies = []string{"running", "from", "bears"}

// or populate all at once
var saul = Person{"Saul", 33, []string{"biggness", "solitude", "painting"}}

// or populate with keys as well
var bill = Person{
	name:    "Abe",
	age:     101,
	hobbies: []string{"fishing", "sailing", "remote control cars"},
}

```
