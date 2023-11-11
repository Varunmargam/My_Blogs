---
title: "Astarix Assignment: Containerizing MERN Stack Application on AWS and Crafting CICD Pipeline."
datePublished: Fri Nov 10 2023 18:30:00 GMT+0000 (Coordinated Universal Time)
cuid: cloubcx04000008ia9gqi88h7
slug: astarix-assignment-containerizing-mern-stack-application-on-aws-and-crafting-cicd-pipeline

---

---

# 📍Docker & Docker-Compose

`Step 1`: Launch an AWS EC2 instance of type t2.medium.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699710602927/32032c16-bebd-46c9-9d29-7f0cbfca0662.png align="center")

`Step 2`: Install Docker and Docker-Compose and permit the Ubuntu user.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699710678438/5e43fe0d-1ddf-4af5-b07b-03cd8ff974cd.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699710686438/95538ba6-7d7e-44c7-b24e-a7a1a682b8ac.png align="center")

**Giving user permission:**

```bash
sudo usermod -aG docker ubuntu
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699711452592/b212b39b-28a5-4d59-b806-b925001cd960.png align="center")

`Step 3`: Clone this GitHub repository:

[https://github.com/Varunmargam/idurar-erp-crm](https://github.com/Varunmargam/idurar-erp-crm)

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699710756586/33b62bf1-a77a-48e7-8f45-9d192ca9146e.png align="center")

`Step 4`: Create a Dockerfile inside the front end and the backend directory.

Backend

```dockerfile
FROM node:16

WORKDIR app/backend

COPY package*.json ./

RUN npm i

COPY . .

EXPOSE 8888

CMD ["npm","run","dev"]
```

Frontend

```dockerfile
FROM node:16

WORKDIR app/frontend

COPY package*.json ./

RUN npm i

COPY . .

EXPOSE 3000

CMD ["npm","run","dev"]
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699710914793/1ea358a4-9627-4448-b5bb-08cf65a53208.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699710930354/1be79769-8373-4d0d-88bf-7cb365a6084a.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699710936075/0d6d41a8-cd99-42f7-8ccf-2e03b49b0ae6.png align="center")

`Step 5`: Edit the `.env` file inside the frontend directory and the backend directory.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699711110533/5002b255-20a3-440b-bb9f-62a74b1f6afe.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699711118487/8a9c7dfb-aa50-4a9e-8b8c-e0a10fb72b79.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699711127536/7980ab3d-58b3-442c-b1fd-1e5c11c697b4.png align="center")

```plaintext
For the MongoURL replace the username and the password with your credentials.
```

`Step 6`: Edit the `vite.config.js` file inside the frontend directory.

Add `host: '0.0.0.0',` at line 24.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699711253587/2a60c2cf-901b-4f74-84b0-39989a435e25.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699711350964/a63b9772-6700-4dc6-8a5b-a346420812cf.png align="center")

`Step 8`: Build the Docker images from `idurar-erp-crm` directory.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699711604390/06431338-f4bf-4a18-b4d9-327078feb2e8.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699711614423/9293276f-8172-4dbe-a258-b09997947521.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699711676391/506a5f3b-ca5f-4f20-a813-3701c0efe393.png align="center")

`Step 7`: Create a Docker-compose file inside the `idurar-erp-crm` directory.

`docker-compose.yml`

```dockerfile
version: '3'
services:

  backend:
    build:
      context: ./backend
    ports:
      - "8888:8888"
    depends_on:
      - database

  frontend:
    build:
      context: ./frontend
    ports:
      - "3000:3000"

  database:
    image: mongo:latest
    ports:
      - "27017:27017"
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699711761483/32703014-0ae0-401a-a3ce-5d5c4c332584.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699711767411/5f33cb6d-8b72-417e-ba0f-3c5ba6b29b10.png align="center")

`Step 8`: Run the docker-compose file.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699711867620/95d45f40-de03-498e-a6b3-10f2b4ed8bf5.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699711908134/bd26e4f3-edcc-43e5-8792-4f85b10bb390.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699712012566/b23725a2-859a-4436-bd0f-7c94b741ed42.png align="center")

`Step 9`: Edit the inbound rules on the EC2 instance and give access to port 3000.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699712151979/5403c8c3-cb68-442d-a085-0725fe723802.png align="center")

`Step 9`: You can access the application on the browser at `http://<AWS_EC2_Pub_IP>:3000`

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699712188429/8b50c878-149f-4865-a271-598362fe573b.png align="center")

---

# 📍CI/CD

Install Jenkins on the EC2 instance and set up a Pipeline. You can refer to this blog for the same:

[https://varunmargam.hashnode.dev/cicd-pipeline-for-2-tier-flask-todo-web-application](https://varunmargam.hashnode.dev/cicd-pipeline-for-2-tier-flask-todo-web-application)

To execute the "**Login to the DockerHub**" step via Jenkins, we have to first give the DockerHub credentials to Jenkins.

* Go to **Dashboard** and click on "**Manage Jenkins**":
    
    * ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692703819898/b3cb5cf3-023c-408d-b4f6-f7ebcde8edbb.png?auto=compress,format&format=webp align="left")
        
    * Go to the "**Security**" section and click on "**Credentials**":
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692703885605/41ed358a-9fdd-4587-8b7b-04905abfba31.png?auto=compress,format&format=webp align="left")
        
    * Click on "(**global)**":
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692704160859/f575cd7f-9869-44c7-b8b0-cbd58e1e7624.png?auto=compress,format&format=webp align="left")
        
    * Click on "**Add Credentials**" at the top right:
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692703960264/35925d62-a047-4f1a-b748-bb45abe017b9.png?auto=compress,format&format=webp align="left")
        
    * Enter the Username and Password of your DockerHub Account:
        
        Enter **ID** as "**DockerHub**" and give **Description** as "**These are DockerHub credentials.**"
        
        Your DockerHub credentials that contain the username and password for your DockerHub account will be identified using this **ID** by Jenkins.
        
    * Click "**Create**":
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692708614566/5d00a8cb-bad1-4ab0-909c-373809c4dcb2.png?auto=compress,format&format=webp align="left")
        
    * Your DockerHub credentials are created with the ID "**DockerHub**".
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692708865242/3e4a2d56-a63a-4792-bd57-0029c881c72d.png?auto=compress,format&format=webp align="left")
        

This is the Jenkinsfile which you can add to the GitHub repository but need to execute this you need to push the changes made to the files in the previous section and commit those changes to GitHub which would not be a good practice since it contains sensitive information like MongoDB URL.

If you want to execute this CICD pipeline you would also have to modify the Docker-compose file in the build section as given below.

```plaintext
pipeline {
    agent any

    stages {
        stage("Clone") {
            steps {
                git url: 'https://github.com/Varunmargam/idurar-erp-crm.git', branch: 'master'
            }
        }

        stage("Build Backend") {
            steps {
                dir('backend') {
                    script {
                        // Assuming Dockerfile is in the backend directory
                        sh "docker build -t backend ."
                    }
                }
            }
        }

        stage("Build Frontend") {
            steps {
                dir('frontend') {
                    script {
                        // Assuming Dockerfile is in the frontend directory
                        sh "docker build -t frontend ."
                    }
                }
            }
        }

        stage("Push to Repository") {
            steps {
                withCredentials([usernamePassword(credentialsId: "DockerHub", passwordVariable: "DockerHubPass", usernameVariable: "DockerHubUser")]) {
                    script {
                        sh "docker login -u ${DockerHubUser} -p ${DockerHubPass}"

                        // Correcting the Docker push commands
                        sh "docker tag frontend ${DockerHubUser}/frontend:latest"
                        sh "docker push ${DockerHubUser}/frontend:latest"

                        sh "docker tag backend ${DockerHubUser}/backend:latest"
                        sh "docker push ${DockerHubUser}/backend:latest"
                    }
                }
            }
        }

        stage("Deploy") {
            steps {
                // Consider using docker-compose.yml file in your project directory
                sh "docker-compose up -d"
            }
        }
    }
}
```

```dockerfile
backend:
    image: "varunmargam/backend:latest"
    ports:
      - "8888:8888"
    depends_on:
      - database

  frontend:
    image: "varunmargam/frontend:latest"
    ports:
      - "3000:3000"
```