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
