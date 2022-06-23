# Getting Started with GKE

## Containers

What are they and why use them rather than simply deploying apps straight to a virtual machine?

How did it used to work? Well, time was, you'd buy an actual server — hardware — and install an OS and any other libraries or dependencies plus your application.
If you needed to scale up, you'd need to built up or out (e.g., by adding CPU to your server or by adding more servers).

The next stage was with virtual machines. Problems emerge, however, when running multiple applications on a single VM:

- They both share the same dependencies, so upgrading deps for one can cause problems for the other
- one might hog processing power

You can implement a new VM for every application, but this quickly becomes unmanageable and inefficient.

Finally, we have the container way: a single VM can have multiple containers that each have their own dependencies. Developers like this because:

- These are lightweight and don't require a full OS,
- they only require the "user space" part of the OS, not the kernel. The kernel part of the OS is shared by others on the VM.
- Because they don't each need a full OS, they can be spun up quickly. You're just starting up the application, not booting up the entire VM and initializing an new Operating System. 
- Because they have their own dependencies, they don't need to worry about clashing with others on the same VM.
- it's easy to copy them because they are just images; it's like copying a file
- They work really well with the microservices design pattern

In the following graphic, we see a VM with 2 containers:

<img width="1168" alt="image" src="https://user-images.githubusercontent.com/2437758/175406517-ce9eb34e-222d-418c-abb6-a5f36b93fa99.png">

### Container vs Image
An application and its dependencies are called an **image**. A **container** is simply a running instance of an image.

Fact: containers are a Linux construct; you can't run a container natively in OS or Windows; you need a virtual linux environment. Containers use Linux c-groups to control what an application can use (cpu and other resources)

You need software to build container images and to run them. Docker is one such tool and it does both. 

In broad terms, Docker enables you to create a container with a Dockerfile based on "layers." You start with `FROM`, which creates the first layer, a particular version of Linux, say: `FROM ubuntu:1804`. You then add a next layer, say your application, by copying it in with the copy command: `COPY ./app`. `RUN` builds the application and the last layer uses `CMD` specifying what command to run when it's launched, e.g. `CMD java app/MAIN`

You can build your own containers, but it isn't necessarily so simple. You can use Google's container registry or other public registries to access existing images with the user space you want. 
