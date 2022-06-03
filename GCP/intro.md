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

`IaaS` Infrastructure as a Service
`PaaS` Platform as a Service.

GCP offers different architectures for different needs. For example **Compute Engine** is IaaS; you pay for actual infrastructure you allocate. **App Engine** is PaaS; you pay for what you use.

**Open APIs**<br/>
GCP makes it easy to use other services that aren't part of Google. Kubernetes, for example, supports interoperability by letting customers mix and match micro-services on different clouds.

**GCP Services**<br/>
Compute: Compute Engine, Kubernetes Engine, App Engine, Cloud Functions

Storage: BigTable, Cloud Storage, etc.

Big Data: BigQuery, Pub/Sub, etc.

Machine Learning.

### Getting Started with GCP

**Principle of Least Privilege**<br/>
Each user should have only those privileges needed to do their jobs. GCP uses something called IAM to handle this.

Google handles much of the security, but it's up to customers using IAM to implement rules that make sense for them. Rules flow _downward_. A rule applied to a project flows to a folder. Privileges on a folder apply to its projects.

Note that _less restrictive policies override restrictive ones_. Example: user X only has view privileges, according to the organization level. But a particular project says X has edit privileges for that project's Cloud Storage. **The edit privileges prevail** not the more restrictive ones.

All GCP services are associated with a **project**. Each project is billed and managed separately.

## Infrastructure Overview

GCP provides a "solution continuum" from IaaS (infrastructure as a service) to SaaS (software as a service).
