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
    main_app
        main_app.go # doesn't need to be the same name as the folder; however, package name must be "main"
        go.mod # don't create this manually; it will be created in step 2
    my_package
        my_package.go # doesn't need to be same name as the folder; however, the package name must be the same
        go.mod # don't create this manually; it will be created in step 2
```
2. `cd` into main_app and run `go mod init example.com/main_app`
3. In prod, your main_app package would import the library package from a repo (e.g. `example.com/my_package`). However, for dev purposes, you may want to import a local package. In that case, you need to <code>cd</code> into `main_app` and run `go mod edit -replace example.com/my_package=../my_package`. 
4. Now run `go mod tidy` to update the mod file
5. In main.go, use the code from my_package.go by using `import "example.com/my_package" and by doing something like `fmt.Println(my_package.SayHello())`. 
  
