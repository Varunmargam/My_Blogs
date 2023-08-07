---
title: "Mastering Docker: Containerize Your Application with Dockerfile, Docker Image, and Containers"
datePublished: Mon Aug 07 2023 11:16:39 GMT+0000 (Coordinated Universal Time)
cuid: cll0s214k000q09mgc4vjccg3
slug: mastering-docker-containerize-your-application-with-dockerfile-docker-image-and-containers
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1691406160119/7807d1aa-ad4c-488e-8ec1-1a8965da7225.png
tags: docker, containerization, devops-journey, 90daysofdevops, day17

---

---

# 📍Introduction

Welcome to my Docker blog series! Here, we'll explore the entire process, from creating a Dockerfile for your program to successfully running it within a container. We will create a Docker project by containerizing a Nodejs web application.

**Prerequisite**: Make sure you know Docker Fundamentals if not or if you need a brush up you can read my previous blog on [Introduction to Docker](https://varunmargam.hashnode.dev/docker-explained-understanding-the-power-of-containerization)

---

# 📍Workflow of Containerizing any application:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691394422785/2521aad4-cdd1-45fc-94f4-be29c3fb34fc.png align="center")

To containerize any application or service we have to 1st create a Dockerfile then build a Docker Image from the Dockerfile and then create and run the Docker Container from the Docker image.

Before containerizing a Node js web app let's see what is Dockerfile and how to create one.

---

# 📍Dockerfile

📝Note: A "Docker file" should always be named `Dockerfile` as per the naming convention.

Dockerfile contains a set of instructions that it needs to perform while creating a Docker image and while running a Docker Container.

Dockerfile contains the OS containing the base image, the code, the set of libraries and dependencies required, commands to run and compile the code, set up instructions, etc. Therefore, it acts as a blueprint to build a Docker image.

This is the reason the Dockerfile contains all the necessary things required for an application to run.

Hence, a Dockerfile is a plain text configuration file used to define the steps and instructions for building a Docker image.

---

# 📍Dockerfile Keywords

Keywords are the commands that tell the Docker Engine what to execute. Here are some commonly used Keywords while writing a Dockerfile:

1. FROM: This keyword is used at the very beginning to pull the base image along with the OS from the DockerHub.
    
    ```dockerfile
    FROM openjdk:latest (<tag>)
    # This will pull the latest image of the openjdk from the DockerHub
    # You can also pull another version instead of the latest by typing the tag
    # You can see all the available tags from DockerHub
    ```
    
2. WORKDIR: This keyword is used to create a working directory inside the container where the application code will reside and run.
    
    ```dockerfile
    WORKDIR app/
    # A directory named app has been created that will reside inside the container.
    ```
    
3. COPY: This keyword is used to copy files and directories from the system into the working directory of the container.
    
    ```dockerfile
    COPY app.js .
    # This will copy the code file app.js from the system inside the app/ working directory
    # If the code file resides in the same directory where there is Dockerfile you can directly mention it.
    # But if it does not then you can give the path of the code file.
    ```
    
4. ADD: Similar to COPY but it has additional features like copying files, directories, or remote URLs from the local system or a remote location into the container. It can also automatically unpack compressed files COPY cannot do this.
    
5. ENV: Used to set the environment variables that some services of the app may need to run.
    
    ```dockerfile
    ENV key=value
    #this will set an environment variable named key you can give whatever contains the value given
    #there may be cases when the application or the service may need these environment variables to run
    ```
    
6. EXPOSE: It is used to expose the specified port i.e. the container will listen to this port. Listening on a port means it is actively waiting for incoming data or requests on that port.
    
    ```dockerfile
    EXPOSE 3000
    # The container will listen to port 3000.
    ```
    
7. RUN: Executes commands inside the container during the image build process. It is used to install packages, set up dependencies, and perform any necessary configurations.
    
    ```dockerfile
    RUN pip install flask
    # Like this you can run all the commands to download all the required dependencies.
    ```
    
8. CMD: Specifies the default command to run when the container starts. Unlike the `RUN` keyword, `CMD` does not execute during image build; instead, it defines the command to run when a container is launched from the built Docker image.
    
    ```dockerfile
    CMD ["python","app.py"]
    # This command is to execute the Python code and it will run when the container is launched.
    # The above is the syntax to write a command where each word is written inside
    # " " divided by , inside the [] brackets.
    ```
    

There are some more, we will explore them as we move towards some more advanced docker concepts.

---

# 📍Syntax

There is a format for writing a Dockerfile. A basic format of the Dockerfile can be seen by creating a Dockerfile for a simple Python code/program.

```dockerfile
# Base image
FROM python:3.9

# Working Directory
WORKDIR app/

# Copy the Python code from the system into the container
COPY app.py . #Here, '.' represents the working directory inside the container

# Run some commands like if we want to download some libraries.
RUN pip install flask # But we do not need it so we can ignore this

# Run to execute the code when the container starts running
CMD ["python","app.py"]
```

This is the basic syntax to write a Dockerfile of a simple program as the project becomes more complex the necessary instructions are written to set up the program using keywords.

📝As a DevOps Engineer, you will get the necessary steps to run an application or program from the developer you don't need to memorize this. As you gain more experience in writing Dockerfiles for various projects, you will get an idea of how to write a Dockerfile for any application.🖊

---

# 📍Simple Nodejs Web-App

I took a simple node js web application code from ChatGPT:

```javascript
// Import the core 'http' module
const http = require('http');

// Create an HTTP server
const server = http.createServer((req, res) => {
    // Set the response header
    res.writeHead(200, {'Content-Type': 'text/plain'});

    // Send a response
    res.end('Hello, Node.js!');
});

// Listen on port 3000
server.listen(3000, () => {
    console.log('Server is running on http://localhost:3000/');
});
```

---

# 📍Creating a Dockerfile for a Nodejs web-app

I am using an AWS EC2 instance with Ubuntu Linux OS as a VM:\\

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691406970934/d89d41d8-ccdb-4886-834d-adbacbebdec4.png align="center")

`Step 1`: Create a Directory for the node web app using: `$mkdir node-app` inside `/home/ubuntu/`

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691403769239/7a824abc-1dda-4391-bebc-605af6f374a7.png align="center")

`Step 2`: Create a file named `app.js` inside the `node-app/` directory and copy the above code using the Vim editor then save & quit (`:wq`)

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691403916735/797499f7-7dfb-42f7-80a6-ba54a14d9092.png align="center")

`Step 3`: Create a Dockerfile using the Vim editor `$vim Dockerfile` and write the below code:

```dockerfile
# This is a base image for the nodejs web app
FROM node:20-alpine3.17

# Creating a Working directory inside the container
WORKDIR app/

# Copying the code from our system into the Working directory
COPY app.js .

# Installing all the necessary libraries required for the web-app
RUN npm i -g install

# Command to run the nodejs web app when the container is launched
CMD ["node","app.js"]
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691403979783/b25d7eff-defd-4358-a9c6-f1bcde2c0870.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691404088332/45bb3897-918e-454e-89fc-1bfdc0314375.png align="center")

---

# 📍Building a Docker Image

`Step 4`: Build the Docker image using the Dockerfile using the command:

`$docker build . -t node-app:latest`: This will create the Docker image `node-app`

`.` means create a Docker image from the Dockerfile in this directory.

`-t` means "tag" i.e. naming the Docker image once it is built.

`node-app:latest` is the name of the Docker image with the `latest` tag.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691404148432/c3da47ea-d566-434d-92d1-9c37d66f62ff.png align="center")

You can see the list of Docker images using the command: `$docker images`

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691404234442/193b7386-3239-40a0-a8ab-40e39ec15b1d.png align="center")

---

# 📍Containerizing Nodejs Web-app

`Step 5`: Run this Docker image using the `docker run` command:

`$docker run -d -p 3000:3000 node-app:latest`:

`-d` It means to run this command as a background process (in the detached mode) like a daemon.

`-p 3000:3000` It is used to map port 3000 of my system to port 3000 of the container so that I can access the services running inside the container.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691404333720/a38b6e5f-509e-4b75-8ef0-f5f7a0a9e0d1.png align="center")

`:3000` Acts as `EXPOSE 3000` commands in the Dockerfile so know port 3000 of the container will receive the traffic from port 3000 of the local system.

Your container containing the Node js web application has been deployed and is now up and running.

You can see the Nodejs web app has been deployed from the AWS EC2 instance IPv4 address:3000:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691404764225/14e5c19b-28c2-45c2-bdc4-340a3e5fe720.png align="center")

Make sure that the inbound rules of the Security Groups of the EC2 instance allow the traffic from anywhere or your Ip address to port 3000:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691404919488/80d1a7aa-36ac-4e59-abdf-9ae3bb637639.png align="center")

🥳Congratulations!! You have containerized a Node js web application from scratch and deployed it.🎉

Remember creating a Dockerfile of any program will come from practice so keep practicing and keep learning. When working with the team the steps to set up an application will be given by the developer. But there may be cases where it is not documented in such cases you have to be comfortable with writing Dockerfiles for any program by researching, practicing, and troubleshooting the errors.

---

# 📍Conclusion

Now, you will be able to build Dockerfile for any Node js application and containerize it. Take some more applications of Node js or a Flask app or MySQL service and try to containerize it. You will get errors, but don't worry it is a part of the process try to google the error, explore, and learn more steadily you will become confident in writing a Dockerfile for any Tier 1 application.

Thank you for reading this blog! 📖 Hope you have gained some value.

If you enjoyed this blog and found it helpful, please give it a like 👍, share it with your friends, do share your thoughts, and give me some valuable feedback.😇 Don't forget to follow me for more such blogs! 🌟

---

# 📍Reference

* [Docker Documentation](https://docs.docker.com/)
    

---