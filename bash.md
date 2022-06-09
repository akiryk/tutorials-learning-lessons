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

You create a variable by simply `myvar="some value"`. 
- Use single quotes if you want to escape `$`. `x='$someVariable, world'` will print `$someVariable, world`. 
- Use double quotes by default. `x="$someVariable, world"` will print `[value of $someVariable], world`. 
- don't use spaces `x = "some value"` fails because bash thinks you have a command, `x` with an argument, `=`
- variable names are case sensitive
- use lowercase names because pre-defined variables are all uppercase and you could override them

Retrieve the value with keyword `echo` and `$`, as in `echo $myvar`. Use `echo` to avoid running the script unintentionally. 

Predefined variables include `$USER` and `$SHELL`. To see all of them, use the `printenv` command.

Note that the behavior changes in zsh compared to bash in some respects:
```sh
files="file1 file2"
touch $files
# in bash, you have two files, file1 and file2
# zsh gives just one file, 'file1 file2'
```

There are several predefined variables such as $USER, $SHELL

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
```

### Debugging
- Add `-v` to `#!/bin/bash -v` so that every line gets printed before it runs. This way, you can see where a script hangs up. 
- Add `-x` instead to print also the values being read, which can be more useful

### Printing/Echoing
`echo` is easy to use for printing content to the terminal, but it isn't very powerful. `printf` is better and does more, but can be complicated. 
```sh
# prints My username is akiryk and I'm using the /bin/zsh shell
printf "My username is %s and my shell is %s\n" $USER $SHELL
```
