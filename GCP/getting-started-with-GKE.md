# Getting Started with GKE

## Introduction to Containers

What are they and why use them rather than simply deploying apps straight to a virtual machine?

How did it used to work? Well, time was, you'd buy an actual server — hardware — and install an OS and any other libraries or dependencies plus your application.
If you needed to scale up, you'd need to built up or out (e.g., by adding CPU to your server or by adding more servers).

The next stage was with virtual machines. Problems emerge, however, when running multiple applications on a single VM:

- They both share the same dependencies, so upgrading deps for one can cause problems for the other
- one might hog processing power

You can implement a new VM for every application, but this quickly becomes unmanageable and inefficient.

Finally, we have the container way: a single VM can have multiple containers that each have their own dependencies. Developers like this because:

- These are lightweight and don't require a full OS,
- they only require the "user space" part of the OS, not the kernel. The kernel part of the OS is shared by others on the VM.
- Because they don't each need a full OS, they can be spun up quickly. You're just starting up the application, not booting up the entire VM and initializing an new Operating System. 
- Because they have their own dependencies, they don't need to worry about clashing with others on the same VM.
- it's easy to copy them because they are just images; it's like copying a file
- They work really well with the microservices design pattern

In the following graphic, we see a VM with 2 containers:

<img width="1168" alt="image" src="https://user-images.githubusercontent.com/2437758/175406517-ce9eb34e-222d-418c-abb6-a5f36b93fa99.png">

### Container vs Image
An application and its dependencies are called an **image**. A **container** is simply a running instance of an image.

Fact: containers are a Linux construct; you can't run a container natively in OS or Windows; you need a virtual linux environment. Containers use Linux c-groups to control what an application can use (cpu and other resources)

You need software to build container images and to run them. Docker is one such tool and it does both. 

In broad terms, Docker enables you to create a container with a Dockerfile based on "layers." You start with `FROM`, which creates the first layer, a particular version of Linux, say: `FROM ubuntu:1804`. You then add a next layer, say your application, by copying it in with the copy command: `COPY ./app`. `RUN` builds the application and the last layer uses `CMD` specifying what command to run when it's launched, e.g. `CMD java app/MAIN`

You can build your own containers, but it isn't necessarily so simple. You can use Google's container registry or other public registries to access existing images with the user space you want. 

### Cloud Build
Tools for CI/CD pipelines

## Kubernetes
A container-centric management environment. It automatest the deployment, scaling, load-balancing, monitoring, and logging of containerized applications. 

It has declarative configuration, so you tell it the desired state and it figures out how to get there. However, if you want to, you _can_ configure it imperatively. 

1. K8s supports **stateless** applications, such as an nginx or apache serve and **stateful** applications where user and session data can be stored persistently. 
2. Autoscaling
3. Resource Limits
4. Extensibility
5. Portability: it can be moved and deployed anywhere

Google's managed offering for Kubernetes is GKE. Why use it?

### GKE
The VMs that host your containers inside a GKE cluster are called nodes. 

### Why choose a compute option?
There are several GCP options and each has reasons you may want to use it. 

**Why choose Compute Engine**: fully customizeable virtual machines
- complete control over your OS and virtual hardware
- most flexible when other solutions don't fit your needs

**Why choose App Engine**: A fully-managed code-first platform
- you just want to code and deploy your website or mobile app
- you want to present a RESTful API

**Why choose Google Kubernetes Engine**
- You have a containerized application
- cloud-native distributed systems
- you want more control over your containers than what App Engine provides
- you want denser packing than what Compute Engine offers

**Why choose Cloud Run**: enables stateless containers
- you want to pay very little (only for the time it is actually responding, good for hobbyists)
- you don't need the slight speed boost of App Engine

**Why choose Cloud Functions**: event-driven, serverless compute service
- can be super helpful for supporting your microservices architecture
- integrate serverless app with third party APIs

## Kubernetes Architecture

### Kubernetes Concepts

1. K8s Object Model
2. The Principle of declarative management

The K8s object is a persistent entity that represents two things: the current state and the desired state of the cluster. This "state" pertains to applications, the resources that are available to them, and policies. 

Pods are the basic building blocks. A pod is the environment for containers and may have 1 or more of them. Pods are the smallest, deployable K8s object. Multiple containers in a pod are tightly coupled and share a network namespace and IP. 

### Kubernetes Control Plane

In order to work, a cluster requires a few things. First and foremost, it needs computers — in GCP, that means VMs. One of these VMs is called the control plane and the others are called nodes. The job of the nodes is to run the pods; the control plane coordinates the cluster. 

When you use the `kubectl` command, you're communicating with the control plane (specifically, the kube API server, which resides there). 

Beyond the API server, the control plane includes a database for storing state of the clusters and tools for scheduling, monitoring, managing pods, and fixing issues. 

### GKE Concepts (or why use it rather than rolling your own)
First, GKE handles all of the control plane components for us. Next, instead of you having to spin up VMs (nodes), GKE does it for you — it deploys and registers Compute Engine instances as nodes. Because they run on Compute Engine, you choose the machine type and other details.

Node pools. What are they and why use them? Not clear, but they are a way to have a bunch of nodes that share the same configuration, say, a few nodes that require more or less memory. 

When you create a cluster, the default is 3 nodes in a single zone. You can improve stability by using a GKE regional cluster, which has a single endpoint but uses multiple zones within a region. 

### Kubernetes Object Management
Controller objects manage the state of our pods. These controller objects represent the applications, daemons, and batch jobs running on your clusters. There are different types of controller objects, including deployment controller, stateful set controller, daemon controller. These controllers enable us to use a single yaml file. 

### Lab: managing k8s
Use the Kubernetes Engine tab in the navigation to create, monitor, and modify clusters. 
Edit the number of nodes by going into the node pool section. See the yaml file, see logs, and everything else there, too. 

### Anthos
Migrate for Anthos is a tool for getting workloads into containerized deployments in the cloud. Even if your application isn't in a k8s envvironment or not in the cloud, it can automatically migrate for you. Migration is a multistep process. In order to kick it off, you need correct permissions (admin level) and you need firewall and other settings in place. 

1. create processing cluster in Compute Engine
2. Install the Anthos process using `migctl setup install`, which installs all needed for the migration
3. Create a migration plan using `migctl migration create` command
4. There's more to it than this — but it's basically a set of predefined steps. 

## Introduction to Kubernetes Workloads
### Kubectl command
You use `kubectl` to communicate with the Kube API server on your control plane. Before it can do anything, first you need to configure it with the location and credentials of a kubernetes cluster. Once configured, you use it to create kubernetes objects, view, delete, and view config files.

In general `kubectl` is a tool for administering the internal state of an existing cluster. It can't create new clusters or change the shape of existing clusters. For that, you need the gke control plane — `gcloud` and clould console are your tools.

### Deployments
Deployements describe a desired state of pods. 
Deployments are designed for stateless applications such as web frontends. A backend stores data persistently and other k8s objects (not deployments) will access it. 
Deployment is a 2-part process. There's a yaml file and a deployment controller. 
A controller is a loop-process created by kubernetes to ensure pods are as specified.

There are three ways to create a deployment
- declaratively, using a yaml file
- imperatively, doing it inline in a terminal
- use the GKE workloads menu in the cloud console.

### Deployment strategies
**Blue/Green deployments**

This is a strategy for upgrading to a new version of your application only after you've fully tested it. YOu create a v2 version that spins up as v1 is still in use. Only then do you update the `.yaml` file to point to v2. The disadvantage is you're using twice as many resources for a period of time. 

**Canary**

A variation on blue/green strategy; in this case, the rollout is gradual. It minimizes excess usage during the update. 

**Choosing the right approach**
<img width="2480" alt="image" src="https://user-images.githubusercontent.com/2437758/182436055-7f8c8e62-e997-42c9-b561-da094746a1fe.png">

### Lab
You create a deployment by, first, having a yaml file. An example is `nginx-deployment.yaml`
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
  labels:
    app: nginx
spec:
  replicas: 3
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:1.7.9
        ports:
        - containerPort: 80
```

Now you can use kubectl to deploy with 
```sh
kubectl apply -f ./nginx-deployment.yaml
# later...
kubectl get deployments
# scale up with 
kubectl scale --replicas=10 deployment nginx-deployment
# later, scale down
kubectl scale --replicas=3 deployment nginx-deployment
```

**Session Affinity**

If you are using a canary deployment, you can't ensure that the client will see the same Pod by default. If you want clients to visit the same pod on each subsequent request, use `sessionAffinity: ClientIP` in yaml file. 

## Pod Networking

- Volumes and persistent volumes
- PersistentVolumes are storage that is available to a Kubernetes cluster
- Persistent Volume Claims (PVCs). PersistentVolumeClaims enable Pods to access PersistentVolumes, so use PersistentVolumeClaims for any data that you expect to survive Pod scaling, updating, or migrating. Remember [what is a pod](https://cloud.google.com/kubernetes-engine/docs/concepts/pod#:~:text=Pods%20are%20the%20smallest%2C%20most,and%20share%20the%20Pod's%20resources.).
- Creating a manifest for persistence

### Create and apply a manifest with a PVC
Most of the time, you don't need to directly configure PV objects or create Compute Engine persistent disks. Instead, you can create a PVC, and Kubernetes automatically provisions a persistent disk for you.

**My note** In the lab, you create a PVC using a manifest yaml file and you create a pod using a different yaml file that specifies the PVC, as in 
```sh
# PVC yaml (just a portion of it)
kind: PersistentVolumeClaim
metadata:
  name: hello-web-disk

# Pod yaml
kind: Pod
volumes:
    - name: pvc-demo-volume
      persistentVolumeClaim:
        claimName: hello-web-disk
```

Once you make a yaml file (your manifest), apply it with `kubectl apply -f pvc-demo.yaml`

Start shell access to your pod: `kubectl exec -it pvc-demo-pod -- sh`

