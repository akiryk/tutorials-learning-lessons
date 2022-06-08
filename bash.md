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
