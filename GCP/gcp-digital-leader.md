# Google Cloud Digital Leader Exam Prep
See course: https://cloudacademy.com/learning-paths/google-cloud-digital-leader-exam-preparation-1-4155/

## Setting up a GCP Environment

- Create Projects
- Manage Users
- Enable APIs
- Manage Billing

### Permissions
Best practice: create "roles" with defined permissions and then assign them to users. 

There are three types of roles, but we recommend just two, Predefined or Custom. 
- Basic tends to give too many or too few permissions. They include Browser, Viewer, Editor, and Owner, so not great for production. 
- Predefined roles provide smaller sets of permissions for specific resources. 
- Custom roles

Best practice: always give the fewest permissions as you can.

### Billing

## Setting up a Linux Virtual Machine

## Design a Google Cloud Infrastructure

### Case Study
We're building an IaaS for a company that has an interior design application with web clients in north america but with hopes to expand internationally. It wants to migrate both Linux and MS systems to the cloud in order to scale more rapidly. 

#### Existing technical environment:
- MySQL db for the design app
- MS SQL Server for payments
- NoSql for dev environment
- Apache and tomcat servers with specific CPU and RAM requirements
- Active Directory  
- a File Server for internal documents
- not using containers

#### Compute Options
For our case study, we can consider App Engine, GKE, and Compute Engine, but the choice is Compute Engine. 

Why not App Engine?
- Because it's advised mainly for creating a new application, not migrating an existing one
- it's designed for microservices based apps
- we want to manage the underlying infrastructure, such as RAM and CPU

Why not GKE?
- because the case study company doesn't already use containers

We choose Compute Engine and need to configure our VMs. Start by looking at our current environment, e.g. Tomcat running on 2 dual-core CPUs with 24GB of ram. For RAM, we can simply select a compute engine instance with the matching amount, but the CPU calculation is slightly more complicated because of how virtual CPUs (vCPUs) work. It can actually be more complicated than this, but for this example, we need to double the amount:

- 2 dual-core CPUs mean 4 CPUs
- 4 * 2 = 8vCPUs

Once we know RAM and CPU requirements, we can either select from pre-existing Compute Engine options or create customer VMs.

#### Storage Options
We have a few options on GCP:
- Standard Persistent Disk: low cost
- SSD Persistent Disk: faster but more money
- Local SSD: faster still, but high risk because they are directly attached to your instance. This makes them faster but vulnerable to failures
- RAM Disks: faster still but more expensive and less durable than SSDs so only suitable for temporary storage
- Cloud Storage. This is usually for bucket storage. Bad: can't be used as a root disk. Good: multiple instances can write to the bucket at the same time; good for global access; good for general purpose file sharing.

#### Availability
Ensure availability by having instances in multple zones within a region or, better yet, in multiple regions. A region contains many zones, so `us-central1` contains `us-central1-a` and `us-central1-b` etc.

For a higher level of availability, use **autoscaling instance groups**. These are managed groups of VM instances that automatically add or remove VM instances depending on load. This only works with managed instance groups. In order to use this option:
- over-provision by 50% of your needs
- use a Cloud Load Balancer
- Instances cannot have stateful data; you need to use a database or Cloud Storage, which is automatically replicated. Cloud SQL has a "high availability" option. 

#### Networks
aka Virtual Private Clouds (VPCs). You don't need Organizations or Folders when organizing your GCP account, but you do need Projects. Projects have separate security controls. Projects by default come with up to 5 networks.

A network belongs to only one project and spans all regions; a subnet belongs to only one network and can belong to only one region; an instance belongs to only one subnet.

A subnet allows you to define an IP range and a default gateway for the resources it contains. 

What about communication among instances? VMs can communicate with one another even if in different subnets, although the default firewall rules say only by SSH, [RDP]([url](https://www.cloudflare.com/learning/access-management/what-is-the-remote-desktop-protocol/)), and [ICMP](https://www.cloudflare.com/learning/ddos/glossary/internet-control-message-protocol-icmp/). 

How can instances in different projects communicate with each other?
1. Internet: slower and less secure and more expenseive
2. VPC Network Peering: two VPCs can connect over google's network without a public IP
3. Shared VPC: this is mainly for enforcing security standards

#### Authentication & Security
IAM and Access Control Lists (ACLs).
- Iam is usually recommended for controlling access to your resources
- ACLs are best when you want fine-grained control, such as who can access what object in a given storage bucket. 

GCP takes care of encryption both in-flight and at-rest. 

#### DDoS attacks
this is a shared responsibility between GCP and you. Your part includes:
- good firewall rules
- use default anti-spoofing protection
- few external IP addresses unless necessary
- use load balancing, since it acts as a proxy to hide your internal instances
- use Cloud Armor
