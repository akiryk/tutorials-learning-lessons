# 1. Instrastructure: Foundation

You can interact with GCP in 4 ways: the console, cloud shell/SDK, the mobile app, and a REST API 

## Cloud Shell Intro

Cloud Shell is an interactive terminal window that gives you:

- built-in authorization for access to resources and instances
- 5 GB of persistent storage
- Command-line access to a free temporary Compute Engine VM

You can create buckets for storing data and files, then upload files from your computer or elsewhere using the shell. Finally, you can copy files from there into the bucket of your choice

```sh
# make a bucket
gsutil mb gs://my_bucket_1

# copy file to that bucket
gsutil cp some_filt gs://my_bucket_1

# Best practice is to use environment variables
# configure the `.profile` file to update shell (it's like bashrc)
MY_BUCKET=gs://my_bucket_1
```

## Virtual Networks

### Useful background on IP addresses
- IP addresses are unique ways of pointing to every computer, printer, router, switch, etc. 
- Subnetting is a way of dividing larger networks into smaller ones.
- We always reserve two IP addresses, one to identify the subnet and another to identify the broadcast address of the subnet.
- If your IP is `192.168.0.147` and your subnet mask is `255.255.255.0`, you know that your network is `192.168.0` and your specific host is ID'd by `147`. 
- There are different sizes of subnets, determined by the specific subnet, which is indicated by a slash after the IP. For example, `192.168.0.147/24` says the subnet mask is 24 bits, which corresponds to `255.255.255.0`. If you used `/20` instead, your mask would be `255.255.240.0`. The important bit is that you can have bigger or smaller subnets based on the specific mask.
- `/30` means you have a network with 4 hosts; `/20` gives more than 4,000.
- An external IP is your public address. An internal IP is private within a private network. 

### Virtual Private Cloud
Projects are the key organizer of infrastructure resources in Google Cloud. A project associates billing with services.
A project contains networks; a network contains regional sub-networks. 
Networks are global and have no IP address range. 

Every project gets a default network with one subnet per region and default firewall rules.

Networks isolate systems. This graphic shows separate virtual machines that can communicate by different means depending on whether they are on the same network or not. A, B, C, and D represent different Virtual Machines. To be clear, C and D communicate over external IPs but not the public internet — they use Google Edge routers. 
<img width="2481" alt="image" src="https://user-images.githubusercontent.com/2437758/173688232-087ea628-2fdb-4674-aa88-8331f88f4193.png">

**Firewalls**
Firewall rules are applied to the network as a whole, but connections are allowed or denied at the instance level.
Even if firewall rules are deleted, there's an implied rule to deny all ingress and allow all egress

### Common Network Designs
- If your app needs increased availability, put multiple VMs in multiple zones but within the same subnet (a **zone** is part of a region; e.g. the region is `us-west1` and the zones are `us-west1-a`, `us-west1-b`, and `us-west1-c`).
- for better latency, put VMs in different regions. 
- for security best-practices, assign only internal IP addresses whenever possible. Gloud NAT can help with this by enabling private instaces to access the internet.
- If your app needs more robust systems, use multiple regions.  

### VMs with no external IP
We create a VM without an external IP and access it with cloud iap. 
We then enable private google access and  so it can access google api services.  

VM instances without external IP addresses are isolated from external networks. With **Cloud NAT**, these instances can access the internet for updates and patches. 

When you make a VM without external IP, you can't ssh to it; however, you can tunnel with iap. To do this, use
```sh
# gcloud ssh [VM_NAME] --zone [ZONE_NAME] --tunnel-through-iap
gcloud compute ssh vm-internal --zone us-central1-c --tunnel-through-iap
```

### Cloud NAT Gateway
In cloud shell, you can update, patch, etc -- e.g. use `sudo apt-get update` and it works!

It won't work if you try `sudo apt-get update` on a VM without external IP. You can fix this by creating a Cloud NAP gateway. Do so 
at the subnet level. 

- go to Network Services > Cloud NAT

## Virtual Machines
A VM is similar to a real piece of hardware with key differences. It includes a virtual CPU, some amount of memory, disk storage, and an IP address. 
On the other hand, a micro-VM shares its CPU with other VMs, so it's cheaper. Also, some offer burst capability; it can offer above-capacity for a brief period. Both of these can't be done by hardware machines.

Google Cloud options for VMs

Compute Engine 
- gives the most flexibility; 
- it's IaaS and you can configure language, scaling. 
- It's very portable.

### Patch management
Critical to maintenance and security for your long-running VMs. Use the OS Patch Management service.

### Machine families
When creating a VM, you have choice of machine families depending on what you need — better price, better memory, etc.

- General Purpose Optimized: There are several options for specific machines from less powerful to more powerful.
- Compute Optimized: things like gaming, ad serving, streaming.
- Memory Optimized: in-memory databases. An in-memory database is faster than one on disk, but requires a lot of main memory. 
- Accelerator Optimized: for computing that requires lots of CPUs 
- Custom: for cases that aren't a good fit with the above options

### Pricing
Google Compute Engine uses per-second billing with a min. of 1 minute. Further, pricing is based on resource use, meaning each virtual CPU and GB of memory is billed separately. 

GCP gives discounts based on a few options

- sustained usage: is you use the VM for a significant portion of a billing period, there's a discount
- preemptible VM: Big discounts, but they only live for up to 24hours and you only get a 30 second heads-up; however, you can put in place controls that will start a new one right away. Useful for batch processing.


### Special configurations
- preemptible
- sole tenant nodes: for isolating workloads based on compliance requirements, for example
- confidential VMs: enable encrypting data while being processed
- shielded VMs: an even more secure foundation so you know your data hasn't been compromised

### Images
When creating a VM, you can choose a boot disk image. Image includes the boot loader, the OS, file system structure, pre-configured software, and customizations.

You can choose a Linux or Windows image. Different types have different charges. You can also use custom images. 

A **machine image** is a compute engine resource that stores all the info requried to create a VM instance. You can use one for system maintentance. They are the ideal resource for cloning and backups. 

### Disk Types
When setting up a VM, you choose an operating system. That OS will be part of a disk, and you can select which type of disk you want. 

Every VM comes with a single root persistent disk; you choose a base image to have it loaded on. 
**?????** What does this mean? 

**Persistent Disks**. These are high performance and attach to either Google Compute Engine VMs or GKE VMs through the network interface. It's not physically attached to the machine, so the disk survives even if the VM terminates. 

There are different kinds of persistent disks, based on cost and performance requirements. 

- Standard is low cost and suited for data processing
- SSDs better for low latenccy and input/output per second (IOPS). 

**Local SSDs** They are _physically attached_ to the machine, so they are not persistent. They will survive a reset but not a VM stop or termination. But they have very high IOPS.

**RAM Disks** Enable you to store data in memory using `tmpfs` (a file system in which all files are in virtual memory). The point of this is to have high throughput and low latency. You'll want to consider an alternate system to back up your data since this method is very volative and erases on restart or stop. 

### Back up data
There are a few ways to do this, each with their own benefits:
- Machine images
- snapshots
- custom images

## Review
This module looked at VNs and VMs and explored common actions. These included:
- create a network and apply different firewall rules
- add VMs of different types
- set up a server with scheduled backups and maintenance 
