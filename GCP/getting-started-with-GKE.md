# Getting Started with GKE

## Containers

What are they and why use them rather than simply deploying apps straight to a virtual machine?

How did it used to work? Well, time was, you'd buy an actual server — hardware — and install an OS and any other libraries or dependencies plus your application.
If you needed to scale up, you'd need to built up or out (e.g., by adding CPU to your server or by adding more servers).

The next stage was with virtual machines. Problems emerge, however, when running multiple applications on a single VM:

- They both share the same dependencies, so upgrading deps for one can cause problems for the other
- one might hog processing power

You can implement a new VM for every application, but this quickly becomes unmanageable and inefficient.

The container way: a single VM can have multiple user-spaces that each have their own dependencies. These are lightweight and
don't require a full OS, they only require the "user space" part of the OS. The kernel part of the OS is shared by others on the VM.
These things — these self-contained user spaces with their own dependencies — are containers. Because they don't each need
a full OS, they can be spun up quickly. Because they have their own dependencies, they don't need to worry about clashing
with others on the same VM.

<img width="1168" alt="image" src="https://user-images.githubusercontent.com/2437758/175406517-ce9eb34e-222d-418c-abb6-a5f36b93fa99.png">
