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
- If your app needs increased availability, put >1 VM in multiple zones but within the same subnet
- If your app needs increased robust systems, use multiple regions.  

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
