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

## Virtual Networks and Virtual Machines

### Virtual Private Cloud
Projects are the key organizer of infrastructure resources in Google Cloud. A project associates billing with services.
A project contains networks; a network contains regional sub-networks. 
Networks are global and have no IP address range. 

Every project gets a default network with one subnet per region and default firewall rules.

Networks isolate systems. This graphic shows separate virtual machines that can communicate by different means depending on whether they are on the same network or not. A, B, C, and D represent different Virtual Machines. To be clear, C and D communicate over external IPs but not the public internet — they use Google Edge routers. 
<img width="2481" alt="image" src="https://user-images.githubusercontent.com/2437758/173688232-087ea628-2fdb-4674-aa88-8331f88f4193.png">
