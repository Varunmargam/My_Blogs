---
title: "Understanding Docker:  The Power of Containerization"
datePublished: Fri Aug 04 2023 04:17:46 GMT+0000 (Coordinated Universal Time)
cuid: clkw2rt15000909mb2a3l8ocm
slug: understanding-docker-the-power-of-containerization
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1691122232088/4241270b-7ed1-4bd4-9e40-05035a67be6d.png
tags: docker, containerization, devops-journey, 90daysofdevops, day16

---

---

# 📍Introduction

Welcome to my Docker series blog, where in this blog we will be understanding what is Docker, why it is used, etc. As a DevOps Engineer having Docker knowledge is very important as it is a modern IT practice for software development.

Let's just dive into this Docker tool and get introduced to the world of containers.

---

# 📍Operating System

The Operating System is nothing but an interface between you and your computer hardware. It allows you to perform various tasks such as running applications, creating a file or a folder, etc. by the hardware to execute these tasks. It has 2 major components:

* **User Interface**: It is the graphical representation of your OS. It allows the user to have a user-friendly environment where they can perform various tasks and run applications. The GUI of Ubuntu Linux looks something like this:
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691120714013/03787c36-5806-4a28-ac85-59f312cbceaf.png align="center")
    
* **Kernel**: It is the heart or brain of the OS. It communicates with the computer hardware to perform the user tasks and does memory management, reading I/O (input/output) devices, process, and resource management.
    

OS is seen everywhere in computers: Windows, Linux, MacOS; in smartphones: Android and IOS; etc.

---

# 📍Virtualization

Virtualization is like having a "computer inside a computer." It involves creating a Virtual Machine (VM) on a physical computer by virtualizing its hardware. This means creating a Virtual RAM, CPU, and Hard Disk by sharing the same physical hardware and maintaining isolation. To make this work, we need hardware resources like RAM, CPU, and Hard Disk, along with an OS that can manage these resources. The OS on the VM can be different from the one on the host computer. To enable this process, we use software called a "Hypervisor."

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691096472999/df5c63ba-9e57-4a5a-84f2-456170b40a6d.png align="center")

**Hypervisor** is a software that sits on top of the **Hardware/Infrastructure** and allows us to create VMs on top of it by allocating some hardware resources for the VM so that OS can be installed and these resources can be managed for the applications to run and perform operations creating a virtual environment similar to a physical computer.

Before Docker was introduced we used VMs to deploy Microservice applications. If you want to know about microservices or microservice architecture read this article by RedHat: [What are Microservices?](https://www.redhat.com/en/topics/microservices/what-are-microservices)

---

# 📍Docker

Docker is a tool and an open platform used for developing, shipping (transferring), deploying, and running applications. Docker makes the application isolated or independent from the infrastructure so that it can run on any machine. It achieves this by storing an application inside a container along with all the dependencies it needs for the application to run smoothly. Using this Docker methodology in Software Development Life Cycle where at every stage the application needs to be running, we can significantly reduce the time writing the code and running in the production. Since all the dependencies required to run the application are inside the container.

By doing this Docker solves the renowned problem "**It works on my computer but does not work on your computer!**"

Let's take a scenario as an example that will help you understand what is Docker and why was it needed.

---

# 📍Scenario

We will take a look at how projects were deployed using virtualization and using Docker.

Let's take a simple web application as our project as an example to understand Docker and compare it with a scenario where the same project is developed using multiple Virtual Machines.

**Project: Web Application**

We are building a simple web application that consists of:

* **FrontEnd**: HTML, CSS, JavaScript
    
* **Backend**: Nodejs
    
* **Database**: MySQL
    

**Using Multiple VMs:**

We would set up three separate virtual machines, each hosting one component of the web application: frontend, backend, and the database.

1. **Frontend VM:** This VM would run the web frontend code along with all the required dependencies.
    
2. **Backend VM:** This VM would host the Node.js server code and its dependencies.
    
3. **Database VM:** This VM would run the MySQL database.
    

**Challenges with Multiple VMs:**

* **Resource Overhead**: Each VM requires a full operating system, leading to more resources and VM takes time to boot.
    
* **Scalability**: To make our website run in production we would have to provide High availability meaning multiple VMs for frontend, backend, and database to ensure if any of the VM stops running then another VM can be initiated.
    
* **Time**: As VM has its OS it takes time to boot and start and run the service. In the case of multiple VM, the time lag can be large and can decrease the engagement of the users.
    
* **Configuration Management**: Managing and synchronizing the configurations and dependencies across multiple VMs can be more complex. At every stage, we would have to repeat this process.
    

Now, let's understand Docker a bit more and then continue with this same scenario but using Docker.

---

# 📍Docker Components

1. **Docker Image**: A Docker Image is like a Screenshot of an application where it contains all the necessary dependencies, libraries, code, and files to run the application. It can run the application with a single command and can be easily shared and run on any computer that has Docker. It is a lightweight portable package. Docker images are the blueprints for creating Docker containers. A docker image is a repository in a Registry.
    
2. **Docker Container**: It is a box that provides an isolated executable environment for Docker images to run. It is a lightweight environment created from the running instance of the Docker image. When you run a Docker container, it becomes an active process with its own isolated filesystem, network, and process space. Containers leverage the host operating system's kernel, making them faster and more efficient compared to traditional virtual machines.
    
3. **Docker Engine**: It is the core of the Docker. It is the software that creates, runs, and manages the containers in your computer or server. It consists of 2 main parts:
    
    * **Docker Daemon**: Just like a daemon that constantly runs in the background and executes all the related processes or subprocesses to carry out a task and ensures smooth execution.
        
        The Docker daemon is a background service that runs on the host machine. It manages all the containers and communicates with the host's operating system to allocate resources, manage networking, and handle storage. The Docker daemon is responsible for creating, starting, stopping, and deleting containers based on the commands you give through the Docker CLI (Command Line Interface) or other Docker tools.
        
    * **Docker CLI**: It is a command-line tool that allows users to interact with the Docker daemon and perform various operations on containers and images. You can use the Docker CLI to pull Docker images from Docker Hub Registry, create and manage containers, check their status, and more.
        
4. **Docker Hub (Registry)**: It is like a huge online store in the cloud where you can find Docker images. You can also share your Docker images by uploading them to Docker Hub using a simple Docker command. It is a huge library and community of Docker images. Docker Hub is the **default** **registry,** if Docker cannot find an image locally it downloads it from the Docker Hub.
    
5. **Dockerfile**: It is a simple text file that contains a set of instructions on what the image should look like and the steps required to set up the application.
    
6. **Docker Compose**: It's a tool that helps you manage and run multiple containers together as a group and containers to work together smoothly
    

---

# 📍Scenario (Continued..)

In the Docker scenario, we would use Docker containers to isolate each component of the web application: frontend, backend, and database. We'll have three Docker containers:

1. **Frontend Container:** This container holds all the files for the web Frontend, including HTML, CSS, and JavaScript.
    
2. **Backend Container:** This container contains the Node.js server code that handles requests from the Frontend and interacts with the database.
    
3. **Database Container:** This container runs the MySQL database that stores the application's data.
    

Docker allows us to package each component along with its dependencies, libraries, and settings into separate containers.

**Advantages of Docker:**

* Easy to manage: We can easily start, stop, and scale individual components using simple Docker commands.
    
* Lightweight: Containers share the host OS kernel, so they consume fewer resources compared to VMs.
    
* Portability: The entire application, along with its dependencies, can be easily moved between different environments using the same Docker configuration.
    

---

# 📍Docker vs Virtualization

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691108830993/a29c4925-d5dd-43bd-9604-2552f669d8cc.webp align="center")

* **Hypervisor** sits on top of the infrastructure and allows to create VMs with their OS called Guest OS.
    
* **Docker** Engine uses the Host OS for its operations and helps you run and manage the containers. Since they have no OS they are lightweight processes and take less time to boot therefore, we can run more containers.
    
* **Virtualization** is a Hardware virtualization since you get virtual RAM, virtual CPU, virtual Hardware, etc so you can install an OS to create a Virtual Machine.
    
* Since processes need OS to run **Docker** creates an illusion of having an OS inside the container for the process to run. Therefore, containerization is OS Virtualization.
    

There are many Container Engines, eg: Podman, Garden, OpenVZ, LXC (Linux Containers), and Docker. Docker is the most popular one.

---

# 📍Docker Commands

To install Docker Engine on your system follow this documentation: [Docker Engine Installation](https://docs.docker.com/engine/install/)

Start your first Docker Container using the command `docker run`:

1. `docker run hello-world` (for normal users): This will very the Docker installation. It will run the image and if the image is not present locally then it will download it from Docker Hub Registry and then run it.
    
    It will also give a prompt on what steps did it take to generate this message if you have followed through and understood the blog you will understand the steps very well.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691115685231/0ee03ae6-94fc-4113-a437-a714e84399d0.png align="center")
    
2. `docker inspect <image>`: Gives detailed information about a container or image.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691115723075/47ddc73f-775e-4cde-88fa-a1e30da9b367.png align="center")
    
3. `sudo systemctl status docker`: Docker is a service/software you can check the status of docker using the `systemctl` command.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691115731209/18080afd-f47f-442e-a2fb-de3ae5184574.png align="center")
    
4. `docker pull <image>`: Pulls i.e. downloads the Docker image from the Docker Hub Registry to the local system.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691117374087/fc4dabbb-325d-4563-becc-e6e9578d0628.png align="center")
    
5. `docker images`: Lists the images locally
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691117707734/611e55aa-eee2-484e-a8e4-1b9ae5be342e.png align="center")
    
6. `docker ps`: Lists all the running containers
    
7. `docker ps -a`: Lists all the containers running and stopped.
    

---

# 📍Conclusion

Thank you for reading this blog! 📖 Hope you have gained some value.

If you enjoyed this blog and found it helpful, please give it a like 👍, share it with your friends, do share your thoughts, and give me some valuable feedback.😇 Don't forget to follow me for more such blogs! 🌟

---

# 📍References

* [Docker Documentation](https://docs.docker.com/)
    
* [Google](http://www.google.com)
    

---