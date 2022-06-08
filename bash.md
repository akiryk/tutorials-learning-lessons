# Bash

## Plurasight Bash Intro Course
Bash is simply a text file run by an interpreter, the Bash shell, zsh, or sh. In order to run a file, you must have executable permissions, which you can add as below:
```sh
#!bin/bash
# Always start your file like so to ensure it's run by the bash shell

# change permissions by adding x to user:
chmod u+x myfile

# run the file:
./myfile.sh

# check permissions
ls -la
# results in: -rwxr--r--    1 akiryk  staff  1843 Dec 30 08:52 ex3.js
```

### Variables
While it is possible to work with numbers, bash isn't the best tool. Variables are best thought of as strings and only strings. 

You create a variable by simply `myvar="some value"`. No spaces! `x = 5` fails because bash thinks you have a command, `x` with an argument, `=`

Retrieve the value with keyword `echo` and `$`, as in `echo $myvar`. Use `echo` to avoid running the script unintentionally. 

Note that the behavior changes in zsh compared to bash in some respects:
```sh
files="file1 file2"
touch $files
# in bash, you have two files, file1 and file2
# zsh gives just one file, 'file1 file2'
```

### Your first script
Create a script file comprised of commands. You can refer to arguments with the dollar sign and the number of the argument. For example `$1` refers to the first argument.
```sh
#!/bin/bash

# create a variable
directory="reports"

# Create a report file using the variable. The -p says not to cause an error if the directory already exists. 
mkdir -p $directory

# search for the string passed as the first argument and create a new file with that name
grep $1 shipments.csv > $directory/$1.csv

# communicate success to the user
echo Report created.
```

The above script can be used like so:
```sh
# pass `claire` as first argument.
./scriptname claire
