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

### Compute Engine vs App Engine
Compute Engine is Googles IaaS offering and App Engine is the PaaS offering.

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
Cloud storage is a type of durable "object-storage". This means it manages data as objects; it's a type of nosql storage. Object storage does not store data in a file/folder hierarchy ("file storage") or as chunks of a disk ("block storage"). Objects stored in this way have a globally unique key, usually a URL, so they work well with the web. Typical types of data stored in this way include media like images, audio, and video. 

Its primary use is for BLOB (binary large-object) content. 

Cloud storage files are organized into buckets. The bucket should be located in a region close to end-users. 

Storage objects are immutable; a new version is created with every change. You can either overwrite the old one or use versioning. 

Because data can quickly get big and expensive, you have options called **lifecycle policies**, such as delete objects older than 365 days or before a certain date or delete only but the three most recent changes. 

There are four **storage classses** in cloud storage:

1. Standard storage: best for frequently accessed, or "hot", data; aka business-critical data
2. Nearline Storage: infrequently accessed data (data backups; archiving, etc)
3. Coldline storage: also for infrequently accessed data, even less frequent
4. Archive storage: when you access less than once a year and is the cheapest

You can add data to any of these types of storage using gcloud's `gsutil` command or with a drag-and-drop option in the console. For importing huge amounts of data, use Storage Transfer Service. 

### Cloud SQL
Cloud options for relational databases include MySql, PostGreSQL, and SQLServer.
Using this option doesn't require any special installations. You get encryption, backups, and automatic replications. 

It's best for web frameworks and for storing things like orders and customer information. 

Compute Engine instances can be configured to access Cloud SQL instances.  

### Cloud Spanner
A fully managed relational database that scales horizontally and runs on SQL. It's great for anything that needs a relational database, large dbs, lots of reads/writes. 

Best for largescale db applications.

### Firestore
A no sql db. Data is stored in documents and organized into collections. It's great for synching data in real-time. 

### Cloud BigTable
Google's no-sql big-data service. It powers Google search, maps, and email. It's a great choice for analytics, internet-of-things, large data-sets.

### BigQuery
This will be discussed later because it straddles data-storage and data-processing. It's generally used for big-data analysis and querying. 

## Containers
Containers scale like PaaS but give you the flexitility and control of IaaS. 

At a high level, Kubernetes is a set of APIs that let you deploy and manage containers on a set of nodes called a cluster. A node represents a computing instance, like a VM. 

A pod is the smallest unit in K8s that you create and deploy. A pod represents a running process on your cluster as either a component of your application or your entire app.

## App Engine
A fully managed, serverless platform for developing and hosting applications. It provides nosql, logging, health checks, load balancing, and a user auth api. You use the console to create new applications, configure domain names, and handle other admin. 

1. **Standard App Engine Environment**
Based on containers, the standard env enables:
- persistent storage
- automatic scaling and load balancing 
- async task queues
- scheduled tasks

It's great for many applications, but less flexible. You must select from specified versions of java, php, python, node, and other languages. It must conform to sandbox constraints. 

2. **Flexible Environment**
- Application instances run within Docker containers on Compute Engine virtual machines (VM). 
- It can support custom runtime or source code written in other programming languages.
- Allows selection of any Compute Engine machine type for instances so that the application has access to more memory and CPU 

How does GKE compare to these two options? 
Choose the standard option if you want GCP to take maximum control of you app's deployment and scaling. In contrast, GKE gives you the full flexibility of kubernetes. The flex environment is somewhere between the two. 

### Cloud Endpoints and Apogee Edge
These are management tools for Google's API. 

**Cloud endpoints** is a distributed system that runs in its own docker container. It enables you to create and maintain APIs with low latency. It provides lots of services to help you with your API. It supports applications running in GKE, App Engine and Compute Engine. 

**Apogee Edge** focuses on business problems such as analytics. It's often used for legacy applications, helping spin off microservices one at a time until the legacy app can be retired. 

## Cloud Run
A fully managed serverless platform that runs individual containers. You give code or a container to Cloud Run, and it hosts and auto scales as needed to respond to web and other events.

Use Cloud Run if you just need to deploy a containerized application in a programming language of your choice with HTTP/s and websocket support. Examples: websites, APIs, data processing apps, webhooks.

[**Useful graphic** and explainer](https://cloud.google.com/blog/topics/developers-practitioners/where-should-i-run-my-stuff-choosing-google-cloud-compute-option)

## Monitoring

### The Four Golden Signals
1. Latency: speed and performance of your system as a whole or in part, measured in various ways
2. Traffic: How many requests are reaching your system, e.g. # of http requests per second but also others.
3. Saturation: measures how close to capacity is the service
4. Errors

### SLIs, SLOs, and SLAs
Service Level Indicators (SLIs) are metrics that measure one aspect of a service's reliability, usually expressed as the number of good events divided 
by the number of bad events, e.g. number of some error / count of all successful events.

Service Level Objective (SLO). Combines an SLI with a target reliability. Guidelines for choosing SLOs since you can't measure everything: SMART
- [S]pecific
- [M]easurable
- [A]chievable
- [R]elevant
- [T]imebound, e.g. a given service should be 99% available per the last 7 days.

Service Level Agreement: a promise to maintain a particular level of success and define consequences if there's a problem. 
