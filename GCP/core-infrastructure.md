# Google Cloud Fundamentals: Core Infrastructure

[Source Table of Contents](https://app.pluralsight.com/library/courses/google-cloud-fundamentals-core-infrastructure/table-of-contents).

## Introducing Google Cloud
What is the cloud? It's a service in which 
- customers get access to computing resources on-demand from anywhere over the internet
- providers have a big pool of resources which they use to allocate based on what customers want/need, enabling economies of scale
- resources are elastic and flexible
- pay only for what you use 

We got to the cloud by starting with on-site servers. We then started using co-location, to save money -- then virtualization. And finally containerization:

<img width="1260" alt="image" src="https://user-images.githubusercontent.com/2437758/174881960-ff508753-6804-429a-a8b1-cd6ca4375b91.png">

## IaaS and PaaS
In IaaS model, you pay for services that you allocate ahead of time, as in: I want some CPUs and storage and network capacity. It's similar to a physical data center but is virtual. You only pay for what you use, but you need to decide what that is. It's like building your own venue where you'll put on your show.

In PaaS model, you pay only for what you use and you don't have to worry as much about the details. It's great for building applications. It's like renting a venue to put on a show vs. building the venue yourself. 

SaaS is another term, although not something related to GCP. Software as a Service is software that runs in the cloud and is used by end-users over the internet. Examples include Google Drive, gmail, etc. 

## The Network
You set up servers and storage in regions and zones around the Google global network. A region is something like Europe or Asia, and you can use regions for redundancy and security. Zones are things like europe-east and europe-west. You can also use multiple zones. Location affects 
- durability: the resource will continue to exist, say, because of backups or redundancy
- availability: system uptime, measured as a percentage
- latency: time from server to user

Google has wide-ranging security protections; enables customers to leave at any time thanks to wide usage of open-source tools such as Kubernetes, and enable pricing tailored to your workload.

## Pricing
You can use alerts, quotas and other tools to ensure you aren't hit with a big price increase. 

# Resources & Access

## Organization of GCP
- Resources are things like storage buckets and VMs
- Resources live inside of **projects**
- Projects  organize your resources and are or can be organized into folders
- Folders enable granular control of privileges for administration
- Organization Node is the top level.

Policies are managed and applied from the top downward. 

## Identity and Access Management (IAM)
Who can do what with which resources.

Can do what part is defined by a **role**. Roles include
- basic: owner, editor, viewer, billing admin
- predefined: roles such as instance admin, which has privileges on compute engine
- custom: define your own roles

**Service accounts** enable you to give permissions to a VM.

**Cloud Identity** enables orgs to manage their users and groups through a console, e.g. to disable a user who has left the company or add a new user.

## Interacting with GCP
You can use the console, the sdk, the mobile app, or an API.
- The SDK and cloud shell is available through a terminal and has tools such as `gsutil` and the `gcloud` command, which are located in the `bin` directory. 

## Google Compute Engine: VMs and Networking
You generally start with a virtual private cloud (VPC). What is a VPC? 
It's everything that can be on a public cloud, but it's secure and private: it can be servers, databases, function, VMs; you can host websites there or have services; and you can set firewall rules and include routes to forward traffic to specific destinations. 

Google VPCs are global and can have subnets in any region. This **is important because** it enables solutions that are resilient yet retain a simple network layout — two VMs can be in different zones but on the same subnet.

Compute Engine is Google's IaaS solution. Enables creating VMs that can be configured much like a phsyical server. You choose pre-defined from the "marketplace" or customize your own machine types. Use a pre-emptible machine for jobs that can be unexpectedly interrupted. 

Routing tables are built-in, and are used to forward traffic from one VM to another within or across subnetworks and zones. 

Firewall rules can be defined through meta-data tags on VM instances.

## Cloud load balancing
Its job is to distribute traffic across multiple instances of an application. You can put it in front of all your traffic, and you don't have to worry about scaling or managing the balancers. 

There are different load balancing solutions depending on your requirements: global HTTP for web traffic, SSL Proxy for secure sockets, regional, and regional internal, which is for load balancing within your network, say between your business and presentation layers. 

## Cloud DNS
This enables the world at large to find applications built in the cloud. 
Cloud CDN can be set up to reduce latency and load. After HTTP load balancing is set up, enable the CDN with a single checkbox. 

## Connect networks outside google
You can connect to on-site networks or to other VPCs using VPN, but Google provides a few other ways: direct peering, carrier peering, dedicated interconnect, or partner interconnect. 

- allow-icmp rule: In order to connect to an external IP use the allow-icmp rule. 
- allow-ssh allows ssh
- allow-custom allows access to the internal IP

## Storage
Google Cloud has five storage options for structured, unstructured, transactional, and relational data.

### Cloud Storage
Duragle "object-storage". This means is manages data as objects and is a type of nosql storage. Object storage does not store data in a file/folder hierarchy ("file storage") or as chunks of a disk ("block storage"). Objects stored in this way have a globally unique key, usually a URL, so they work well with the web. Typical types of data stored in this way include media like images, audio, and video. 

Its primary use is for BLOB (binary large-object) content. 

Cloud storage files are organized into buckets. The bucket should be located in a region close to end-users. 

Storage objects are immutable; a new version is created with every change. You can either overwrite the old one or use versioning. 

Because data can quickly get big and expensive, you have options called **lifecycle policies**, such as delete objects older than 365 days or before a certain date or delete only but the three most recent changes. 

There are four **storage classses** in cloud storage:

1. Standard storage: best for frequently accessed, or "hot", data; aka business-critical data
2. Nearline Storage: infrequently accessed data (data backups; archiving, etc)
3. Coldline storage: also for infrequently accessed data, even less frequent
4. Archive storage: when you access less than once a year and is the cheapest

### Cloud Spanner

### Cloud BigTable
