---
title: "Docker Cheatsheet: A Comprehensive Resource for DevOps Professionals"
datePublished: Wed Aug 16 2023 17:55:07 GMT+0000 (Coordinated Universal Time)
cuid: clle1951i000d08mbflrzeybd
slug: docker-cheatsheet-a-comprehensive-resource-for-devops-professionals
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1692206051745/0d15738a-106e-404b-b44b-1c38e30217d1.png
tags: docker, devops-journey, 90daysofdevops, day20, dockercheatsheet

---

---

# 📍Installation

1. Install Docker on Linux:
    
    ```yaml
    sudo apt install docker.io (ubuntu)
    sudo yum install docker (centos)
    ```
    
2. Install Docker desktop for Windows: [download docker](https://www.docker.com/products/docker-desktop/)
    

---

# 📍Docker Commands

1. `sudo usermod -aG docker <user>`: Allow `<user>` to run docker commands. By default, only the root user has permission to run docker commands.
    
2. `docker pull <image:tag>`: Pulls Docker image from the Registry DockerHub.
    
3. `docker push <image:tag>`: Pushes the docker image from the local system to the DockerHub.
    
    ```bash
    # Step 1: Login to your dockerhub
    # Step 2: In your docker CLI do:
    docker login
    # Enter username and password of your DockerHub profile
    # Change the name of your image in the format username/dockerimage:tag
    docker image tag <old_image_name> <username/image_name:tag>
    # Push the docker image to the dockerhub
    docker push <new_image_name:tag>
    # This will push your image to the Dockerhub in your repository.
    ```
    
4. `docker build <path of Dockerfile> -t <docker_image_name>`: Build Docker image from the Dockerfile `-t` means `tag` an option to give a name to the Docker image.
    
5. `docker images`: Lists all Docker images in the system with image\_id, date of creation, etc.
    
6. `docker images -q`: Lists only the image\_id of all the Docker images in the system.
    
7. `docker rmi <image_id or image_name:tag>`: Removes the image.
    
8. `docker rmi $(docker images -q)`: Removes all the unused images, and throws an error if an image is in use.
    
9. `docker image prune -a`: Removes only the unused or dangling images and not the images used by a container. Gives you a prompt to proceed or not.
    
10. `docker image prune -af`: `-f` flag is a force flag that removes unused images without giving a prompt.
    
11. `docker run <image>`: Run a Docker container from the docker `<image>`.
    
12. `docker run -d <image>`: Run a Docker container in the background `(-d: detached mode)`.
    
13. `docker run -d -p <host_port:container_port> <docker_image_name>`: Run a Docker container in the background.
    
    `-p <host_port:container_port>`: This flag maps a port from the host machine to a port on the container. Replace `<host_port>` with the port number on the host machine, and `<container_port>` with the port number the container is listening on.
    
14. **Pass Environment Variables to a Container:**
    
    ```bash
    bashCopy codedocker run -e VAR_NAME=value <image>
    ```
    
15. `docker exec -it <container_id> <shell>`: Gives `-it` interactive terminal, a `<shell>` inside the running container to interact or run commands.
    
16. `docker ps`: Lists all the running containers along with some additional information.
    
17. `docker ps -a`: Lists all the containers running or stopped existing in the system.
    
18. `docker ps -q`: Lists only the `container_id` of all the running containers in the system.
    
    `docker ps -qa`: Lists only the `container_id` of all the containers in the system.
    
19. `docker inspect <container_id>`: Gives detailed information about the specified container like container configuration, network information, mount and volumes, resources, etc.
    
20. `docker logs <container_id>`: Gives logs generated while the container is running. This information helps in troubleshooting as we can see where an error has occurred.
    
21. `docker kill <container_id>`: Used to forcefully terminate a running container without giving it a chance to perform any cleanup or shutdown procedures.
    
22. `docker stop <container_id>`: Used to gracefully stop a running container by allowing the process to perform any necessary cleanup tasks before the container shuts down.
    
23. `docker rm <container_id>`: Used to remove the stopped container, and throws an error if the container is in use.
    
24. `docker rm $(docker ps -qa)`: Used to remove all the stopped containers.
    
    *(Note: Make sure no containers are running otherwise will throw an error.)*
    

---

# 📍Docker Compose Commands

📝Note: You must run all these docker-compose commands inside the directory where `docker-compose.yml` is present otherwise it will not be able to find the docker-compose configuration file and will not execute.🖊

1. `docker-compose up`: Starts the containers defined in the `docker-compose.yml` file. If required Docker images are not present then it will either pull the images from the Docker Registry or build the image from the Dockerfile provided before starting the container.
    
2. `docker-compose up --build`: Start and recreate containers, forcing a build.
    
3. `docker-compose up --no-build`: Start the containers with the available images without building images. If the related images are not found it will throw an error.
    
4. `docker-compose up -d`: Start containers in the background `(-d: detached mode)`.
    
5. `docker-compose down`: Stop and removes all the running containers networks, and volumes defined in the `docker-compose.yml` file for a specific project.
    
6. `docker-compose build`: Build images defined in the `docker-compose.yml` file.
    
7. `docker-compose logs`: View logs of all the services or containers running from the `docker-compose` command.
    
8. `docker-compose logs <service_name or container_id>`: View logs of the service specified.
    
9. `docker-compose ps`: List all the containers (running or stopped) associated with the services defined in the `docker-compose.yml` file.
    
10. `docker-compose rm`: Removes stopped service containers that are defined in the `docker-compose.yml` file.
    
11. `docker-compose up -d --scale <service_name>=<num_of_replicas>`: Used to scale services. Creates replicas in Swarm Mode.
    

---

# 📍Docker Volumes Commands

1. `docker volume create --name <volume_name> --opt type=<volume_type> --opt device=<directory_path> --opt o=bind<or any other>`:
    
    * `docker volume create`: This is the main command used to create a Docker volume.
        
    * `--name <volume_name>`: This flag specifies the name of the volume you want to create.
        
    * `--opt type=<volume_type>`: This flag is used to specify options for the volume. The `type` option indicates the type of the volume. This can be used to set the type of storage for the volume, such as `nfs`, `vfs`, `btrfs`, `host`, etc.
        
    * `--opt device=<directory_path>`: This flag specifies the directory path of the device for the volume where the data from the container will be stored. This could be a directory on the host machine or a network-attached storage path.
        
    * `--opt o=bind`: This flag allows you to pass additional options to the volume. The `o` option can be used to specify additional mount options, such as `bind` for mounting a directory from the host machine into the volume.
        
2. `docker run -d --mount source=<volume_name>,target=<container_path> <image_name:tag>:` Mount the docker volume to the container and then starts the container.
    
    We cannot directly mount volumes in a Dockerfile it doesn't handle runtime configuration like volume mounting. Therefore, we mount the volume while starting the container.
    
    * `docker run`: This command starts a new container instance based on a specified image.
        
    * `-d`: This flag runs the container in detached mode, which means the container runs in the background and doesn't attach to the terminal.
        
    * `--mount source=<volume_name>,target=<container_path>`: This flag specifies the volume to mount inside the container. `<volume_name>` is the name of the volume you want to mount, and `<container_path>` is the path inside the container where the volume will be mounted.
        
        `<container_path>` refers to directories and files within the container, such as application data directories, configuration files, or any specific paths that your application or process might require.
        
    * `<image_name:tag>`: This is the name and tag of the Docker image from which you want to run the container.
        
3. `docker volume ls`: Lists all the docker volumes present in your system.
    
4. `docker volume rm <volume_name>`: Removes the specified volume, and throws an error if the volume is still in use by a running or stopped container i.e. actively using it.
    
5. `docker volume prune`: Deletes all the unused volumes.
    
6. `docker volume inspect <volume_name>`: It provides a JSON-formatted output that contains various details about the volume's configuration, usage, and metadata.
    
7. **Mount a Volume in Docker Compose:**
    
    ```yaml
    yamlCopy codeservices:
      myservice:
        image: <image-name>
        volumes:
          - <volume-name>:<container-path>
    ```
    
8. **Use a Named Volume in Docker Compose:**
    
    ```yaml
    yamlCopy codeservices:
      myservice:
        image: <image-name>
        volumes:
          - <volume-name>:<container-path>
    volumes:
      <volume-name>:
    ```
    

---

# 📍Docker Network Commands

1. `docker network create <network_name>`: create a custom Docker network with the specified name.
    
2. `docker network rm <network_name>`: Removes the specified network and disconnects any containers that are connected to it.
    
3. `docker network ls`: Lists all the networks currently present on your system.
    
4. `docker inspect <network_name>`: Provides a JSON-formatted output that contains various details about the network, including its configuration, containers connected to it, IP addresses, and more. This information can be useful for troubleshooting network-related issues and understanding how containers are interacting within the network.
    
5. `docker network prune`: Removes unused docker networks.
    
6. `docker run --network <network_name> <container_id>`: Attach specific network to the Docker container before running.
    
7. `docker network connect <network_name> <container_id>`: Attach already running containers or containers launched using different commands to the user-defined network.
    

---

# 📍Conclusion

Thank you for reading this blog! 📖 Hope you have gained some value.

If you enjoyed this blog and found it helpful, please give it a like 👍, share it with your friends, share your thoughts, and give me some valuable feedback.😇 Don't forget to follow me for more such blogs! 🌟

---