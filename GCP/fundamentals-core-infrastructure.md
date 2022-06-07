# Fundamentals: Core Infrastructure

## Introduction

GCP offers 4 main kinds of services:

1. Compute
2. Storage
3. Big Data
4. Machine Learning

This course focuses on Compute and Storage, together with the topic of networking.

What is cloud? Pay for what you use; scale easily.

GCP provides a "solution continuum" from IaaS (infrastructure as a service) to PaaS (Platform as a Service) to SaaS (software as a service).

GCP offers different architectures for different needs. For example:

**Compute Engine** is IaaS: you pay for the infrastructure based on what you allocate.

**App Engine** is PaaS: you pay for the extent to which you use the platform.

**Open APIs**<br/>
GCP makes it easy to use other services that aren't part of Google. Kubernetes, for example, supports interoperability by letting customers mix and match micro-services on different clouds.

**GCP Services**<br/>
Compute: Compute Engine, Kubernetes Engine, App Engine, Cloud Functions

Storage: BigTable, Cloud Storage, etc.

Big Data: BigQuery, Pub/Sub, etc.

Machine Learning.

### Identity and Access Management

**Principle of Least Privilege**<br/>
Each user should have only those privileges needed to do their jobs. GCP uses something called IAM to handle this.

Google handles much of the security, but it's up to customers using IAM to implement rules that make sense for them. Rules flow _downward_. A rule applied to a project flows to a folder. Privileges on a folder apply to its projects.

Note that _less restrictive policies override restrictive ones_. Example: user X only has view privileges, according to the organization level. But a particular project says X has edit privileges for that project's Cloud Storage. **The edit privileges prevail** not the more restrictive ones.

All GCP services are associated with a **project**. Each project is billed and managed separately.

IAM policies have 3 parts:

- Who: A google group, account, etc
- Can do what: defined by an IAM role, a collection of permissions
- on which resource

**IAM Roles**

- primitive: owner, editor, viewer. Only owner can set up billing. Primitive roles are not well suited to sensitive data.
- custom: can only be used at the project or org levels, not folder level.

### Interacting with GCP

You can use the web console, app, SDK, or REST API.
Web console is very useful. You can use the Cloud Shell on the console to interact with the SDK without installing the SDK.

### Quiz 1

Go to console > marketplace and search for LAMP.
Choose LAMP Bitnami and launch.
Once it's launched, enter the shell and create a phpinfo.php page, which you can then view.

## Compute Engine: Virtual Machines in the Cloud

VPC (Virtual Private Cloud).

Compute Engine lets you run virtual machines. They have power of a full OS in each; you configure it like a server (memory, storage, OS, etc).

Use Compute Engine to set up your VM. Choose the type of machine that meets your needs.

### Cloud Load Balancing

A fully distributed, software-defined managed service for all your traffic.
You can put cloud load-balancing in front of all your traffic.
A single IP frontends all your backend instances around the world.

There are different types of load balances for HTTP, SSL, TCP, and other options.

### Create a Virtual Machine in the console

Go to compute engine > VM Instances. Choose options and click Create.
Once the VM is made, you'll see it listed on the VM Instances panel. You can SSH into each instance you create. In this exercise, we made a second instance and proved it could load the web page at the other instance. We did this by enabling HTTP access.

### Infrastructure Overview

GCP provides a "solution continuum" from IaaS (infrastructure as a service) to SaaS (software as a service).

## Storage in the Cloud
Core storage options:
- Cloud Storage
- CloudSQL
- Cloud Spanner
- Cloud DataStore 
- Google Big Table
- Big Query

### Cloud Storage 
Cloud storage is frequently the ingestion point for getting data into the cloud and is frequently the long-term storage location for data. 

What is it? It's binary large-object storage. This means you hand over an arbitrary chunk of bytes and GCP gives you a key so you can access it later. The key is often in the form of a URL, so it works well with the web. 
- You don't need to provision capacity ahead of time. 
- the objects are immutable; you don't change them in place but create new versions; 
- there are various options for managing versioning and keeping or deleting old versions
- there are also options for access, frequent vs infrequent — i.e. multiregional storage vs cold storage (for data access < 1 per year)
    - multi-regional
    - regional
    - nearline
    - coldline
 - there are various ways to get data into Cloud Storage, depending on how much you need to transfer

**Use Cloud Storage if**: you need to store large immutable blobs, such as movies or large images. 

### Big Table
A managed NoSQL solution. It's ideal for data that has a single look up key. In fact, you could think of it as a persistent hash table. 
Big table has some advantages over managing your own data:
- scalability
- all data is encrypted "in-flight" and "at rest"
- it's the same db that powers Gmail and Maps and other Google services
- Data can be read or written with a layer like an HBase REST Server.

`HBase`: Apache Hadoop is a library for handline data. 

**Use Big Table if**: you need to store a large amount of structured objects; it does not support SQL like queries or multi-row transactions. 

### Cloud SQL
Offers MySQL and PostgreSQL databases as a service. It is an RDBMS, "relational db management system", meaning it's a program that allows you to create, update, and administer a relational database. Traditionally, relational DBs are a lot of work to set up and manage; Cloud SQL does a lot of that work for you. 

Scalability: It can scale vertically, by changing the machine type, or horizontally via read replicas (i.e. create a replica with near-realtime data updates to keep replica in sync with the original box). 

Vertical vs Horizontal scaling: **Vertical** means improving the machine by upgrading, adding memory, CPU, etc. **Horizontal** means adding additional machines. 

Alternative: You could run your own db in a virtual machine, but then it's up to you to manage. 

### Cloud Spanner
If you need more horizontal scaling (not just replication), consider Cloud Spanner. It's great for when you need sharding and fits with transactional database uses such as inventory management. 

**Use Cloud SQL or Cloud Spanner if**: you need full SQL support. 

### Cloud Datastore
Also a NoSQL option. It's a horizontally scalable NoSQL db. 

Unlike Cloud Big Table, it offers transactions that update multiple rows.

**Use Cloud Datastore if**: you need to store unstructured objects or if you require support for transactions and SQL like queries.

### BigQuery
THe usual reason to use it is for its big data analysis and interactive querying capabilities. You wouldn't use it as the backing store for an online application.

### Compare options

<img width="1208" alt="image" src="https://user-images.githubusercontent.com/2437758/172006160-c1d6057e-6625-4123-bd8a-3f987fef9206.png">

## GKE: Containers in the Cloud
Google Kubernetes Engine (GKE)

Let's revisit IaaS compared to PaaS. 

**Compute Engine** is an Infrastructure as a Service. You pay to access virtualized insfrastructure that is based on real-world hardware. You install the OS of your choice and you get things like CPU, memory, file systems, networking, but you don't have to manage the real hardware yourself. This has a lot of advantages, but it can take a while to boot up and if you need to scale quickly it can be hard.

**App Engine** is Platform as a Service, You pay to access a "family" of services, such as caching, DB, storage, Networking. Scaling happens easily and rapidly, but you don't have control over the underlying architecture. 

**Kubernetes Engine** is like the best of both of these. It scales like PaaS but gives you nearly the flexibility of IaaS. The container abstraction gives you a lot of portability. You can treat the operating system and hardware as a black box. 

Kubernetes is a tool for deploying containers to a set of nodes called a cluster. Each node in Kubernetes is a computing instance. In Google Cloud, each node is a virtual machine running in compute engine. 

Kubernetes uses "pods". You can have a single container per pod or a bunch of stuff, but it's common to keep them limited to one container. Each pod gets a unique IP address. 

A deployment is a group of replicas of the same pod. 

`kubectl run nameofcontainer` will run a container. Say "cube-c-t-l".
`kubectl get pods` will show you the running pods. 
By default pods in a deployment are only accessible within a cluster. However, you can make them public by connecting a load balancer. You do this with `kubectl expose deployments`. Kubernetes will then create a service that points to a single IP address for your pods. It's a networked load balancer. Any client that hits that IP address will be routed to a pod behind the service. 

`kubectl get services` will show you your public IP address.

The real strength of Kubernetes is not imperative but declarative. Instead of issueing commands, you provide a config file that says how you want your desired end-state to look. Kubernetes takes care of the how.

### kubectl commands
```sh
kubectl get pods
kubectl create deploy
kubectl expose deployment
kubectl get services 
```

## App Engine
Both GKE and GCE provide infrastructure for applications in which you choose the infrastructure in which it runs. GCE uses VMs and GKE uses containers. If you don't want to focus on the infrastructure at all, App Engine may be a good solution. App Engine manages the platform and hardware. You just hand it your code and it takes care of the rest. 

App Engine has to options, Standard and Flexible. 

### Cloud Endpoints 
It enables APIs using a proxy in front of your service. You can use REST and more. Cloud endpoints support apps running in GKE and Compute Engine. 

