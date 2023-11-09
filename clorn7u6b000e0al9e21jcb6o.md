---
title: "Apiwiz Assignment"
datePublished: Thu Nov 09 2023 20:30:05 GMT+0000 (Coordinated Universal Time)
cuid: clorn7u6b000e0al9e21jcb6o
slug: apiwiz-assignment

---

---

Linux:

1. Provide steps to create a directory inside a directory where the parent directory does not exist.
    
    ```bash
    mkdir -p parent-dir/child-dir
    ```
    
2. How to install a package on a Linux server when there is no internet connection?
    
    Ans - If you need to install a package on a Linux server without an internet connection, you can use a package file that you've downloaded manually from the internet using another computer. The package file will usually have a `.deb` extension for Debian-based distributions (e.g., Ubuntu) or a `.rpm` extension for Red Hat-based distributions (e.g., CentOS).
    
    Here are the steps for each package type:
    
    * For `.deb` packages (Debian/Ubuntu):
        
        1. Copy the `.deb` package file to the Linux server using a USB drive or other transfer method.
            
        2. Open a terminal on the Linux server.
            
        3. Navigate to the directory where you've copied the `.deb` package file.
            
        4. Install the package using the `dpkg` command. For example, if the package file is called `package.deb`, you can install it using the following command:
            
    
    ```bash
    sudo dpkg -i package.deb
    ```
    
    * For `.rpm` packages (Red Hat/CentOS):
        
        1. Copy the `.rpm` package file to the Linux server using a USB drive or other transfer method.
            
        2. Open a terminal on the Linux server.
            
        3. Navigate to the directory where you've copied the `.rpm` package file.
            
        4. Install the package using the `rpm` command. For example, if the package file is called `package.rpm`, you can install it using the following command:
            
    
    ```bash
    sudo rpm -i package.rpm
    ```
    
3. How to access specific folders of Server A from Server B and Server C?
    
    Ans -
    
    To access specific folders of Server A from Server B and Server C, you can set up file sharing using a protocol such as NFS (Network File System).
    
    On Server A (the NFS server):
    
    1. Install the NFS server package:
        
        ```bash
        sudo apt-get install nfs-kernel-server   # Debian/Ubuntu
        sudo yum install nfs-utils               # Red Hat/CentOS
        ```
        
    2. Create the folder you want to share (e.g., `/srv/share`):
        
        ```bash
        sudo mkdir /srv/share
        ```
        
    3. Add an entry to the `/etc/exports` file to share the folder with Server B and Server C. For example, if the IP addresses of Server B and Server C are `192.168.1.2` and `192.168.1.3`, respectively, you can add the following line to `/etc/exports`:
        
        ```bash
        /srv/share 192.168.1.2(rw,sync,no_subtree_check) 192.168.1.3(rw,sync,no_subtree_check)
        ```
        
    4. Restart the NFS server:
        
        ```bash
        sudo systemctl restart nfs-kernel-server
        ```
        
        On Server B and Server C (the NFS clients):
        
    5. Install the NFS client package:
        
        ```bash
        sudo apt-get install nfs-common   # Debian/Ubuntu
        sudo yum install nfs-utils        # Red Hat/CentOS
        ```
        
    6. Create a mount point for the shared folder (e.g., `/mnt/share`):
        
        ```bash
        sudo mkdir /mnt/share
        ```
        
    7. Mount the shared folder from Server A:
        
        ```bash
        sudo mount 192.168.1.1:/srv/share /mnt/share
        ```
        
        Replace `192.168.1.1` with the IP address of Server A.
        
    
    Now, Server B and Server C should be able to access the shared folder from Server A at the `/mnt/share` mount point.
    
4. How to check all the running processes from a server?
    
    Ans -
    
    To check all the running processes on a server, you can use the `ps` command. The most commonly used option is `ps aux`, which displays detailed information about all the running processes on the system. Here's an example of how to use the `ps` command:
    
    ```bash
    ps aux
    ```
    
    The output will show a list of all running processes, along with information such as the process ID (PID), user, CPU usage, memory usage, and the command that started the process.
    
5. Provide the command to delete all the files older than X days inside a specific directory.
    
    Ans -
    
    To delete all files older than X days inside a specific directory, you can use the `find` command in combination with the `xargs` command and the `rm` command. Here's an example of how to use these commands:
    
    ```bash
    find /path/to/directory -type f -mtime +X -print0 | xargs -0 rm
    ```
    
    * In this command, replace `/path/to/directory` with the path to the directory where you want to delete the files and replace `X` with the number of days.
        
    * The `-type f` option tells the `find` command to search for files.
        
    * The `-mtime +X` option tells the `find` command to match files modified more than X days ago and the `-print0` and `-0` options tell the `find`.
        
    * The `xargs` commands to handle filenames with special characters (such as spaces or newlines).
        
6. Create a shell script to identify the process ID
    
    a. script should as a user input for the process ID
    
    b. If the process exists script should print the process ID and exit
    
    c. If the process doesn't exist script should print the process doesn't exist and ask for another input
    
    Ans -
    
    ```bash
    #!/bin/bash
    
    while true; do
      # Prompt the user to enter a process ID
      echo "Enter a process ID:"
      read process_id
    
      # Check if the process ID exists
      if ps -p $process_id > /dev/null; then
        # If the process ID exists, print the process ID and exit the loop
        echo "Process $process_id exists"
        exit 0
      else
        # If the process ID doesn't exist, print a message and prompt the user for another input
        echo "Process $process_id doesn't exist"
      fi
    done
    ```
    

---

Docker:

1. What is docker and why do we need it?
    
    Ans -
    
    Docker is an open-source platform that makes applications easy to develop, ship, deploy and run inside containers. A container is a lightweight, stand-alone, executable package that includes everything needed to run a piece of software, including the code, runtime, system libraries, and dependencies. Containers provide a consistent and standardized environment for applications, ensuring that they run the same way on any system, regardless of the underlying infrastructure.
    
    Each virtual machine requires its own full operating system, which consumes additional resources and increases startup times. In addition, managing and maintaining multiple virtual machines can be complex and time-consuming. Docker was created as an alternative to virtualization that addresses some of these challenges. Docker uses container technology, and containers share the host system's kernel and resources, making them more efficient and lightweight compared to virtual machines. Docker is ideal for scenarios where a microservice architecture is implemented.
    
2. Write a docker file for a sample Java/python application.
    
    Ans -
    
    Here's the file structure where the source code exists.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699167295210/a8111360-8e30-4df4-b978-63b61bd2d28d.png align="center")
    
    Here's a simple example of a Dockerfile for a Java application using the SpringBoot framework:
    
    ```dockerfile
    # Use the official OpenJDK base image
    FROM openjdk:8-jdk-alpine
    
    # Set the working directory inside the container
    WORKDIR app/
    
    # Copy the JAR file into the container
    COPY target/my-app.jar my-app.jar
    
    # Expose the port that the application runs on
    EXPOSE 8080
    
    # Start the application
    CMD ["java", "-jar", "my-app.jar"]
    ```
    
    Here's a Dockerfile for a Python application using the Flask framework:
    
    This is a part of my **Flask-Todo-CICD** Project using Jenkins:
    
    **Repository**: [https://github.com/Varunmargam/2-tier-flask-todo-cicd](https://github.com/Varunmargam/2-tier-flask-todo-cicd)
    
    **Blog**: [https://varunmargam.hashnode.dev/cicd-pipeline-for-2-tier-flask-todo-web-application](https://varunmargam.hashnode.dev/cicd-pipeline-for-2-tier-flask-todo-web-application)
    
    ```dockerfile
    # Use an official Python runtime as the base image
    FROM python:3.9-slim
    
    RUN apt-get update \
        && apt-get upgrade -y \
        && apt-get install -y gcc default-libmysqlclient-dev pkg-config \
        && rm -rf /var/lib/apt/lists/*
    
    # Set the working directory in the container
    WORKDIR /app
    
    # Copy all the files into the container
    COPY . .
    
    # Install app dependencies
    RUN pip install --upgrade pip \
        && pip install mysqlclient \
        && pip install -r requirements.txt
    
    # Specify the command to run your application
    CMD ["python", "app.py"]
    ```
    
3. What is the docker lifecycle?
    
    Ans -
    
    The Docker lifecycle starts by pulling the image from the Registry or by creating a Dockerfile to build a Docker image and then pushing it to the registry. Running the Docker image i.e. to create a container running the application. Then performing operations on the container till it is deleted.
    
    The Docker lifecycle consists of several stages:
    
    * **Build**: The Dockerfile is used to build a Docker image. The Docker image is a snapshot of the application and its dependencies.
        
    * **Run**: The Docker image is used to run a Docker container. The container is a running instance of the image.
        
    * **Stop**: The Docker container can be stopped, which halts the execution of the application.
        
    * **Start**: The Docker container can be started again, resuming the execution of the application.
        
    * **Remove**: The Docker container can be removed, which deletes the container and frees up resources on the host.
        
4. What is the difference between an image and a container?
    
    Ans -
    
    1. **Docker Image:** A Docker image is a lightweight, standalone, and executable software package that contains everything needed to run a piece of software, including code, runtime, libraries, and dependencies. Images are built from Dockerfiles and serve as blueprints for creating Docker containers.
        
    2. **Docker Container:** A Docker container is a runnable instance of a Docker image. It encapsulates the application and its runtime environment, providing isolation from the host system and other containers. Containers can be started, stopped, and managed independently. They are ephemeral and designed to be disposable and replaceable.
        
5. How to check docker container logs? Provide the command for the same.
    
    Ans -
    
    To check the logs of a Docker container, you can use the `docker logs` command followed by the container ID or name.
    
    ```bash
    docker logs <container_id or container_name>
    docker logs -f <container_id or container_name> # -f option to see logs in real-time
    ```
    

---

Kubernetes:

1. What are the different types of services?
    
    Ans -
    
    Kubernetes services are abstractions that define a logical set of pods and a policy by which to access them. There are several types of services in Kubernetes:
    
    * **ClusterIP**: Exposes the service on an internal IP in the cluster. This type makes the service reachable only within the cluster.
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699169384123/60f8cd92-4ada-47d2-a60e-6d834eda2105.png align="center")
        
    * **NodePort**: Exposes the service on each node's IP at a static port. This type makes the service reachable from outside the cluster.
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699169400711/08b3a446-9891-4b89-9373-1b9f4ff2fb85.png align="center")
        
    * **LoadBalancer**: Exposes the service externally using a cloud provider's load balancer.
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699169418840/8dce952f-5829-40c6-8b31-381d8cade2b6.png align="center")
        
    * **ExternalName**: Exposes the service using an arbitrary name by returning a CNAME record with the name.
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699169424924/419edebb-c497-4051-b0cd-b1e3aaed171e.png align="center")
        
2. What is a pod?
    
    Ans -
    
    A pod is the smallest deployable unit in K8s that contains typically one or more containers running inside. Containers within a pod share the same network namespace, which means they can communicate with each other using [`localhost`](http://localhost) and share the same storage volumes. A pod can be scheduled, automatically scaled, and automatically healed. If a pod goes down or is unavailable it can replicate to maintain the desired number of pods. All the components of the **K8s cluster** work to provide these features and run this smallest unit called pod running a containerized app. It can be used in production.
    
3. Create a pod with the above-created custom image when a pod dies k8s should automatically restart
    
    Ans -
    
    A Kubernetes pod created from a Pod Manifest file does not automatically restart if it fails or is terminated unless it is implemented via a Deployment Manifest file.
    
    Here's an example of a Kubernetes deployment manifest file that defines a pod using my custom Docker image:
    
    ```yaml
    apiVersion: apps/v1
    kind: Deployment
    metadata:
      name: todo-deployment
      namespace: django
      labels:
        app: todo-app
    spec:
      replicas: 1     # deployment will try to maintain this number of replicas
      selector:
        matchLabels:
          app: todo-app
      template:
        metadata:
          namespace: django
          labels:
            app: todo-app
        spec:
          containers:
          - name: todo-app
            image: trainwithshubham/django-todo:latest
            ports:
            - containerPort: 8000
    ```
    
    `Step 1`: Create a `deployment.yml` file and write the above YAML code.
    
    `Step 2`: Apply this `deployment.yml` file
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699189206705/304c31ce-6e6a-4fd2-ae7f-cd699fb4f897.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699189211119/20f4e187-4cdf-42c3-ac93-f02ab87d16cd.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699189265586/f091f2a8-e03a-4aa7-b30d-90cd923b0554.png align="center")
    
    `Step 3`: Delete the pod created and authenticate if another pod is created proving the auto-healing feature of Kubernetes.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699189281421/3dd574c2-c9ea-452d-a7d4-1f2ae2713434.png align="center")
    
    We can see as soon as the pod was deleted a new pod was immediately created by the deployment resource of K8s maintaining the `replicas: 1` as our desired state showing K8s auto-healing feature.
    
4. How to access the custom application with a specific port?
    
    Ans -
    
    You can access the above custom application at port 8000:
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699189399079/19a5dbcf-eb65-454e-b6fa-8586149ae787.png align="center")
    
    To access the custom application with a specific port example port 80, you can expose the pod using a service.
    
    Here's an example of a Kubernetes manifest file that defines a service to expose the pod on default port 80:
    
    ```yaml
    apiVersion: v1
    kind: Service
    metadata:
      name: todo-service
      namespace: django
    spec:
      selector:
        app: todo-app
      ports:
        - port: 80
          targetPort: 8000
    ```
    
    The service `todo-service` will listen at default port 80 and forward the traffic to port 8000 on the pods that have the label `app: my-app`. The `selector` field specifies the labels that the service should use to select the pods.
    
    After creating the service, you can access the application using the service's IP address `curl -L <clusterip>:80 or curl -L <clusterip>`.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699189599880/9762dda6-d65a-43d7-9705-2a9dce0e21d7.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699189607906/694e2467-8e03-449b-95b8-d9b412588c25.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699189616578/dd39017d-4496-473d-bf32-a768c1a648ba.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699189623237/664a3b99-a536-4dd1-b6ed-95d530732a31.png align="center")
    

---

CI/CD:

1. Set up a pipeline (Github actions/Gitlab runner/ Jenkins or any open source tool) to build, test, create a docker image, publish and deploy to k8s. Use the application present in this public repo [https://github.com/apiwizlabs/wizdesk](https://github.com/apiwizlabs/wizdesk).
    
    **Dockerfile for Frontend:**
    
    This file will be located inside the `wizdesk` directory.
    
    ```dockerfile
    # Use the official Node.js base image
    FROM node:16-alpine
    
    # Set the working directory inside the container
    WORKDIR /app
    
    # Copy the package.json and package-lock.json files into the container
    COPY package*.json ./
    
    # Install the dependencies
    RUN npm install
    
    # Copy the application code into the container
    COPY . .
    
    # Expose the port that the application runs on
    EXPOSE 3000
    
    # Start the application
    CMD ["npm", "start"]
    ```
    
    Dockerfile for Backend:
    
    This file will be located inside the `wizdesk/Server` directory.
    
    ```dockerfile
    # Use the official Node.js base image
    FROM node:16-alpine
    
    # Set the working directory inside the container
    WORKDIR /app
    
    # Copy the package.json and package-lock.json files into the container
    COPY package*.json ./
    
    # Install the dependencies
    RUN npm install
    
    # Copy the application code into the container
    COPY . .
    
    # Expose the port that the application runs on
    EXPOSE 3002
    
    # Start the application
    CMD ["node", "server.js"]
    ```
    
    Docker-composes file:
    
    This file will be located inside the `wizdesk` directory.
    
    ```dockerfile
    version: '3'
    
    services:
      frontend:
        build:
          context: .
          dockerfile: Dockerfile
        ports:
          - "3000:3000"
    
      backend:
        build:
          context: Server/
          dockerfile: Dockerfile
        ports:
          - "3002:3002"
        environment:
          - DB_URL=mongodb://mongo:27017/mydb
    
      mongo:
        image: mongo:latest
        ports:
          - "27017:27017"
        volumes:
          - mongo_data:/data/db
    
    volumes:
      mongo_data:
    ```
    
    CI/CD Jenkins file
    
    ```plaintext
    pipeline {
        agent any
    
        stages {
            stage("Clone") {
                steps {
                    git url: 'https://github.com/apiwizlabs/wizdesk.git', branch: 'main'
                }
            }
    
            stage('Build Frontend') {
                steps {
                    sh 'cd wizdesk && npm install'
                    sh 'cd wizdesk && npm run build'
                    sh 'cd wizdesk && docker build . -t apiwiz-frontend'
                }
            }
    
            stage('Build Backend') {
                steps {
                    sh 'cd wizdesk/Server && npm install'
                    sh 'cd wizdesk/Server && docker build . -t apiwiz-backend'
                }
            }
    
            stage('Test') {
                steps {
                    // Run the tests for the frontend
                    sh 'cd wizdesk && npm test'
    
                    // Run the tests for the backend
                    sh 'cd wizdesk/Server && npm test'
                }
            }
    
            stage("Push to Repository") {
                steps {
                    withCredentials([usernamePassword(credentialsId: "DockerHub", passwordVariable: "DockerHubPass", usernameVariable: "DockerHubUser")]) {
                        sh "docker login -u ${env.DockerHubUser} -p ${env.DockerHubPass}"
                        sh "docker tag apiwiz-frontend ${env.DockerHubUser}/apiwiz-frontend:${env.BUILD_NUMBER}"
                        sh "docker push ${env.DockerHubUser}/apiwiz-frontend:${env.BUILD_NUMBER}"
                        sh "docker tag apiwiz-backend ${env.DockerHubUser}/apiwiz-backend:${env.BUILD_NUMBER}"
                        sh "docker push ${env.DockerHubUser}/apiwiz-backend:${env.BUILD_NUMBER}"
                    }
                }
            }
    
            stage('Deploy') {
                steps {
                    // Deploy the MongoDB database and application to the Kubernetes cluster
                    script {
                        // Load the Kubernetes credentials
                        withCredentials([kubernetes(credentialsId: 'KubeconfigCredentials', variable: 'KUBECONFIG')]) {
                            // Deploy the MongoDB database and application using kubectl
                            sh "kubectl apply -f Kubernetes/deployment.yml"
                        }
                    }
                }
            }
        }
    }
    ```
    
    Kubernetes Deployment file:  
    This file will be located inside the `wizdesk` directory.
    
    ```yaml
    apiVersion: apps/v1
    kind: Deployment
    metadata:
      name: mongodb
    spec:
      replicas: 1
      selector:
        matchLabels:
          app: mongodb
      template:
        metadata:
          labels:
            app: mongodb
        spec:
          containers:
          - name: mongodb
            image: mongo:latest
            ports:
            - containerPort: 27017
    ---
    apiVersion: apps/v1
    kind: Deployment
    metadata:
      name: apiwiz-frontend
    spec:
      replicas: 2
      selector:
        matchLabels:
          app: apiwiz-frontend
      template:
        metadata:
          labels:
            app: apiwiz-frontend
        spec:
          containers:
          - name: frontend
            image: dockerhub-username/apiwiz-frontend:latest
            ports:
            - containerPort: 80
    ---
    apiVersion: apps/v1
    kind: Deployment
    metadata:
      name: apiwiz-backend
    spec:
      replicas: 2
      selector:
        matchLabels:
          app: apiwiz-backend
      template:
        metadata:
          labels:
            app: apiwiz-backend
        spec:
          containers:
          - name: backend
            image: dockerhub-username/apiwiz-backend:latest
            ports:
            - containerPort: 5000
            env:
              - name: DB_URL
                value: "mongodb://mongodb-service:27017/db-name"
    ---
    apiVersion: v1
    kind: Service
    metadata:
      name: mongodb-service
    spec:
      selector:
        app: mongodb
      ports:
        - protocol: TCP
          port: 27017
          targetPort: 27017
    ---
    apiVersion: v1
    kind: Service
    metadata:
      name: apiwiz-frontend-service
    spec:
      selector:
        app: apiwiz-frontend
      ports:
        - protocol: TCP
          port: 80
          targetPort: 80
    ---
    apiVersion: v1
    kind: Service
    metadata:
      name: apiwiz-backend-service
    spec:
      selector:
        app: apiwiz-backend
      ports:
        - protocol: TCP
          port: 5000
          targetPort: 5000
    ```
    
2. Automate to spin up a network and virtual machines. Install the Nginx package and start the service(any cloud)
    
    Ans - I will be using Terraform to provision infrastructure on AWS Cloud
    
    For this, I will create 4 files:
    
    `terraform.tf`
    
    ```plaintext
    provider "aws" {
      region = "us-east-1"
    }
    
    terraform {
      required_providers {
        aws = {
          source = "hashicorp/aws"
          version = "5.16.1"
        }
      }
    }
    ```
    
    `main.tf`
    
    ```plaintext
    resource "aws_key_pair" "key" {
      key_name   = "id_rsa"
      public_key = file("~/.ssh/id_rsa.pub")
    }
    
    resource "aws_default_vpc" "default_vpc" {}
    
    resource "aws_security_group" "allow_ssh" {
      name        = "allow_ssh"
      description = "Allow ssh inbound traffic"
      vpc_id      = aws_default_vpc.default_vpc.id
    
      ingress {
        description = "SSH from VPC"
        from_port   = 22
        to_port     = 22
        protocol    = "tcp"
        cidr_blocks = ["0.0.0.0/0"]
      }
    
      tags = {
        Name = "allow_ssh"
      }
    }
    
    resource "aws_instance" "my_ec2" {
      ami             = var.ami_id
      instance_type   = "t2.micro"
      key_name        = aws_key_pair.key.key_name
      vpc_security_group_ids = [aws_security_group.allow_ssh.id]
    
      user_data = <<-EOF
                  #!/bin/bash
                  apt update
                  apt install -y nginx
                  systemctl start nginx
                  EOF
    
      tags = var.tags
    }
    ```
    
    `variables.tf`
    
    ```plaintext
    variable "ami_id" {
      description = "this is ubuntu ami id"
      default     = "ami-053b0d53c279acc90"
    }
    
    variable "tags" {
      type = map(string)
      default = {
        "name" = "Varun's ec2"
      }
    }
    ```
    
    `output.tf`
    
    ```plaintext
    output "instance_ip" {
      value = aws_instance.my_ec2.public_ip
    }
    ```