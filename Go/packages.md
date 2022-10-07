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
