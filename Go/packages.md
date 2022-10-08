# Packages in Go

## Overview
There are two types of packages
1. Main
2. Libraries

Main packages are the main binary that runs your program. It's the single **entrypoint** for your application.

Libraries should be logically coherent and are used by other libraries or binaries. The critical point, however, is they don't stand on their own; their used by something else.

Where do these packages live?

`main` package can be in any directory and don't need to match the name of the directory. Other packages must be in a directory of their name —
that is, package `mylib` must be in a folder called "mylib"

## Make and use a package
This requires a proper directory structure, proper `go.mod` files, and use of `go mod tidy`. Plus, one very special command.

1. Create your directory structure
```sh
my-project
    main
        main.go
    package
        package.go
```
2. `cd` into each directory and run `go mod init example.com/main` and `go mod init example.com/package`. Note that main and package can be named anything.
3. In prod, your main would import the package from a repo (e.g. `example.com/package`). However, for dev purposes, you may want to import a local package. In that case, you need to <code>cd</code> into `main` and run `go mod edit -replace example.com/package ../package`
4. In main.go, use the code from package.go by using `import "example.com/package" and by doing something like `fmt.Println(package.SayHello())`. 
  
