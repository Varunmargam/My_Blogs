---
title: "Kubernetes Fundamentals: Features, Necessity, and Architectural Insights"
datePublished: Sun Aug 27 2023 18:30:00 GMT+0000 (Coordinated Universal Time)
cuid: cllv6y54q000209maavaw0svu
slug: kubernetes-fundamentals-features-necessity-and-architectural-insights
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1693245928110/8f5587a4-0d40-4885-982f-5e0c4917ee9f.png
tags: kubernetes, devops-journey, kubernetes-architecture, 90daysofdevops, day30

---

---

# 📍Introduction

Welcome to my Kubernetes blog series. In this introductory blog, we'll explore Kubernetes, its features, significance, and architecture. Our journey will also lead us to delve into the realms of monolithic and microservice architectures. Join me as we dive into the fascinating world of Kubernetes and embark on our container orchestration journey.🚀

---

# 📍Kubernetes

Kubernetes is an open-source container orchestration/management tool that automates container deployment, scaling, and load balancing of containerized applications. It was developed by Google in 2008 to manage their applications. It is written in GoLang and is popularly used in the industry to manage containerized applications.

**It provides great features**:

1. Container Orchestration ( clustering of any number of containers running on a different network. )
    
2. Auto Scaling ( Vertical & Horizontal )
    
3. Auto Healing
    
4. Configuration Management
    
5. Load balancing
    
6. Fault Tolerance ( Node/POD/Failure )
    
7. Rollback ( Going back to the previous version )
    

All the top Cloud Providers support Kubernetes. With all these features Kubernetes is ideal for managing a containerized microservice architecture. Let's see what is microservice application.

**Kubernetes** is also known as **K8s** since there are '8' letters between '**K**' and '**s**' in Kubernetes.

---

# 📍Monolithic & Microservice Architecture

There are two types of architecture for building applications:

1. **Monolithic architecture** (aka Stand alone machine)
    
2. **Microservice architecture**
    

## ✔Monolithic architecture

Monolithic means single therefore, monolithic architecture is a tightly coupled architecture where every service or functionality of an application is closely dependent on each other and is integrated into a single unit. Let's take an example of an e-commerce website with a monolithic architecture:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693216808278/191fbad2-4456-4c1b-a8e6-09bce39e86c4.png align="center")

In the above example, we can see an e-commerce app where all its services and functionalities like Sign-in, Checkout, Add to Cart, Customer Care, Payment, etc. are present in a single instance i.e. in a single server.

**Advantages:**

1. It is simple to deploy as the entire application is in a single instance.
    
2. Testing the application is simpler.
    
3. Communication between components is faster.
    

**Disadvantages:**

1. Single Point of Failure.
    
2. If I have to work on a single component (e.g.: Sign-in) the whole app needs to be taken down.
    
3. If the application grows then it can become complex to maintain with various services.
    

## ✔Microservice architecture

Microservice is a distributed loosely coupled architecture where each component or service is running on a different server. The microservice architecture of the above e-commerce app can be visualized like this:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693218852502/18fd06e5-43fc-4b41-b6ca-3cb00edeb50f.png align="center")

Here, each of the services is running a separate instance and is communicating with each other via the internet.

**Advantages:**

* Services can be scaled independently based on specific requirements, leading to better resource utilization.
    
* Failures in one service do not necessarily affect others, leading to more resilient applications.
    
* When working on a particular service or a feature we do not need to down the whole application.
    
* Different services can use different technology stacks, allowing teams to choose the best tools for each task.
    

**Disadvantages:**

* Developing and maintaining a distributed system is more complex and requires expertise
    
* Maintaining data consistency across services can be complex, especially in scenarios requiring transactions.
    
* Communication between services requires careful design and can lead to increased overhead.
    
* Inter-service communication introduces network latency, which can impact overall application performance.
    

Microservice architecture is used more frequently nowadays, and containerizing a microservice application means running all the services of the application in a separate container. Popularly Docker containers are used to deploy services and applications.

## ✔Why use Kubernetes❓

**Disadvantages of Docker containers and how Kubernetes overcomes them:**

* Docker doesn't automatically recover containers from node failures. Kubernetes can detect node failures and automatically reschedule affected containers to healthy nodes.
    
* Docker lacks built-in tools for the automatic scaling of containers, and K8s provide autoscaling of the containers.
    
* Docker alone doesn't provide native tools for health monitoring and automated container recovery. Kubernetes constantly monitors the health of containers and can automatically restart or replace unhealthy containers.
    
* Docker requires manual configuration for networking, storage, and resource allocation. Kubernetes uses declarative YAML files to define application configurations, making it easier to manage and version these configurations
    
* Docker doesn't inherently provide mechanisms for ensuring high availability and load distribution across nodes. Kubernetes manages container placement, rescheduling, and load distribution, enhancing reliability and availability.
    
* And many more...
    

All these features, make Kubernetes an ideal tool to use for containerized microservice applications.

---

# 📍Kubernetes Architecture

**Kubernetes Architecture** also called **Kubernetes Cluster** contains **8 major components**.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693220690145/b4546531-0641-4182-b4cf-1d6c8e3ed13a.png align="center")

A cluster is nothing but a group of servers therefore, to create a cluster we need at least **two servers**. In the above example, we have 2 servers/nodes forming a K8s cluster:

1. **Master Node** ( a.k.a **Control Plane** ): Controls the overall cluster. Contains 4 components:
    
    1. **Scheduler**
        
    2. **etcd**
        
    3. **Control Manager**
        
    4. **API Server**
        
2. **Node ( Worker node ):** Where actual work is executed like running containers as directed by the master node. Contains 2 components:
    
    1. **Kubelet**
        
    2. **Kube-proxy ( Service-proxy )**
        

Let's dive into u=this Kubernetes cluster and understand each component in detail.

---

# 📍K8s Architecture Components

## ✔Master Node

Also known as the **Control Plane** is responsible for managing and controlling the cluster's overall state and operations. The main components of the control plane are:

1. **API Server** ( **kube-api-server** ):
    
    * Front-end for the control plane.
        
    * Provides an interface for users, applications, and other components to interact with the Kubernetes cluster.
        
    * It serves as the entry point for executing commands, managing resources, creating and updating objects (such as pods, services, and deployments), and querying the state of the cluster.
        
2. **etcd:**
    
    * Similar to a database that is designed to store data in a simple key-value format.
        
    * `etcd` is specifically optimized for distributed environments and is used to maintain configuration data, metadata, and the current state of a cluster.
        
    * It ensures consistency, high availability, and reliability in a distributed environment
        
    * Data stored in `etcd` is persistent, meaning it is stored on disk and survives restarts or crashes.
        
    * Distributed across multiple nodes to ensure that data is replicated and available even if some nodes fail.
        
3. **Scheduler** ( **kube-scheduler** ):
    
    * When users request the creation and management of Pods, Kube-scheduler is going to take action on these requests.
        
    * Handles POD creation and management.
        
    * Responsible for assigning workloads (such as pods) to worker nodes within the cluster.
        
    * Optimizes resource utilization, maintains load balance, and ensures that pods are placed on appropriate nodes based on their resource requirements and constraints.
        
    * Plays a role in enabling and supporting certain aspects of auto-scaling.
        
4. **Controller-Manager**:
    
    * Ensures that the desired state of objects in the cluster matches the actual state.
        
    * If K8s is on the **cloud**, then it will be a **cloud-controller-manager**, for **non-cloud** it will be a **kube-controller-manager**.
        
    * Different controllers manage various resources like nodes, pods, services, and more:
        
        * **Node Controller:** Ensures the correct number of nodes are running.
            
        * **Replication Controller:** Maintains the desired number of replicas for a set of pods.
            
        * **Pods Lifecycle Controller:** Monitors and maintains the lifecycle of individual pods.
            
        * **Endpoints Controller:** Populates the Endpoints object (record of IP addresses and ports) for services.
            
        * **Service Account & Token Controllers:** Create default accounts and API access tokens for pods.
            
        * **Namespace Controller:** Ensures that namespaces are correctly configured and maintained.
            
        * **Volume Controller:** Manages the lifecycle of volumes used by pods.
            
        * **Service Controller:** Responsible for maintaining the services in a consistent state.
            

## ✔Node ( Worker node )

Nodes are machines in the cluster responsible for running containers and executing workloads. Each worker node has the following 3 components:

1. **Kubelet:**
    
    * An agent that runs on each node and interacts with the control plane ( API-server ).
        
    * Ensures containers are running inside pods and that the nodes are functioning properly.
        
2. **Container Engine** ( **Runtime** ):
    
    * Software that runs containers, such as Docker.
        
    * Works with Kubelet.
        
    * It's responsible for creating and managing container instances.
        
3. **Kube-Proxy** ( **service-proxy** ):
    
    * Maintains network rules for communication between pods and provides load balancing for service traffic.
        
    * Assign IP to each pod. ( dynamic )
        
    * It runs on each pod, ensuring each pod will get its unique IP Address.
        
4. **Pod**:
    
    * A pod is the smallest deployable unit in Kubernetes.
        
    * It is a part of the worker node you can see in the diagram represented with orange boxes.
        
    * It represents a single instance of a running process in a cluster.
        
    * A pod can contain one ( typically ) or more containers that share the same network namespace, IP address, and storage.
        

## ✔Kubectl

* Kubectl is the command-line tool used to interact with Kubernetes clusters.
    
* It acts as a client to the Kubernetes API server and allows users to manage various aspects of the cluster.
    
* Some common `kubectl` commands include creating and deleting resources, checking cluster status, scaling applications, and more.
    

Let's do a hands-on and implement the Kubernetes architecture. Kubernetes Cluster can be set up using:

**Local**:

1. **MiniKube**
    

**Production**:

1. **Kubeadm ( Bare Metal )**
    
2. **EKS** ( **Elastic Kubernetes Service** \[**AWS\]** )
    
3. **AKS** ( **Azure Kubernetes Service** )
    
4. **GKE** ( **Google Kubernetes Engine** )
    

Visit this GitHub URL: [https://github.com/LondheShubham153/kubestarter](https://github.com/LondheShubham153/kubestarter)

Start your Kubernetes journey by forking this GitHub URL.

---

# 📍MiniKube Setup

It is a Local Setup you can use it for practicing Kubernetes. Minikube runs on a single server and creates a **virtual** Kubernetes cluster using **containers**. It runs a Kubernetes Cluster inside a container that contains the components kube-scheduler, etcd, kubelet, etc. each service running inside a container. You can visualize it as many containers running inside a big container.

## ✔EC2 instance Setup

`Step 1`: Launch an EC2 instance

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693242559617/3bfd04f3-cc31-4bad-a404-dc0b1f008533.png align="center")

`Step 2`: Name it as '**minikube-server**'

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693242603903/d439babc-fd96-4c7d-aad6-c69a4b5ea41b.png align="center")

`Step 3`: Select '**Ubuntu**' AMI

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693242646859/09efadca-766e-492a-9f5c-29c969c36c6f.png align="center")

`Step 4`: Select instance type '**t2.medium**'

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693242676412/fe16605d-1f1a-4a82-acdf-5fe008592043.png align="center")

`Step 5`: Click on '**Create a new key pair**'

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693242706686/00483b9d-4733-4244-a946-3f12443325d4.png align="center")

`Step 6`: Name your key-pair '**minikube-key**' or any name you like and **click** on '**Create key pair**'

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693242746258/a0572466-fca1-494c-b448-e46bea84edd5.png align="center")

`Step 7`: Click on '**Launch instance**'

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693242773515/d951aee7-51e8-4000-9785-a6566c761135.png align="center")

`Step 8`: If you see this, then your EC2 instance has been successfully created, you can **click** on '**Instances**' and see your instance.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693242808804/b4de3dce-60fc-44af-8bf4-32db48d133d3.png align="center")

`Step 9`: Wait for some time to start the instance till shows '**Running**'.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693242840876/ec53626a-1e1e-4f86-b248-456579565fa5.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693242873712/051ebf71-9383-49a1-8409-b7adce3c9ab6.png align="center")

`Step 10`: Select your instance and click on the '**Connect**' option at the top right.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693242929208/95b4b984-82ba-4120-8481-64acfe3c1f53.png align="center")

`Step 11`: Select the '**SSH client**' option and follow the steps mentioned.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693243011264/6d92d1f1-99df-4c67-99da-1b04279ee26d.png align="center")

`Step 12`: Open your **Terminal** for **Linux** and **Mac**, and open '**GitBash**' for '**Windows**'. Go to your '**Downloads**' using `cd Downloads` folder where the **private key file** is usually located.

Verify it using this command in the '**Downloads**' folder: `ls | grep -i minikube`

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693243059934/e1c348b4-f51b-49e6-a35e-62b77b51b2f2.png align="center")

We have to change the permission to only read for the owner.

`Step 13`: Copy the `chmod` command and paste it into your terminal

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693243123792/34c827a0-05e9-4b38-be2a-29cdb4e9d200.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693243182220/45e3519d-d264-4ec5-ac3c-cd2ba791513c.png align="center")

`Step 14`: Copy the `ssh` command and paste it into your terminal

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693243249389/89e49652-3e4e-4ac4-9f14-abc1596c76f8.png align="center")

Type '**yes**' for the prompt:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693243282831/0d03d091-cb65-42c2-b34d-aca29a4b30a0.png align="center")

And you will be connected to your EC2 instance:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693243386797/43111916-3ea5-43d3-a469-253a71a7574b.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693243440014/d7acf855-cb9e-4e4c-a5e7-6d9d94eb6fe1.png align="center")

Now go to this GitHub URL [Kuberstarter](https://github.com/LondheShubham153/kubestarter) and follow the instructions to install and set up **MiniKube.**

After setting up the Minikube type the command `docker ps` you will see one container is running on your instance:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693243506275/0db9e597-925e-4375-b893-246057b29ed1.png align="center")

Using the `kubectl get nodes` command you can see a 'control-plane' server is running:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693243576141/fe733a53-c7b8-4c75-85ef-937c7fc978d7.png align="center")

This is the container that is running a virtual Kubernetes cluster with its components running inside a container. To see that type the command `minikube ssh` to enter this running container and then execute the `docker ps` command.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693243658624/ad7ecd46-ab4f-47b3-9f93-d85d1a789b14.png align="center")

You can see all the components of the Kubernetes cluster are running inside the containers.

📝**Note**: Make sure you terminate this instance within 1 hour since '**t2.medium**' is not under the free tier and cost charges on an hourly basis.🖊

---

# 📍Kubeadm Setup

This is used in production, and for this, we need to set up AWS Instances:

1. **kubernetes-master**
    
2. **kubernetes-node**
    

`Step 1`: **Click** on '**Launch Instance**' and give the name as '**kubernetes-master**' and on the right-hand side in the '**Number of Instances**' type '**2**'.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693243722234/54a8d047-ac80-42af-b714-2ea513482963.png align="center")

`Step 2`: Select '**Ubuntu**' AMI and instance type '**t2.medium**'.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693243782166/e54f9257-0c4d-44a2-a654-c0c9e6a67118.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693243789419/2cf98df2-0259-4a85-a605-73cb7584179b.png align="center")

`Step 3`: Select the '**minikube-key**' key pair we created while creating minikube instance.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693243829620/67c55520-3d29-4198-9438-7fd5aade5163.png align="center")

`Step 4`: Click on '**Launch instance**'

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693243863322/5caa3fdc-f8a5-4278-89c7-7cc2aaef9e21.png align="center")

`Step 5`: Click on each '**instance id**' and that particular instance will be opened in two separate types.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693243899391/89626338-0026-4815-815b-4137a0cf0614.png align="center")

`Step 6`: Rename one of the instances as '**kubernetes-node**'. This is our worker node.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693243931080/8e4394dc-813d-49e6-9a34-a463a1db6af7.png align="center")

So now we have a **master instance** which will contain **four** components and a **node instance** that will contain **two** components:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693243989948/f4439391-e124-4db7-b570-0fc0cae421f8.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693243994856/2fa67fa5-0d9d-4f45-8516-74c7918ebfda.png align="center")

`Step 7`: Now connect these two instances using the **SSH client** as we saw in the Minikube setup section in two separate GitBash terminals. Keep it side by side.

Since they are both similar we will modify it to identify which is the master node and the worker node.

Go to your Master instance terminal and do the following steps:

`Step 1`: Click on the '**GitBash'** icon on the **control** **bar** of the GitBash terminal. You will see a window like this:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693244087862/f6b18059-2ba3-4aba-95a6-9ceb8c609b6f.png align="center")

`Step 2`: Click on '**Options**' and you will see this window:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693244124563/0e4dda68-77ef-45ac-ae45-971ee8c8b90c.png align="center")

`Step 3`: Select '**Foreground**' in the **Colours** section, select '**Red**' color and click '**OK**'

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693244158945/1c16af9b-a1d6-48df-9bce-3d729764735f.png align="center")

`Step 4`: Click on '**Apply**'. You will the text is now in '**Red**'.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693244207535/7e6b1302-8378-4ecf-aceb-b963033ef575.png align="center")

Do similar steps to your **worker node** terminal with the '**Blue**' color. Now, you can identify your **master** instance and **node** instance with '**Red**' and '**Blue**' colors respectively. Like this:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693244279260/7bb5ee57-cd25-411f-a7a6-f23028d3d433.png align="center")

Now, follow the Kubeadm installation steps in this GitHub URL [Kuberstarter](https://github.com/LondheShubham153/kubestarter)

📝**Note**: Make sure you terminate this instance within 1 hour since '**t2.medium**' is not under the free tier and cost charges on an hourly basis.🖊

---

# 📍Conclusion

Thank you for reading this blog! 📖 Hope you have gained some value. In the future blog, we will be launching a Kubernetes cluster with nginx running on it. Until then get more familiarized with the Kubernetes cluster. If you want to practice Kubernetes make sure you do it on minikube or at [killercoda.com](https://killercoda.com/) where you get K8s playground for free.

If you enjoyed this blog and found it helpful, please give it a like 👍, share it with your friends, share your thoughts, and give me some valuable feedback.😇 Don't forget to follow me for more such blogs! 🌟

---

# 📍Reference

* [Monolithic Architecture Image](https://in.images.search.yahoo.com/search/images;_ylt=AwrKC0JMbexkIicMwBK9HAx.;_ylu=c2VjA3NlYXJjaARzbGsDYnV0dG9u;_ylc=X1MDMjExNDcyMzAwNQRfcgMyBGZyA21jYWZlZQRmcjIDcDpzLHY6aSxtOnNiLXRvcARncHJpZANJM2xGbHlFQlJYR1duYmhXQlEuSk1BBG5fcnNsdAMwBG5fc3VnZwMxBG9yaWdpbgNpbi5pbWFnZXMuc2VhcmNoLnlhaG9vLmNvbQRwb3MDMARwcXN0cgMEcHFzdHJsAzAEcXN0cmwDMjUEcXVlcnkDbW9ub2xpdGhpYyUyMGUtY29tbWVyY2UlMjBhcHAEdF9zdG1wAzE2OTMyMTYyOTQ-?p=monolithic+e-commerce+app&fr=mcafee&fr2=p%3As%2Cv%3Ai%2Cm%3Asb-top&ei=UTF-8&x=wrt&type=E211IN826G0#id=10&iurl=https%3A%2F%2Fd1jnx9ba8s6j9r.cloudfront.net%2Fblog%2Fwp-content%2Fuploads%2F2018%2F02%2FMonolithic-Framework-Usecase-What-Is-Microservices-Edureka.png&action=click)
    

---