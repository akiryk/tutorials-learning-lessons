# The Go Standard Library

## Printing and formatting

When using `fmt.Printf()`, you can pass in variables corresponding to the data type. For a complete list, see [the golang fmt docs]([url](https://pkg.go.dev/fmt)). 
```go
// print variable as a string
fmt.Printf("hello, %s", name)

// as a decimal integer
fmt.Printf("hello, %d", number)

// as the default type
fmt.Printf("hello, %v", somevariable)

fmt.Printf("%d in binary is %b\n", 42, 42)
```

- Use `fmt.Printf()` most of the time because it's powerful and flexible.
- Use `fmt.Sprintf()` to hold formatted strings without printing, e.g. `output := fmt.Sprintf("Hello");` and you can print `output` later.
