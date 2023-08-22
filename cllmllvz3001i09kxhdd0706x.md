---
title: "CI/CD pipeline for 2-Tier Flask Todo Web Application"
datePublished: Tue Aug 22 2023 17:47:04 GMT+0000 (Coordinated Universal Time)
cuid: cllmllvz3001i09kxhdd0706x
slug: cicd-pipeline-for-2-tier-flask-todo-web-application
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1692726316579/f7d0bfc8-ae03-4f31-b402-59dd2b5ee578.png
tags: jenkins, cicd, devops-journey, 90daysofdevops, day27

---

---

# 📍Introduction

🚀Welcome to my Jenkins blog series, where we'll dive into crafting a declarative pipeline for a 2-tier Flask Todo Web Application with MySQL. Follow our step-by-step journey as we set up a holistic pipeline, covering cloning, building, DockerHub integration, and deployment. Let's get started!💡

To ensure a seamless experience, make sure to check out my previous blog, which will help you with an easy understanding and implementation of the steps outlined in this blog:📚

[Introduction to Jenkins Pipelines: Streamlining Your Development Workflow](https://varunmargam.hashnode.dev/introduction-to-jenkins-pipelines-streamlining-your-development-workflow)

---

# 📍Pipeline Structure

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692724986393/f3d91423-dd2e-4246-b323-814829b68dff.png align="center")

---

# 📍Declarative Pipeline for 2-Tier Flask App

`Step 1`: Fork this GitHub repository to your GitHub account:

Repository URL: [https://github.com/Varunmargam/2-tier-flask-todo-cicd](https://github.com/Varunmargam/2-tier-flask-todo-cicd)

`Step 2`: Create an **AWS EC2 instance** with **Ubuntu AMI**, select **t2.medium**, and allow "**HTTPS**, and **HTTP traffic from the internet"**. This is for the app, and the pipeline to run smoothly.

`Step 3`: Installation and setup of all the necessary services: You can skip if you have docker and Jenkins already installed

```bash
# Installing docker & docker-compose
sudo apt update
sudo apt install docker.io -y # -y flag means yes permission.
sudo apt install docker-compose -y
sudo systemctl enable docker

# Installing Java for Jenkins
sudo apt update
sudo apt install openjdk-17-jre
java -version # verify java installation

# Installing Jenkins
curl -fsSL https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key | sudo tee \
  /usr/share/keyrings/jenkins-keyring.asc > /dev/null
echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
  https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null
sudo apt-get update
sudo apt-get install jenkins

# Allow permissions for jenkins user to execute docker commands
sudo usermod -aG docker jenkins # adding jenkins user into docker group.
sudo systemctl reboot # Or you can stop and start the instance.
```

The Setup for our project has been completed.

`Step 4`: Go to the "**security**" section of your **EC2 instance**, select the **security group Id**, and click on "**Edit Inbound rules**". Make sure you allow traffic from Anywhere IPv4 to ports `8080` (for Jenkins), `5000`(for the Flask app), and `3306`(for MySQL).

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692699199534/acd60cac-50ac-4e2e-8d4c-cccf40db079b.png align="center")

Click on "**Save rules**".

`Step 5`: Go to your browser and type **public\_IP\_address** of your aws instance\*\*:8080\*\* `ec2__public_ip:8080` and click on "New Item".

Give the job name: "**Flask-todo-app-cicd**", select "**Pipeline**", and click "**Ok**". We will be making a declarative pipeline.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692699682076/a618ec3e-9a7d-4412-ae98-86fb73e0631d.png align="center")

`Step 6`: Give a description:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692699847839/5c1df233-c832-4838-8ae0-bf2494d9da0e.png align="center")

`Step 7`: Check the "**GitHub project**" option and in the "**Project url**" field enter the URL for the GitHub repository which contains this Flask Web Application :

Copy the Forked GitHub repository URL:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692700164843/4484100b-c2f5-4de6-a6db-b476cf93beac.png align="center")

`Step 8`: Click on the "**Advanced**" dropdown and add "**Display name**" as "**Flask Todo Web App**"

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692700285605/d1d4e226-1c89-4e06-bd3a-6df4303ecaf8.png align="center")

`Step 9`: Scroll down to the "**Advanced Project Options**" click on the "**Advanced**" dropdown and add the same "**Display name**" as "**Flask Todo Web App**"

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692700408220/bcbb1c0e-d72c-4047-9cbb-9377dc8f6bf5.png align="center")

`Step 10`: Come to the "**Pipeline**" section and add this pipeline script:

This pipeline script is to test the working of the pipeline ( optional )

```java
pipeline{
    agent any

    stages{
        stage("Clone"){
            steps{
                echo "Code cloned"
            }
        }
        stage("Build"){
            steps{
                echo "Code built"
            }
        }
        stage("Push to Repository"){
            steps{
                echo "docker image pushed to the DockerHub repository"
            }
        }
        stage("Deploy"){
            steps{
                echo "Flask app has been deployed"
            }
        }
    }
}
```

`Step 11`: Click on Save, now our Pipeline has been created to test try and run this pipeline by clicking on "**Build Now**".

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692700888219/3b6574cf-b5b6-4dcc-add1-159bb7e9ec1c.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692700920476/74d9ef1e-187b-4eb2-8ddc-f94b94ec6f7f.png align="center")

Our first build of the pipeline has been successful.

Now let's define the steps of the stages one by one.

`Step 12`: For the stage ("Clone") we will have to write the Groovy syntax to clone the Git repository from GitHub:

1. Google "**groovy syntax for git clone**", and I got this result from StackOverflow:
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692701240868/9e1e5e03-289d-4910-b935-af0f1ebb93cd.png align="center")
    
2. Copy the **HTTP** URL of the GitHub repository:
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692701412854/1ab65dce-f7c8-458c-ae37-1c6db33cf3b9.png align="center")
    

Type the groovy syntax for git clone:

```java
stage("Clone"){
    steps{
        git url: 'https://github.com/Varunmargam/2-tier-flask-todo-cicd.git', branch: 'master'
    } // branch is to mention the branch we want to clone, here in our case 'master'
}
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692701778486/d3416233-99ed-49f4-b300-c5064278d787.png align="center")

`Step 13`: Click on "**Save**" and start the build of the pipeline.

Instead of running the whole build process after we have defined all the stages. It is always a good practice to define the steps in 1 stage and check if the build process is running successfully or not. This helps in troubleshooting if the build fails.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692702000455/167e3864-a4b2-4a0d-91a1-201f923aa33e.png align="center")

You can see our **#2** build has been successful, check the logs of the "**Clone**" stage by clicking on it:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692702094726/2dbbedd0-124c-4c56-9ff4-0d051f341e42.png align="center")

It will display the logs of that particular stage:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692702146539/82dbafff-1627-4800-a411-626a53d5b0ec.png align="center")

You can see in the logs it has cloned the Git repository inside the `/var/lib/jenkins/workspace/` directory:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692702284694/5f76d699-302d-4562-86ec-4db5c2b85a0f.png align="center")

You can see the Flask-todo-app-cicd is a Git repository with `ls -a` command. It has a `.git` file.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692702429690/bd83544c-2e96-4fd0-b468-cd2ceac4f7de.png align="center")

`Step 14`: Define the Build process, using the command `docker build . -t flask-todo-app-cicd`. To execute shell commands inside the Groovy syntax file use `sh "shell command"`:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692702827583/abebfcc8-4c70-4c0c-8f44-b152f2d7bd72.png align="center")

Save this and run the pipeline to check if the build stage is successful or not.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692702941504/e1e21773-3bb5-485b-8781-99f2b296b811.png align="center")

You can check the Build stage "**Logs**" or the "**Console** **Output**". Executing the `docker images` command to verify the built images:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692703101920/e94f9ef3-d0a4-4923-905d-b7ca97121203.png align="center")

`Step 15`: Define the "**Push to Repository**" stage, the steps to push this Docker image we have built in the "**Build**" stage to the DockerHub from the terminal are:

1. **Login to the DockerHub**: `docker login -u <user_name> -p <password>`
    
    `<user_name>` and `<password>` are the credentials to log in to DockerHub.
    
2. **Rename the image in the format username/image\_name**: `docker tag <image_name> username/<image_name>:latest` "latest" represents the version of the image.
    
    Since the images in the DockerHub repository are named in the above format.
    
3. **Push the image to DockerHub**: `docker push <new_image_name>:latest`
    

`Step 16`: To execute the "**Login to the DockerHub**" step via Jenkins, we have to first give the DockerHub credentials to Jenkins.

* Go to **Dashboard** and click on "**Manage Jenkins**":
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692703819898/b3cb5cf3-023c-408d-b4f6-f7ebcde8edbb.png align="center")
    
* Go to the "**Security**" section and click on "**Credentials**":
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692703885605/41ed358a-9fdd-4587-8b7b-04905abfba31.png align="center")
    
* Click on "(**global)**":
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692704160859/f575cd7f-9869-44c7-b8b0-cbd58e1e7624.png align="center")
    
* Click on "**Add Credentials**" at the top right:
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692703960264/35925d62-a047-4f1a-b748-bb45abe017b9.png align="center")
    
* Enter the Username and Password of your DockerHub Account:
    
    Enter **ID** as "**DockerHub**" and give **Description** as "**These are DockerHub credentials.**"
    
    Your DockerHub credentials that contain the username and password for your DockerHub account will be identified using this **ID** by Jenkins.
    
* Click "**Create**":
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692708614566/5d00a8cb-bad1-4ab0-909c-373809c4dcb2.png align="center")
    
* Your DockerHub credentials are created with the ID "**DockerHub**".
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692708865242/3e4a2d56-a63a-4792-bd57-0029c881c72d.png align="center")
    

`Step 17`: Go to your "**Flask-todo-app-cicd**" pipeline and click on "**Configure**" to define the "**Login to the DockerHub**" step inside the "**Push to Repository**" stage.

```java
/* The Groovy Syntax has a function called withCredentials() that passes
 the credentials are passed as arguments to the function and inject into the
 scope of this function. */
stage("Push to Repository"){
    steps{
        withCredentials([usernamePassword(credentialsId:"DockerHub",passwordVariable:"DockerHubpass",usernameVariable:"DockerHubUser")]){
            sh "docker login -u ${env.DockerHubUser} -p ${env.DockerHubPass}"
        }
    }
}
```

* `withCredentials()`: Groovy function that accepts credentials as arguments to be used inside the scope of its function.
    
    Inside this `withCredentials()` function we are passing a list of credentials mentioned in `[]`.
    
* `usernamePassword()`: This is a Groovy function used to pass the credentials.
    
* `credentialsId:"DockerHub"`: Key value pair.
    
* `passwordVariable:"DockerHubpass"`: Here we are defining a variable for the password with the name `"DockerHubpass"` same is for this `usernameVariable:"DockerHubUser"`.
    
* `sh "docker login -u ${env.DockerHubUser} -p ${env.DockerHubPass}`: Here we are accessing the credentials passed as arguments to this function, `env` here is the environment variable.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692712030796/7fc7500c-1c78-473b-ad5f-dc1c8746e838.png align="center")

`Step 18`: Enter these steps, "**Save**" these changes, and start the "**Build**" process. This is to ensure that Jenkins can successfully log in to DockerHub.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692712482508/35fc0498-8d31-4548-9729-64bfb9940965.png align="center")

You can see that the build has been successful. Check the "**Console Output**" of this **#4** build.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692712588067/9cd88e45-18d0-4e11-a245-a7b83920f0dd.png align="center")

As you see in the above "**Console Output**" "**Login Succeeded**".

`Step 19`: Let's start defining the "**Rename the image in the format username/image\_name"** step and the **"Push the image to DockerHub"** step.

```java
stage("Push to Repository"){
    steps{
        withCredentials([usernamePassword(credentialsId:"DockerHub",passwordVariable:"DockerHubpass",usernameVariable:"DockerHubUser")]){
            sh "docker login -u ${env.DockerHubUser} -p ${env.DockerHubPass}"
            sh "docker tag flask-todo-app-cicd ${env.DockerHubUser}/flask-todo-app-cicd:latest"
            sh "docker push ${env.DockerHubUser}/flask-todo-app-cicd:latest"
        }
    }
}
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692713276790/51bd00df-d9ca-40c3-81cf-1a489d2dc521.png align="center")

`Step 20`: "**Save**" this and click on "**Build Now**".

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692713372668/1514ae96-4868-46d6-972d-85cae1136e73.png align="center")

As you can see the **#5** build has been successful now let's see the "**Console Output**" and see if the Docker image has been pushed to DockerHub or not.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692714639450/c99c41b2-f052-4b51-a3df-9f1d04d44085.png align="center")

You can see the image `flask-todo-app-cicd` has been pushed to my DockerHub account.

Now my original `docker-compose.yml` was this:

```dockerfile
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
      MYSQL_PASSWORD: root@123
      MYSQL_DB: todo_db  # Create a new database for the to-do app
    depends_on:
      - mysql

  mysql:
    image: mysql:5.7
    environment:
      MYSQL_ROOT_PASSWORD: root@123
      MYSQL_USER: varun
      MYSQL_PASSWORD: varun@123
    volumes:
      - mysql-data:/var/lib/mysql
      - ./init.sql:/docker-entrypoint-initdb.d/init.sql

volumes:
  mysql-data:
```

Here, the backend service is building the image from the contents of my project. But I want to use the image that we have pushed to the DockerHub. For that, I have updated my `docker-compose.yml` file to this:

```dockerfile
version: '3'
services:
  
  backend:
    image: "varunmargam/flask-todo-app-cicd:latest"  # Use the image from DockerHub
    ports:
      - "5000:5000"
    depends_on:
      - mysql

  mysql:
    image: mysql:5.7
    environment:
      MYSQL_ROOT_PASSWORD: root@123
      MYSQL_USER: varun
      MYSQL_PASSWORD: varun@123
    volumes:
      - mysql-data:/var/lib/mysql
      - ./init.sql:/docker-entrypoint-initdb.d/init.sql

volumes:
  mysql-data:
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692715083484/5fa379cb-5e4e-4531-b1a8-179e335083ab.png align="center")

`Step 21`: Define the "**Deploy**" stage using these commands:

```java
stage("Deploy"){
    steps{
        sh "docker-compose down && docker-compose up -d"
    }
}
```

While building the pipeline multiple times we have to stop the running containers and remove these stopped containers from the previous build. To achieve this we first execute `docker-compose down` and then execute `docker-compose up -d`.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692715407778/e802eaf6-142d-482d-994c-e98f663479d1.png align="center")

`Step 22`: "**Save**" this and build the pipeline:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692715519661/bf5bf6d6-835c-4c7a-871e-8d68c820dd5c.png align="center")

As you can see our **#6** build has been successful, which means our application has been successfully deployed.

Go to your browser and type this URL: `ec2_public_ip:5000`

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692715615931/92c82701-813b-4821-906e-4a3b8c31d442.png align="center")

You can add some tasks to the list:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692715654096/9c254d7c-2b82-4cf2-ac2e-9f394afb06f8.png align="center")

And can click on checkboxes to remove the completed task:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692715706254/082f4012-42fb-4009-8620-e5ba61ae6f37.png align="center")

Let's also add Webhooks to the pipeline so that we can achieve Continuous Deployment i.e. it will **automatically** trigger the Build pipeline as soon as changes are committed to the code. Thereby achieving "**Continuous Integration and Continuous Deployment**".

`Step 23`: Go to your Forked GitHub repository, click on "**Settings**", and click on "**WebHooks**" at the left:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692716750945/5f40646f-5847-4b0b-a0d3-cc6c66986372.png align="center")

`Step 24`: Add the Jenkins Web Interface URL in the "**Payload URL**" field in the format `jenkins_web_url/github-webhook/` as you can see in the above image. Click on "**Send me everything**" in the events section and click on "**Add webhook**".

You will see your webhook has been created and is active if it shows a "green tick" mark:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692717037700/c9f31bfd-43ce-47b9-b30c-add35ffdcac3.png align="center")

If you do not see the tick refresh the page.

`Step 25`: Go to the Jenkins Web Interface **Dashboard**, click on "**Configure**", go to the "**Build Triggers**" section, and check on "**GitHub hook trigger for GITScm polling**".

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692716621908/d8fa7c5d-3b2e-44f6-b84e-f497e7eba31b.png align="center")

Click on "**Save**", and adjust your GitHub tab and the Jenkins tab side by side like this:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692717245784/3000da2f-4024-40cb-87d0-f0502d89fa03.png align="center")

`Step 26`: Make some changes to my code and commit them to verify whether the build of the pipeline gets automatically triggered or not.

Go to the `index.html` file inside the `templates` folder and click on "`edit`" which will be at the left corner represented by a "**pencil**".

I will be making changes in the &lt;h1&gt; tag so that the changes are easily visible:

Originally the &lt;h1&gt; tag contained a "To-Do **List**"

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692717708250/06213285-0419-4a5b-905f-87d2b23c8c4b.png align="center")

The change I made was:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692717803147/83fd51be-0b42-42e9-8b02-bb0685bd60e5.png align="center")

And I committed those changes:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692717884004/1555314c-0095-4225-8fd5-3aea674af0da.png align="center")

You can see the build process has been started as soon as I committed those changes

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692717938852/54312750-fdfd-48d8-8c34-3755d6310c88.png align="center")

The build process has been successful. Let's see if the changes have been reflected in the updated app:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692718033386/67579750-4623-49ae-8f99-424786e60cdc.png align="center")

Yay!!🥳 The changes have been successfully implemented, indicating that our pipeline setup aligns with our intended configuration.

( Apology for the spelling mistake😅)

You can also trigger this CICD pipeline without using the Jenkins Web Interface by adding the pipeline script inside the file named Jenkinsfile along with your project code in the GitHub repository.

This way whenever you will commit the changes to the code in GitHub the Webhook will trigger the Jenkins build of the Jenkins pipeline and when Jenkins will locate and read the Jenksfile it will execute the stages as defined in the Jenkinsfile.

( My repository code already contains the Jenkinsfile so you can skip to the step )

To upload the Jenkinsfile to your GitHub repo follow these steps:

`Step 1`: Go to your GitHub repository, click on "**Add file**", and click "**Create new file**"

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692718699528/01210c75-f538-4c2f-9eae-e01871a4cc6f.png align="center")

`Step 2`: Go to your Jenkins Web interface, click on "**Configure**", copy the "**Pipeline script**", and paste it into this GitHub file.

```java
pipeline{
    agent any
    
    stages{
        stage("Clone"){
            steps{
               git url: 'https://github.com/Varunmargam/2-tier-flask-todo-cicd.git', branch: 'master' 
            }
        }
        stage("Build"){
            steps{
                sh "docker build . -t flask-todo-app-cicd"
            }
        }
        stage("Push to Repository"){
            steps{
                withCredentials([usernamePassword(credentialsId:"DockerHub",passwordVariable:"DockerHubPass",usernameVariable:"DockerHubUser")]){
                    sh "docker login -u ${env.DockerHubUser} -p ${env.DockerHubPass}"
                    sh "docker tag flask-todo-app-cicd ${env.DockerHubUser}/flask-todo-app-cicd:latest"
                    sh "docker push ${env.DockerHubUser}/flask-todo-app-cicd:latest"
                }
            }
        }
        stage("Deploy"){
            steps{
                sh "docker-compose down && docker-compose up -d"
            }
        }
        stage("Remove unused images"){
            steps{
                sh "docker image prune -af"
            }
        }
    }
}
```

Name the file "Jenksfile" at the top:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692718828473/104994d2-446f-4d3e-ae43-65c04c2455bf.png align="center")

Do not commit the changes now

`Step 3`: Go to your Jenkins Web Interface, go to your pipeline, click on "**Configure**", scroll down to the "**Pipeline**" section, delete the "**Pipeline** **Script**", in the Definition field click on the dropdown, and select "**Pipeline script from SCM**". SCM - Source Code Management.

* In the "SCM" section select "Git".
    
* In the "**Repository"** section add the **HTTP URL** inside the "**Repository URL**" field.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692719157465/c8012f95-099e-4b66-a193-e50d3d3eb82d.png align="center")

* Scroll down to the "**Branches to build**" section and type "**\*/master**" and click "**Save**"
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692719396607/79c80668-e481-40e1-98fb-023dd64a26aa.png align="center")

`Step 4`: Again adjust the two windows like this:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692719462911/ea255bdc-694d-4916-a12a-dfb9c189ddaf.png align="center")

`Step 5`: Commit the changes:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692719504789/0b3d94b5-b9ac-450a-a3cf-161a020ce204.png align="center")

You can see the build process has been triggered via webhook as soon as the changes were committed:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692719571972/cac41845-88c0-4c31-bba4-de32888d8170.png align="center")

But you can see that an additional stage has been added at the beginning of "Declarative **Checkout SCM**" It means that Jenkins went to GitHub and did Declarative checkout i.e. **located** the Jenkinsfile and then started the build process of the pipeline as defined in the **Jenkinsfile**.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692719854670/40590bc7-e794-4538-a988-15e0fc5d440e.png align="center")

Now if Jenkins keeps on building new containers, the images run by previous containers will be remained unused in the system and will occupy space. This may cause the memory to fill in the pipeline and keeps executing after a certain number of times.

Let's add another stage in the Pipeline that removes the unused images using the command:

`docker image prune -af`

I went to my GitHub repository and edited **Jenkisfile** by adding the "**Remove unused images**" stage.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692720107739/5069df17-beb0-4b3f-b76a-aca9826a5d8d.png align="center")

And committed to those changes:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692720189921/63dddbe2-e521-47b7-9dc8-6e510bf1cd62.png align="center")

This commit will trigger the pipeline build:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692720234509/ae839f2d-b674-4aaf-89cb-9236d952f852.png align="center")

You can see now a new stage has been added at the end that removes the unused images from the system:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692720297830/1883e116-ed7e-4df2-a9c1-2d0614cf2406.png align="center")

The images created due to the above build:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692720349312/991149dc-9ae9-45a3-824a-ee5a2f6b45dc.png align="center")

Again built the pipeline:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692720387399/2781865b-a5fc-4505-bc2e-4c95f6fd4470.png align="center")

Now you can see the previous images were removed and only the images created in the above build exist in the system:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692720464499/d8a0a38d-9161-4293-88dd-f1a9bf2235db.png align="center")

Congratulations!!🥳 We have successfully created a Declarative pipeline for a 2-tier Flask Todo Web Application.🎉

---

# 📍Conclusion

As we conclude this blog, you've not only gained insights into creating a robust pipeline but also learned how to streamline the process with Git integration and SCM synchronization. Your journey toward mastering Jenkins automation has just begun. Keep on practicing and craft more pipelines for different applications.🚀🌟

Thank you for reading this blog! 📖 Hope you have gained some value. In the future blog, we will be creating and exploring Jenkins pipelines.

If you enjoyed this blog and found it helpful, please give it a like 👍, share it with your friends, share your thoughts, and give me some valuable feedback.😇 Don't forget to follow me for more such blogs! 🌟

---

# 📍Reference

* [ChatGPT](https://openai.com/chatgpt)
    

---