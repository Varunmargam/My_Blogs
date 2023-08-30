---
title: "Exploring Docker Compose: Building a 2-Tier Flask To-Do Web App"
datePublished: Mon Aug 14 2023 18:21:47 GMT+0000 (Coordinated Universal Time)
cuid: cllb7bq2h000c09jz5mwecrti
slug: exploring-docker-compose-building-a-2-tier-flask-to-do-web-app
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1692037151914/2549617c-d348-4a5b-91e6-f32eb9308630.jpeg
tags: docker, docker-compose, devops-journey, 90daysofdevops, day18

---

---

# 📍Introduction

Welcome to my Docker blog series! Here, we'll explore docker-compose and do a hand's-on project by containerizing and deploying a **2-tier flask to-do web application** and also troubleshooting the errors we will be facing.

**Prerequisite**: Make sure you know Docker Fundamentals if not or if you need a brush up you can read my previous blogs:

* [Introduction to Docker](https://varunmargam.hashnode.dev/docker-explained-understanding-the-power-of-containerization)
    
* [Mastering Docker: Containerize Your Application with Dockerfile, Docker Image, and Containers](https://varunmargam.hashnode.dev/mastering-docker-containerize-your-application-with-dockerfile-docker-image-and-containers)
    

---

# 📍Docker Compose

Up until now, we've explored how to containerize individual services or simple applications. However, real-world applications often follow a multi-tier architecture involving 2 or 3 tiers.

Consider a scenario where we aim to containerize a 3-tier architecture application, comprising:

1. **Front-end**
    
2. **Back-end**
    
3. **Database**
    

To containerize this application, we adopt a strategy of isolating each program into distinct containers to containerize this intricate setup. Thus, we establish three separate containers one for the front end, another for the back end, and a third for the database. We accomplish this by crafting a Dockerfile for each component.

**The approach involves two main steps**:

1. **Organizing Directory Structure**: We create two directories—one for the front end and another for the back end. Within these directories, we place the respective codes along with their dedicated Dockerfiles. Meanwhile, the Dockerfile for the database resides in the project directory where the front-end and back-end directories are located.
    
2. **Building and Running Containers**: Once the directories and Dockerfiles are in place, we initiate the process by executing `docker build` and `docker run` for each `Dockerfile`. This step efficiently constructs the containers, encapsulating the distinct tiers.
    

Consider this scenario: We previously discussed a 3-tier architecture, but now imagine a more complex microservice architecture where each service needs to be containerized. The manual approach we discussed earlier would become impractical in this context. Fortunately, there's a more efficient solution: "Docker Compose."

Docker Compose is a tool that comes with a program called docker-compose. It offers a streamlined method for managing multi-container applications. Instead of individually building and launching containers, Docker Compose allows us to define all the necessary actions in a single **configuration file**. This file outlines how to build and run multiple Docker containers concurrently, eliminating the need for repetitive tasks. Operations like `docker-compose up` and `docker-compose down` simplify the process further. The configuration file itself is written in **YAML (Yet Another Markup Language)**, and it typically carries the name "`docker-compose.yml`" for convention's sake

Some common Docker Compose commands:

1. `docker-compose up`: Build and start containers as defined in the `docker-compose.yml` file.
    
2. `docker-compose up -d`: Build and start containers in the background (detached mode).
    
3. `docker-compose down`: Stop and remove containers, networks, and volumes defined in the `docker-compose.yml` file.
    
4. `docker-compose build`: Build images for services defined in the `docker-compose.yml` file.
    
5. `docker-compose start`: Start containers that are already defined in the `docker-compose.yml` file.
    
6. `docker-compose stop`: Stop containers that are already defined in the `docker-compose.yml` file.
    
7. `docker-compose ps`: List running containers defined in the `docker-compose.yml` file.
    
8. `docker-compose logs`: Display logs from containers defined in the `docker-compose.yml` file.
    
9. `docker-compose exec`: Execute a command in a running container.
    
10. `docker-compose run`: Run a one-off command in a new container.
    
11. `docker-compose pull`: Pull images from the registry as defined in the `docker-compose.yml` file.
    
12. `docker-compose images`: List images used by the services in the `docker-compose.yml` file.
    
13. `docker-compose config`: Validate and view the final configuration after variable substitution in the `docker-compose.yml` file
    

📝Make sure to run these commands where the `docker-compose.yml` file is present.🖊

---

# 📍YAML: Configuration Language

YAML is a markup language and is commonly used alongside JSON for creating configuration files. Let's explore how to compose a YAML file.

To understand the syntax of YAML we will be taking an example of a Python data structure "dictionary".

```python
dict= ["name": "Varun", "age": 21, "hobbies": {singing, dancing, guitar}]

# Check out my Python blog if you don't know about Python dictionary.
```

[Python: Empowering DevOps with Automation and Efficiency (Part 2)](https://varunmargam.hashnode.dev/python-empowering-devops-with-automation-and-efficiency-part-2)

We will be converting this Python dictionary of key-value pairs into YAML

```yaml
name: Varun
age: 21
hobbies: # It contains a list in YAML it is written as this:
    - singing
    - dancing
    - guitar
# This indentation (spacing) is very important as we do not have {} brackets to denote where does this key-value pair belong

# We can put numbers as strings using "" example
password: "12345"
```

That's it, it is this simple to write a YAML file. You can see it is similar to Python Dictionary with key-value pair but does not include `{}` brackets.

---

# 📍Docker Compose File Structure

Configuration File name: `docker-compose.yml` should always be named this by convention otherwise `docker-compose` commands will not recognize the file.

```yaml
version: '3'  # Specify the version of Docker Compose syntax

services:
  service_name1:  # Name of the first service (example: frontend)
    image: image_name1:tag  # Docker image for the service
    ports:
      - "host_port:container_port"  # Map host port to container port
    environment:
      ENV_VARIABLE1: value1  # Environment variables for the service

  service_name2:  # Name of the second service (backend or database)
    image: image_name2:tag
    volumes:
      - volume_name:container_path  # Mount a volume to the container
    depends_on:
      - service_name1  # Depend on another service

networks:
  network_name:  # Define custom networks if needed
    driver: bridge

volumes:
  volume_name:  # Define named volumes for data persistence
```

* `version`: Specifies the version of the Docker Compose syntax being used.
    
* `services`: Defines the various services (containers) that make up your application. Each service has its configuration options, including the Docker image to use, ports to expose, environment variables, and more.
    
* `image`: Specifies the Docker image to use for the service, along with an optional tag.
    
* `ports`: Maps host ports to container ports, allowing you to access the service from outside the container.
    
* `environment`: Sets environment variables for the service.
    
* `volumes`: Defines volumes that can be mounted to containers, allowing data persistence.
    
* `depends_on`: Specifies the order in which services are started. Services listed here will start before the service using this option.
    
* `networks`: Defines custom networks if needed. Networks allow communication between containers.
    
* `volumes`: Defines named volumes that can be used for data persistence across containers.
    

We will discuss docker volumes and docker networks in the next upcoming blog.

📝Remember that the structure can be more complex based on the needs of your application. You can have multiple services, networks, and volumes defined in a single Docker Compose file. The structure helps orchestrate the deployment and management of your multi-container application.

Now that we know how to write a docker-compose.yml file. Let's do a hand's-on project by containerizing and deploying a **2-tier flask to-do web application** using **docker-compose** this will make things more clear.🚀

---

# 📍2-Tier Flask Web Application

We will be containerizing a two-tier Flask web application, it is a simple to-do app. We will make 2 containers:

* Container 1: Contains the front end and the backend
    
* Container 2: Contains the database that will be running — MySQL, in our case.
    

Here is the File Structure for the project:

📁two-tier-flask-app (Project folder/directory name)

* 📄app.py (backend)
    
* 🐳Dockerfile
    
* 🐳docker-compose.yml
    
* 📄requirements.txt (Contains all the dependencies)
    
* 📁templates (directory for the front end)
    
    * 📄index.html (Basic frontend)
        

This will be our project file structure. Copy the code into their respective file.

`Step 1`: Create a file `app.py` and copy this code in it:

```python
import os
from flask import Flask, render_template, request, redirect, url_for
from flask_mysqldb import MySQL

app = Flask(__name__)

# Configure MySQL from environment variables
app.config['MYSQL_HOST'] = os.environ.get('MYSQL_HOST')
app.config['MYSQL_USER'] = os.environ.get('MYSQL_USER')
app.config['MYSQL_PASSWORD'] = os.environ.get('MYSQL_PASSWORD')
app.config['MYSQL_DB'] = os.environ.get('MYSQL_DB')

# Initialize MySQL
mysql = MySQL(app)

@app.route('/')
def index():
    cur = mysql.connection.cursor()
    cur.execute('SELECT * FROM tasks')
    tasks = cur.fetchall()
    cur.close()
    return render_template('index.html', tasks=tasks)

@app.route('/add', methods=['POST'])
def add():
    new_task = request.form.get('new_task')
    cur = mysql.connection.cursor()
    cur.execute('INSERT INTO tasks (task) VALUES (%s)', [new_task])
    mysql.connection.commit()
    cur.close()
    return redirect(url_for('index'))

if __name__ == '__main__':
    app.run(host='0.0.0.0', port=5000, debug=True)
```

`Step 2`: Create a file `requirements.txt`

```plaintext
Flask==2.0.1
Flask-MySQLdb==0.2.0
mysqlclient==2.1.0
```

`Step 3`: Create a Dockerfile for the backend `app.py`

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

---

# 📍Docker Compose for a 2-Tier application

`Step 4`: Create `docker-compose.yml` file

```yaml
version: '3'
services:
  
  backend:
    build:
      context: .
    ports:
      - "5000:5000"
    environment:
      MYSQL_HOST: mysql 
      MYSQL_USER: root
      MYSQL_PASSWORD: root_password # Make sure to add a root password
      MYSQL_DB: todo_db  # Create a new database for the to-do app
    depends_on:
      - mysql

  mysql:
    image: mysql:5.7
    environment:
      MYSQL_ROOT_PASSWORD: root_password # Make sure to add your root password
      MYSQL_DATABASE: todo_db  # Create a new database for the to-do app
      MYSQL_USER: user_name # Make sure to add your username, password
      MYSQL_PASSWORD: user_password
    volumes:
      - mysql-data:/var/lib/mysql

volumes:
  mysql-data:
```

We will be seeing about Docker volumes in my next blog. For now, just understand that docker volumes are created so that the container data can be persisted in our system if the container gets crashed.

`Step 5`: Create a templates directory and inside it create an `index.html` file

```xml
<!DOCTYPE html>
<html>
<head>
    <title>To-Do List App</title>
</head>
<body>
    <h1>To-Do List</h1>
    <ul>
        {% for task in tasks %}
            <li>{{ task[1] }}</li>
        {% endfor %}
    </ul>
    
    <form action="/add" method="post">
        <input type="text" name="new_task" placeholder="Add a new task">
        <input type="submit" value="Add">
    </form>
</body>
</html>
```

---

# 📍Deploying a Two-Tier Flask app using docker-compose

Now that our project file structure is ready, let's containerize and deploy the Flask app:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692024903609/a543d8a9-ef69-4196-a393-82fb3dcd0041.png align="center")

Run: `docker-compose up -d`

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692025046374/22eba48e-acf3-48c9-9515-2db283930e5d.png align="center")

When you see this output:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692025158556/3b8e4680-6668-4e9a-900b-c0a2b413610d.png align="center")

This means your container is up and running to see our deployed Flask application:

Go to Browser and search: `localhost:5000`

In my case I am using an AWS EC2 instance, therefore for me `ec2_ip_address:5000`

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692025306383/48c3dfea-07ae-45cc-89ef-979d571bc1c9.png align="center")

You will get this error saying the database 'todo\_db' does not exist.

For some reason, it did not create a MySQL database, to avoid this we can do:

Create a todo\_db database manually while the MySQL container is running.

`Step 1`: Press the `Ctrl + c` key to stop the program.

`Step 2`: `docker-compose up -d` This will run the program in a detached mode in the background this will help us give the command terminal:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692025689330/34513adc-50cf-46a0-b8e3-69adf18a175e.png align="center")

You can see that the containers are running. Let's get inside the MySQL container using the command:

`docker exec -it <mysql_container_id> /bin/bash`: This will give us a bash shell to interact with the MySQL container.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692025826398/f1c9e875-d76f-4ba2-9062-fd4d836c4d0c.png align="center")

Login to the MySQL container from the bash using `mysql -u root -p`

Enter the root password in our case it is `root@123`

Let's see the list of databases:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692026160605/f4d87802-309c-4247-82b6-c722f5501873.png align="center")

As we can see there is no todo\_db database created. Let's create:

MySQL query to create the database: `create database todo_db;`

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692026299417/1a334a09-6981-4906-b1b6-b96710ee278f.png align="center")

Now that the database is created let's refresh and see our deployed application:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692026364376/cc7d804f-5690-4222-aa8a-ecb83abe092d.png align="center")

Now it is giving an error called "Table 'todo\_tasks' does not exist"

Let's create this table:

MySQL query to create a table: `create table todo_db.tasks (task varchar(255))`

(If you don't know this just do a simple Google search. It is ok we learn as we practice and build more projects.)

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692026493206/484ac299-b4f6-4d01-b813-6c560f187739.png align="center")

Let's refresh and see our Flask application:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692026670528/5b25b012-31b5-41b2-bb5b-75550db46771.png align="center")

Yay!!!🤩 Our 2-tier Flask To-do web application has been successfully deployed.

🎉Congratulations you have containerized a 2-tier we application using docker-compose. You can add this project to your resume!🥳

📝Note: Initially, some might find this process challenging. If you encounter errors, don't be discouraged; simply search for them online or consult resources like ChatGPT to troubleshoot effectively.

Even I faced challenges with my first 2-tier project using docker-compose and struggled with errors for days. Persevere and continue experimenting eventually, you'll achieve a successful deployment.🖊

---

# 📍Conclusion

Now that you've successfully deployed a two-tier application as part of your practice, you can further enhance your skills by selecting any existing 2-tier or 3-tier application. Transform it into a containerized setup by crafting Dockerfiles and configuring docker-compose files, all while mastering the art of troubleshooting. This will enable you to enrich your resume/portfolio with diverse projects. This approach sharpens your expertise in Docker and equips you to adeptly containerize intricate microservices architectures.

Thank you for reading this blog! 📖 Hope you have gained some value.

If you enjoyed this blog and found it helpful, please give it a like 👍, share it with your friends, do share your thoughts, and give me some valuable feedback.😇 Don't forget to follow me for more such blogs! 🌟

---

# 📍References

* [StackOverflow](https://stackoverflow.com/)
    
* [ChatGPT](https://openai.com/chatgpt)
    
* [Google](http://google.com)