# Bash

## Plurasight Bash Intro Course
Bash is simply a text file run by an interpreter, the Bash programming language. In order to run a file, you must have executable permissions, which you can add as below:
```sh
# inside myfile.sh

# change permissions by adding x to user:
chmod u+x myfile

# run the file:
./myfile.sh

# check permissions
ls -la
# results in: -rwxr--r--    1 akiryk  staff  1843 Dec 30 08:52 ex3.js
```
