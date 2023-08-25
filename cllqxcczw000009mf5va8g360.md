---
title: "Docker Important interview Questions"
datePublished: Thu Aug 24 2023 18:30:00 GMT+0000 (Coordinated Universal Time)
cuid: cllqxcczw000009mf5va8g360
slug: docker-important-interview-questions
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1692987985442/9183733c-dfa8-45db-a1bb-cbab9937cd4c.png
tags: docker, devops-journey, 90daysofdevops, day21, docker-interview-questions

---

---

1. What is the Difference between an Image, Container, and Engine?
    
    Ans:
    
    **Docker Image**: A blueprint that contains all the necessary libraries, dependencies, and code to run a service or an app. Docker Image is built from a configuration file called Dockerfile. Docker images are also stored in a Registry called DockerHub where predefined images of services are kept in a repository with various tags. These tags indicate the version of that service.
    
    **Docker Container**: It is a running instance of a Docker Image. Docker Image is a blueprint containing instructions on how to run the app. Container is an isolated environment that runs the service and is deployed on the server.
    
    **Docker Engine**: It is a software or a program that sits on top of the Host Operating system that allows us to run multiple containers on the host machine. Docker Engine consists of two parts:
    
    1. **Docker Daemon**: It is a background process that manages the containers, networking, and storage for containers, and uses a low-level service called container d (daemon) that creates, removes, and schedules the container.
        
    2. **Docker CLI**: It is a command Line Interface that helps us run Docker commands to perform various docker-related tasks.
        
    
    <details data-node-type="hn-details-summary"><summary>Things that can be added</summary><div data-type="detailsContent"><strong>Docker images</strong> are read-only and immutable, which ensures consistency across different environments and helps with reproducibility. <strong>Docker Containers</strong>: Containers are isolated environments that package not just the application code, but also all the required runtime dependencies, making them highly portable and consistent. <strong>Docker Engine: </strong>It manages resources, isolates containers, and enables communication between them. Docker Engine is part of the larger Docker platform, which also includes tools like Docker Compose and Docker Swarm for orchestration.</div></details>
2. What is the Difference between the Docker command **COPY** vs. **ADD**?
    
    Ans:
    
    **COPY** and **ADD** are both keywords that are used to write a Dockerfile. Although both do similar tasks there are some differences in their features.
    
    **COPY**: This command copies the files or folders from the system inside the Working Directory of the Container. We have to specify the files or folder that we want to copy from our local machine.
    
    **ADD**: Similar to **COPY**, it copies the files or folder from the local machine to the container's working directory. But it has an added functionality i.e. it can also pull or download content or code from an external URL or a repository.
    
    <details data-node-type="hn-details-summary"><summary>Things that can be added</summary><div data-type="detailsContent"><strong>ADD</strong>: It can be used to directly download and extract an archive from a URL or pulling code from a version control repository.</div></details>
3. What is the Difference between the Docker command CMD vs. RUN?
    
    Ans:
    
    **CMD** and **RUN** are both primary keywords that are used while defining a Dockerfile.
    
    **RUN**: It is used to run the commands while building the Docker image. These commands generally include downloading libraries, dependencies, runtime environment, and running some test cases that are necessary to ensure the app is running when deployed in a container. The commands mentioned using each RUN keyword act as a different layer while building the Docker image, therefore it is a good practice to put all the required commands that can be grouped in a single RUN keyword that helps in reducing the layers while building a Docker Image.
    
    **CMD**: In this keyword, we mention the commands that we want to run while the container is being deployed. These can include commands for post-build actions that can include sending a message, giving a prompt, etc.
    
    <details data-node-type="hn-details-summary"><summary>Things that can be added</summary><div data-type="detailsContent"><strong>RUN</strong>: It's important to clarify that the commands in the <code>RUN</code> instruction are executed at image build time, and they contribute to the creation of the intermediate image layers. These layers make up the final image. Additionally, besides downloading dependencies and running tests, the <code>RUN</code> command can also be used for setup tasks like creating directories, setting environment variables, etc. <strong>CMD</strong>: The commands specified in <code>CMD</code> are not executed during the build process but rather when the container is run based on the image. These commands can include the main process that your container should run, like starting a web server or running an application.</div></details>
4. How will you reduce the size of the Docker image?
    
    Ans:
    
    This answer is from ChatGPT as I did not have a comprehensive knowledge on this topic:
    
    Reducing the size of a Docker image is essential for efficient containerization and optimized resource usage. Here are several techniques you can use to achieve this:
    
    1. **Use a Minimal Base Image:** Start with a minimal base image, like Alpine Linux or a "slim" version of official images. These images contain only essential components, helping to keep your image size small.
        
    2. **Optimize Dockerfile Instructions:** Be mindful of how you structure your Dockerfile. Combine multiple commands into a single `RUN` instruction to minimize layers. For example:
        
        ```dockerfile
        RUN apt-get update && apt-get install -y package1 package2 && apt-get clean
        ```
        
    3. **Clean Up After Installations:** After installing packages or software, remove temporary files and caches using `apt-get clean`, `yum clean`, or `apk cache clean` to reduce the image size.
        
    4. **Use Multi-Stage Builds:** If possible, use multi-stage builds. This involves creating a build image with all development tools, compiling your application, and then copying only the necessary artifacts to a smaller runtime image.
        
    5. **Minimize Installed Components:** Only install libraries and dependencies that your application needs. Avoid including unnecessary tools or files that won't be used.
        
    6. **Avoid Unnecessary Files:** Use `.dockerignore` to exclude files and directories that are not needed in the image, such as logs, temporary files, and build artifacts.
        
    7. **Use COPY Instead of ADD:** Prefer the `COPY` command over `ADD` when copying files into the image. This prevents unnecessary extraction and potential security risks.
        
    8. **Single Responsibility Principle:** Each container should have a single responsibility. Splitting applications into separate containers can help reduce their individual sizes.
        
    9. **Compress Artifacts:** If your application generates build artifacts, compress them before copying them into the image. This reduces the size of transferred files.
        
    10. **Use Smaller Alternatives:** Consider using lightweight alternatives for tools and services. For example, use NGINX instead of Apache if your needs allow it.
        
    11. **Optimize Layers:** Arrange instructions in your Dockerfile so that frequently changing parts (like source code) are placed later. This way, changes to your application code won't invalidate previous layers.
        
    12. **Minimize the Number of Layers:** As mentioned earlier, minimize the number of layers in your image. Each layer adds overhead to the image size.
        
    
    Remember that these techniques can be combined to achieve the best results. The goal is to create lean and efficient images that still fulfill the requirements of your application.
    
5. Why and when to use Docker?
    
    Ans:
    
    Docker is ideal for scenarios where a microservice architecture is implemented. Since it provides isolation, and virtualization and also is a better alternative than virtual machines. Since docker is lightweight, it uses a Host kernel for performing tasks rather than downloading the whole OS.
    
    A more comprehensible answer from **ChatGPT**
    
    Docker is a powerful tool for containerization, offering numerous advantages for various scenarios:
    
    1. **Microservices Architecture:** Docker is well-suited for microservices-based applications. It allows you to package each component of your application as a separate container, enabling easy deployment, scaling, and management of individual services.
        
    2. **Isolation and Consistency:** Docker containers provide process-level isolation, ensuring that applications run in their own isolated environments. This isolation improves security and prevents conflicts between applications that share the same host.
        
    3. **Portability:** Docker containers encapsulate the application and its dependencies, including libraries and configurations. This "containerized" format makes applications highly portable across different environments, from development to production.
        
    4. **Efficiency and Resource Utilization:** Compared to traditional virtual machines, Docker containers share the host system's OS kernel, resulting in less overhead. Containers are lightweight and start up quickly, enabling efficient use of resources.
        
    5. **Development and Testing:** Docker simplifies development and testing by providing consistent environments across various stages of the development lifecycle. Developers can build containers locally that closely resemble the production environment.
        
    6. **Continuous Integration/Continuous Deployment (CI/CD):** Docker plays a vital role in CI/CD pipelines. You can define the application's environment in a Dockerfile, ensuring that the same environment is used for testing and deployment, reducing "it works on my machine" issues.
        
    7. **Scalability and Load Balancing:** Docker containers can be easily scaled up or down to handle varying loads. Container orchestration tools like Kubernetes and Docker Swarm make managing and scaling containerized applications seamless.
        
    8. **Version Control and Rollbacks:** Docker images are versioned, enabling you to track changes and roll back to previous versions if needed. This simplifies version control and makes application updates more manageable.
        
6. Explain the Docker components and how they interact with each other.
    
    Ans:
    
    1. **Docker Engine:** The Docker Engine is the core component of Docker. It's responsible for managing and running containers on a host system. It includes two main parts:
        
        * **Docker Daemon:** The Docker daemon is a background service responsible for building, running, and managing Docker containers. It listens for Docker API requests and manages container processes.
            
        * **Docker CLI:** The Docker Command Line Interface (CLI) is a tool that allows users to interact with the Docker daemon. It provides a set of commands to create, manage, and control Docker containers and images.
            
    2. **Dockerfile:** A Dockerfile is a text file that contains a set of instructions for building a Docker image. It specifies the base image, environment variables, application code, dependencies, and configuration needed to create a functional container. Dockerfiles are used to automate and standardize the image-building process.
        
    3. **Docker Image:** A Docker image is a lightweight, standalone, and executable software package that contains everything needed to run a piece of software, including code, runtime, libraries, and dependencies. Images are built from Dockerfiles and serve as blueprints for creating Docker containers.
        
    4. **Docker Container:** A Docker container is a runnable instance of a Docker image. It encapsulates the application and its runtime environment, providing isolation from the host system and other containers. Containers can be started, stopped, and managed independently. They are ephemeral and designed to be disposable and replaceable.
        
    
    **Interaction and Workflow:**
    
    1. A developer creates a **Dockerfile** that defines the environment and instructions for building an application image.
        
    2. The developer uses the **Docker CLI** to execute the `docker build` command, which processes the Dockerfile and creates a **Docker image**. The image is stored in the host system's Docker image registry.
        
    3. The developed image can now be shared and distributed among various environments or other team members.
        
    4. To run the application, the developer or operations team uses the **Docker CLI** to execute the `docker run` command, creating a **Docker container** based on the image. The container runs as an isolated process on the host system.
        
    5. Containers can be stopped, started, paused, and removed using the **Docker CLI**.
        
7. Explain the terminology: Docker Compose, Docker File, Docker Image, Docker Container?
    
    Ans:
    
    Docker Compose is a program or a feature of Docker that allows us to run multiple containers using a single command using the docker-compose command. It is useful for containerizing a multi-tier application. It runs according to the instructions given in a configuration file named docker-compose.yml file. It is written in the YAML language popularly used for scripting where we specify the instructions to run the application and the services in a container.
    
    Dockerfile: It is a configuration file that Docker follows to build a Docker Image. It contains a set of instructions for the setup required to run an app or a service. It is defined using keywords like IMPORT, WORKDIR, COPY, RUN, CMD, etc.
    
    Docker Image: It is a snapshot of all the code and necessary components used to run an application or a service. It is built from a Docker file and acts as a blueprint for a Docker container.
    
8. In what real scenarios have you used Docker?
    
    Ans:
    
    **Microservices Architecture:** Docker is often used to containerize individual microservices within a larger application. This approach enables better isolation, scalability, and maintainability of each component. I have used Docker-compose while containerizing a 2-tier flask web application.
    
    **Continuous Integration/Continuous Deployment (CI/CD):** Docker is integrated into CI/CD pipelines to build, test, and deploy applications automatically. Containers provide a consistent environment for testing and deploying code changes. I have integrated Docker with Jenkins while building a CI/CD pipeline for a 2-tier flask application.
    
9. Docker vs. Hypervisor?
    
    Ans:
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691108830993/a29c4925-d5dd-43bd-9604-2552f669d8cc.webp?auto=compress,format&format=webp align="left")
    
    * **Hypervisor** sits on top of the infrastructure and allows to create VMs with their OS called Guest OS.
        
    * **Docker** Engine uses the Host OS for its operations and helps you run and manage the containers. Since they have no OS they are lightweight processes and take less time to boot therefore, we can run more containers.
        
    * **Virtualization** is Hardware virtualization since you get virtual RAM, virtual CPU, virtual Hardware, etc. so you can install an OS to create a Virtual Machine.
        
    * Since processes need OS to run **Docker** creates an illusion of having an OS inside the container for the process to run. Therefore, containerization is OS Virtualization.
        
    
    Docker's lightweight and portable approach is excellent for microservices and containerized applications, while hypervisors are more appropriate for scenarios requiring strong isolation between applications or support for multiple operating systems on a single machine.
    
10. What are the advantages and disadvantages of using docker?
    
    Ans:
    
    **Advantages of Using Docker:**
    
    1. **Isolation and Portability:** Docker containers encapsulate applications and their dependencies, providing consistent and isolated runtime environments. This isolation makes it easier to move applications across different environments, from development to production.
        
    2. **Efficiency and Resource Utilization:** Docker containers share the host OS kernel, leading to efficient resource utilization. Containers start quickly and have lower overhead compared to traditional virtual machines.
        
    3. **Consistency and Reproducibility:** Docker enables consistent environments throughout the development lifecycle. What works in a developer's environment is likely to work the same way in production, reducing issues related to "it works on my machine."
        
    4. **Continuous Integration/Continuous Deployment (CI/CD):** Docker containers simplify CI/CD pipelines by providing a standardized environment for testing and deployment. This ensures that code behaves consistently across various stages.
        
    5. **Microservices Architecture:** Docker is well-suited for microservices-based applications, allowing teams to develop, test, and deploy individual services independently.
        
    
    **Disadvantages of Using Docker:**
    
    1. **Security Risks:** While containers provide isolation, misconfigured containers or insecure images can still pose security risks. Proper security practices and continuous monitoring are necessary.
        
    2. **Persistent Data:** Handling persistent data in Docker containers can be complex. Special solutions or volume mounts are needed to ensure data persistence beyond the lifecycle of a container.
        
    3. **Limited Operating System Support:** Containers share the host OS kernel, so all containers must run on the same type of OS. This might not be suitable for all use cases.
        
    4. **Resource Sharing:** Sharing the host OS kernel means that resource-heavy containers could potentially affect the performance of other containers on the same host.
        
    5. **Version Control and Storage:** Docker images can accumulate over time, consuming storage space. Careful image management and version control are needed to prevent storage bloat.
        
    6. **Complex Networking:** Networking configuration in Docker containers can be complex, especially when dealing with multiple containers and services.
        
    7. **Image Vulnerabilities:** Using pre-built images can introduce vulnerabilities if not properly maintained or monitored for security updates.
        
11. What is a Docker namespace?
    
    Ans:
    
    Need to learn this, I do not know about this concept at all.
    
12. What is a Docker registry?
    
    Ans:
    
    A Docker registry is a place that stores and hosts repositories that contain predefined Docker Images created by the users and organization. DockerHub is a Docker Registry that hosts Docker Repositories. It is a place from where docker pulls the image if needed to run the container. Some images are stored in the local system if they are not present in the local system then Docker pulls the image from the Docker Registry.
    
13. What is an entry point?
    
    Ans:
    
    Don't know much about it apart from knowing that is a keyword used to define Dockerfiles, since up until now there haven't been instances where I needed to use this keyword to define a Dockerfile.
    
14. How to implement CI/CD in Docker?
    
    Ans:
    
    By integrating Docker with Jenkins we can implement CI/CD. Jenkins is a primary tool that helps us to automate the software development process with pipelines. Certain steps require integration of docker since docker provides a click command to deploy an app as well as remove the app from the deployed environment.
    
15. Will data on the container be lost when the docker container exits?
    
    Ans:
    
    If a running container is stopped or killed the data inside the container will be lost even if the container is not removed from the system. Docker volumes were created to overcome this issue and persist the data from the docker containers. Docker volume provides a bridge between the local system and the container that can transfer the data from the container to the local machine and vice versa. To achieve that we have to create docker volumes in our local machine using docker CLI and mount the created volume to the container while running the `docker run` command using the flag `--mount`.
    
16. What is a Docker swarm?
    
    Ans:
    
    I haven't learned this concept since I was told that it is no longer used in the industry as an alternative to this Kubernetes is the tool that is more popularly used to manage and orchestrate containers.
    
    Here's the answer from ChatGPT:
    
    Docker Swarm, often referred to as "Docker Swarm Mode," is a native clustering and orchestration solution provided by Docker. It allows you to create and manage a swarm of Docker nodes, enabling you to deploy and manage services across a cluster of machines.
    
    **Key Concepts of Docker Swarm:**
    
    1. **Node:** A physical or virtual machine that participates in the Docker Swarm. Nodes can be manager nodes or worker nodes.
        
    2. **Manager Node:** A manager node is responsible for orchestrating the activities within the swarm. It maintains the cluster state, schedules services, and manages worker nodes.
        
    3. **Worker Node:** Worker nodes are the machines where containers are deployed and run. They perform the actual work of running containers.
        
    4. **Service:** A service is a definition of the tasks to be executed on the worker nodes. It specifies the image, desired replicas, and other settings.
        
    5. **Task:** A task is a unit of work that a worker node performs. It represents an instance of a running container associated with a service.
        
    6. **Overlay Network:** Docker Swarm provides built-in overlay networking, allowing services running on different nodes to communicate securely with each other, regardless of the physical network setup.
        
    7. **Load Balancing:** Swarm includes an integrated load balancer that distributes incoming traffic among the replicas of a service.
        
    8. **Scaling and Rolling Updates:** You can scale services up or down to meet demand, and you can also perform rolling updates to update services without downtime.
        
    9. **High Availability:** Manager nodes use a consensus algorithm to ensure high availability and fault tolerance. If a manager node fails, another manager can take over.
        
    
    **Use Cases for Docker Swarm:**
    
    1. **Container Orchestration:** Docker Swarm simplifies the management of containerized applications across a cluster of machines, making it easier to deploy, scale, and update services.
        
    2. **Microservices:** Docker Swarm is a suitable choice for deploying and scaling microservices-based applications, managing individual services as part of a larger application.
        
    3. **Scalability:** Swarm's built-in load balancing and scaling capabilities make it easy to scale services up or down based on demand.
        
    4. **Zero-Downtime Deployments:** Docker Swarm's rolling updates feature allows you to update services without causing downtime for users.
        
    5. **Simplified Setup:** Docker Swarm is included with Docker and doesn't require external tools or additional installations.
        
17. What are the docker commands for the following:
    
    * view running containers
        
        ```bash
        docker ps
        ```
        
    * command to run the container under a specific name:
        
        ```bash
        docker run -t -d --name <container_name> <image_name>
        ```
        
    * command to export a docker:
        
        To export a container as an image, you can commit the changes made to a container into a new image.
        
        ```bash
        docker commit <container_id> <new_image_name> # I did not know this
        ```
        
    * command to import an already existing docker image:
        
        ```bash
        docker pull <image_name>:<tag>
        ```
        
    * commands to delete a container:
        
        ```bash
        docker stop/kill <container_id> && docker rm <container_id>
        ```
        
    * command to remove all stopped containers, unused networks, build caches, and dangling images?
        
        ```bash
        docker system prune -a
        ```
        
18. What are the common Docker practices to reduce the size of Docker Images?
    
    Ans: I did not have a satisfactory comprehensive answer
    
    **ChatGPT** answer:
    
    Reducing the size of Docker images is important for optimizing resource usage, speeding up image distribution, and improving security. Here are common Docker image size reduction practices:
    
    1. **Use Alpine Linux or Minimal Base Images:** Choose lightweight base images like Alpine Linux instead of full-fledged operating systems. Alpine images are smaller and contain only essential components.
        
    2. **Multi-Stage Builds:** Utilize multi-stage builds to create intermediate images for building and compiling your application, then copy only the necessary artifacts into the final runtime image. This reduces the final image size significantly.
        
    3. **Minimize Layers:** Each instruction in a Dockerfile creates a new layer in the image. Minimize the number of layers by grouping related instructions into a single RUN command.
        
    4. **Use Specific Tags for Base Images:** Specify specific tags (e.g., version numbers) for base images. This prevents unintentional updates when using generic tags like "latest."
        
    5. **Remove Unnecessary Files:** Clean up after installing packages. Remove temporary files, cache, and any files that are not required in the final image.
        
    6. **Optimize Dockerfile Instructions:** Order instructions wisely. For example, copy only necessary files, run apt-get update and install in the same layer, and clean up apt caches in the same RUN instruction.
        
    7. **Avoid Installing Unnecessary Dependencies:** Only install libraries and packages that are required for your application. Removing unnecessary dependencies reduces image size.
        
    8. **Use .dockerignore File:** Create a `.dockerignore` file to exclude unnecessary files and directories from being added to the image during the build process.
        
    9. **Compress Assets:** Compress files, images, and other assets before adding them to the image. This reduces the size of the image and the resources required to transmit it.
        
    10. **Use Smaller Alternatives:** Opt for smaller alternatives or minimalist libraries when available. For example, use a smaller web server like Nginx instead of a full Apache HTTP server.
        
    11. **Avoid Running Services in the Same Container:** Design your application to separate different components into different containers. Don't run multiple services within a single container, as it increases the size and complexity.
        
    12. **Use Caching Wisely:** Use Docker's caching mechanisms effectively. Place instructions that change less frequently (e.g., installing dependencies) earlier in the Dockerfile to leverage the cache for subsequent builds.
        

---

# 📍Reference

* [ChatGPT](https://openai.com/chatgpt)
    

---