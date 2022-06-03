# Google Cloud Platform

## Fundamentals: Core Infrastructure

### Introduction

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

## Virtual Machines in the Cloud

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

## Infrastructure Overview

GCP provides a "solution continuum" from IaaS (infrastructure as a service) to SaaS (software as a service).
