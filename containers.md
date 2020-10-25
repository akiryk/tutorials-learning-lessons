# Containers

* [Front end masters course](https://frontendmasters.com/courses/complete-intro-containers/chroot/)
* [Helpful files and how-tos](https://btholt.github.io/complete-intro-to-containers/chroot)

When you make a container, you make a self-contained environment. It knows nothing of the outside, so you need to "copy" everything included the OS inside. 

There are three key parts to this:
1. `chroot` change the root directory of the project so that the containerized environment thinks it's at the base root with nothing else
2. 

`ldd` command lists requirements for a file. 
```sh
ldd /bin/cat
# above will print
/lib/x86_64-linux-gnu/libc.so.6
/lib64/ld-linux-x86-64.so.2
# which indicates we need these two files placed in the lib and lib64 directories.
```
