---
title: "Efficient CI/CD with Jenkins: Exploring Master-Slave Architecture and Agents"
datePublished: Wed Aug 23 2023 18:30:00 GMT+0000 (Coordinated Universal Time)
cuid: cllojrw9e000009mg7176hx5n
slug: efficient-cicd-with-jenkins-exploring-master-slave-architecture-and-agents
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1692844139443/fa2d8696-2341-43d2-9766-62b2fdda7c72.png
tags: jenkins, devops-journey, 90daysofdevops, jenkins-master-slave, day28

---

---

# 📍Introduction

Welcome to my Jenkins blog series! In this blog, we're delving into the core concepts of Jenkins Master-Slave Architecture, Jenkins Agents, and SSH-based connections. From theory to practice, we'll guide you through setting up a Master-Slave architecture and running a pipeline to deploy a Node.js application. By the end of this read, you'll be empowered with the knowledge and tools to optimize your development workflow. Let's embark on this enlightening journey together!

**Prerequisites**: Must be familiar with Jenkins, creating a Jenkins job, and Pipelines. You can refer to my blogs if you want to learn Jenkins or need a refresher.

---

# 📍Master-Slave Architecture in Jenkins

The Jenkins **Master-Slave (or Master-Agent**) architecture is a powerful framework that significantly enhances the Continuous Integration/Continuous Deployment (CI/CD) processes within software development. This architecture is designed to **optimize resource utilization**, **speed up build and testing cycles**, and **accommodate diverse environments**.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692802547983/7d3283e8-f03f-41fc-8b81-09c44bc648e3.jpeg align="center")

**Key Benefits:**

1. **Scalability:** The architecture scales horizontally by adding more agents, enabling parallel execution of tasks, and reducing overall pipeline duration.
    
2. **Resource Utilization:** Agents make optimal use of hardware resources by constantly engaging in tasks, and minimizing idle periods.
    
3. **Diverse Environments:** Organizations can test their applications on various platforms and configurations, ensuring compatibility and reliability.
    
4. **Security and Isolation:** Communication between the master and agents occurs within the internal network, mitigating external vulnerabilities.
    
5. **Reliability and Fault Tolerance:** If an agent fails, tasks can be rerouted to other available agents, ensuring pipeline continuity.
    

## **✔Practical Scenario**

Imagine a technology company developing a comprehensive web application. The application must be tested across different platforms (Windows, Linux, macOS) before deployment.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692802706945/09644f76-3da5-4c22-9b6d-fa388bbe1fe0.webp align="center")

By employing the Jenkins Master-Slave architecture:

* The Jenkins master server oversees the entire CI/CD process, from source code integration to deployment.
    
* Agents are configured on **Windows**, **Linux**, and **MacOS** machines, creating a versatile testing ecosystem.
    
* A developer commits code changes, triggering a Jenkins job.
    
* The master server determines the suitable agent for each task:
    
    * **Windows** agent for **Windows-specific tests**.
        
    * **Linux** agent for **backend testing**.
        
    * **MacOS** agent for **UI testing**.
        
* These tasks run in parallel across agents, drastically reducing testing time.
    
* As agents complete tasks, the master aggregates their results, generating comprehensive reports.
    
* The development team receives feedback promptly, enabling swift iteration and issue resolution.
    

## ✔Master Server

The Jenkins Master Server is the central control hub of the Jenkins Master-Slave architecture. It plays a pivotal role in orchestrating Continuous Integration/Continuous Deployment (CI/CD) processes, managing job execution, and providing an interface for administrators to configure, monitor, and analyze pipeline activities.

**Key Responsibilities:**

1. **Job Scheduling and Coordination:** The master server schedules and delegates tasks to the appropriate agents based on predefined configurations and triggers.
    
2. **Configuration Management:** It stores and manages job configurations, plugins, and global settings, ensuring consistency across the pipeline.
    
3. **User Authentication and Access Control:** The master server authenticates users, granting access based on roles and permissions defined within Jenkins.
    
4. **Monitoring and Reporting:** It tracks job progress, collects results from agents, and generates comprehensive reports to assist in analyzing pipeline health.
    
5. **Plugin Integration:** The master server supports a wide range of plugins that enhance functionality, enabling seamless integration with tools and services.
    
6. **Pipeline Definition:** Using Jenkinsfile or pipeline scripts, the master server defines complex workflows as code, ensuring consistent and repeatable processes.
    

**Key Considerations for Setting Up a Jenkins Master:**

1. **Installation:** Jenkins should be installed on a stable machine with adequate resources (CPU, memory, storage).
    
2. **Access Control:** Configure authentication mechanisms (e.g., LDAP, OAuth) and define user roles to secure access.
    
3. **Backup and Recovery:** Implement regular backups of Jenkins configuration, jobs, and plugins to prevent data loss.
    
4. **Plugins:** Install required plugins based on the project's needs (version control systems, build tools, notification systems).
    
5. **Scalability:** Opt for a scalable solution to accommodate growing pipeline demands, such as distributed file systems for artifacts.
    
6. **Security:** Secure the master server with firewalls, VPNs, and security best practices to protect sensitive data.
    

## ✔Agent Server

Jenkins Agents, also known as slaves, are worker nodes that execute tasks delegated by the master server. Agents run on separate machines or virtual instances and facilitate parallel execution of jobs, enhancing resource utilization and speed.

**Key Responsibilities:**

1. **Task Execution:** Agents perform the actual tasks defined in the CI/CD pipeline, such as building, testing, and deploying software.
    
2. **Environment Specialization:** Agents can be configured to specialize in specific platforms (Windows, Linux, macOS) or tasks (testing, deployment).
    
3. **Report Submission:** After completing tasks, agents report results, logs, and status back to the master server for compilation and analysis.
    
4. **Isolation:** Agents provide an isolated environment for task execution, preventing interference with other jobs or agents.
    
5. **Concurrency:** By leveraging multiple agents, jobs can be executed concurrently, reducing pipeline completion times.
    

**Setup Considerations:**

1. **Installation:** Agents should be set up on machines with compatible environments for the tasks they'll perform.
    
2. **Agent Communication:** Agents should establish secure communication with the master server, often using SSH keys or agent-to-master protocols.
    
3. **Resource Allocation:** Adequate resources (CPU, memory, storage) should be allocated to agents based on the types of tasks they'll handle.
    
4. **Scaling:** Organizations should have the flexibility to add or remove agents as pipeline demand fluctuates.
    
5. **Plugin Compatibility:** Agents might require specific plugins for tools or services they interact with; ensure compatibility.
    
6. **Security:** Agents should be protected by firewalls and network security measures to prevent unauthorized access.
    
7. **Agent Maintenance:** Regularly update and maintain agents to ensure their optimal performance and security.
    

To summarize, the Jenkins Master-Slave architecture empowers DevOps engineers with scalability, resource efficiency, and flexibility, ensuring swift development cycles, top-notch releases, and streamlined management of diverse testing and deployment scenarios. The Jenkins Master Server centrally manages job scheduling, configuration, and user interaction, necessitating stable installation with essential plugins and security measures. Jenkins Agents execute tasks in specialized environments, reporting results to the master. Agent setup involves allocating resources, ensuring secure communication, and task compatibility. Skillful configuration of the master server and agents establishes a robust CI/CD pipeline, effectively orchestrating software development and deployment.

---

# 📍Establishing SSH Key-Based Connections to Remote Servers

You can connect your local system to a remote server if you have access to its `Secure Shell (SSH) protocol` that runs on `Port 22`. This default port allows secure communication between a client and a server, enabling encrypted data exchange and remote access.

**📝Note**: While `port 22` is the standard port for SSH, it can be configured to use a different port if needed for security reasons or to avoid conflicts with other services.

Through SSH, you can execute desired operations on the remote server using commands. SSH facilitates communication with the server's kernel to perform these operations, granting access to hardware resources.

Remote connections are established using SSH logins, which come in two forms:

1. **Username and Password:** This method involves entering your credentials for remote server access.
    
2. **Key-Based:** Preferred widely in the industry, key-based logins offer enhanced security. In this context, we'll delve into the process of '**Establishing a Connection to a Remote Server using SSH Key-Based Login**.'
    

## ✔How SSH Key-Based Connections Work❓

**SSH key-based** connections involve a **private-public key pair** for **authentication**. The **public key** is shared with the **remote server**, while the **private key** remains on your **local system**. Upon connecting to the remote server, the private-public key pair is used for authentication. If the keys match, access is granted. This approach enhances security and eliminates password exchange. The process of **SSH key-based connection** can be visualized from the following diagram:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692804647087/fad3eb49-fac1-4660-a4b8-3a6d6a5fd0cb.png align="center")

The system trying to connect to the remote server is generally referred to as a **client**.

Now equipped with the foundational understanding of Jenkins' Master-Slave Architecture, the role of Jenkins Agents, and establishing connections through SSH, it's time to translate theory into action! 🚀Let's do some hands-on and implement this Jenkins Master-Slave Architecture followed by running a Jenkins Job.🛠️

---

# 📍Implementing Master-Agent Jenkins Architecture

We will run a pipeline for a Nodejs application.

`Step 1`: Create and launch two EC2 instances type t2.micro with Ubuntu AMI named **jenkins-master** and **jenkins-agent-1**. Connect to both instances and place them side by side.

`Step 2`: Set up and install Jenkins inside the "**jenkins-master**" instance.

Refer to this blog: [Introduction to Jenkins](https://varunmargam.hashnode.dev/jenkins-essentials-a-comprehensive-introduction-to-automation) from the Installation and Setup section.

`Step 3`: Install **Open JDK** in the **agent-1** instance since this is where the execution of the pipeline occurs.

`Step 4`: In the "**jenkins-master**" instance go inside the `.ssh` folder and execute the command `ssh-keygen`:

Keep pressing the "**Enter**" key for the prompts:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692812985300/f7af20e4-ac84-4024-8339-4142bb0b00fd.png align="center")

When you execute the `ls` command inside the `.ssh` directory you can see a key-pair has been generated named **id\_rsa** ( private key ) and **id\_rsa.pub** ( public key ):

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692813215320/8f93d69a-5f1e-4014-b9f9-d7765ec879e2.png align="center")

Now, we have to connect the master and agent instances using this SSH key pair.

We are establishing a connection to the agent from the master. Therefore, this master instance will have the private key and we have to give the agent instance the public key.

`Step 5`: Execute the command `cat id_rsa.pub` and copy the key:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692813519620/7bf02616-9783-46bb-b19d-06615ec727ef.png align="center")

`Step 6`: Go to your "**agent-1**" instance, and `cd` inside the `.ssh` location there is a `authorized_keys` where we have to store the public key. Therefore, execute the `vim authorized_keys` command.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692813710478/21fc0ec6-720c-475d-885a-da285f5383c7.png align="center")

`Step 7`: Paste the copied public key `id_rsa.pub` from the master inside this `authorized_keys` file, save, and exit the Vim editor using `:wq`.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692814034512/11613937-be71-48b2-b3e0-2378a1c7bd66.png align="center")

`Step 8`: Go to the master instance and execute the command ssh `ubuntu@agent_instance_public_ip` ubuntu is the hostname of the agent:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692814289217/90f7c5e1-cdb5-4113-92d8-75ef29741b7f.png align="center")

Your connection will be established and you will be inside the **jenkins-agent-1** SSH:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692814390573/2ce3f0b8-b693-45c6-8fbd-de653c57d5fc.png align="center")

You can execute the `exit` command and you will log out from the **agent-1** instance and you will be back in your **master** instance:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692814463518/4799c015-8799-4320-a78c-768d3666c1fb.png align="center")

Here, `172-31-10-210` is the private IP address of the "**jenkins-agent-1**" instance and `172-31-13-73` is the private IP of the "**jenkins-master**" instance.

`Step 9`: Go to your Jenkins Web Interface **Dashboard** and in the "**Set up a distributed build**" section select "**Set up an agent**".

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692814733576/3185d158-07a2-4634-869d-bcb8c12c01fb.png align="center")

`Step 10`: Give the node the name "**agent-1**" With this name Jenkins will identify our agent, select "**Permanent** **Agent**", and click on "Create".

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692814943513/63e51c75-1542-42e4-af9d-01251d506249.png align="center")

You will be directed to the configuration page of the node (agent):

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692815016494/52ce4485-6aca-417e-a09b-4114ba16edf5.png align="center")

`Step 11`: Add the **Description** and inside the "**Remote root directory**" give the path of your home directory i.e. "**/home/ubuntu**" This is where the agent will execute the job, we are specifying the working directory here.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692815186977/13d44cef-1c9e-4d3f-ab11-6eb273afbede.png align="center")

`Step 12`: In the Label section give the label "**dev**". This label is very important, Suppose we want to run a Django app then I can name this agent with the label **Django.** Since we will be running a Nodejs app you can label it "**Nodejs**".

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692815472249/384babd1-dc65-417d-baf1-d0b0a44b7228.png align="center")

The Usage section has 2 options:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692815927353/48bc2959-0678-4d73-b3d0-c05c4bd2c6f4.png align="center")

1. **Use this node as much as possible:** Since we have only one node we can keep this.
    
2. **Only build jobs with label expressions matching this node**: We select this when want our job to be executed on this node only when it matches the label.
    

`Step 13`: In the "**Launch method**" section select the option "**Launch agents via SSH**" since we want to connect to our agent via SSH.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692816040045/3107e67c-9912-4eda-8b10-9898033804aa.png align="center")

`Step 14`: In the "**Host**" field we have to give the **Host IP address** of the agent we want to connect.

Copying the Host IP of the "**jenkins-agent-1**" instance:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692816245337/4b689586-ae1a-4d0a-b9d0-4c65f2c0f307.png align="center")

Pasting it:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692816282095/b332576b-0274-4c0a-aa4e-a93428cd11a9.png align="center")

`Step 15`: Go to the "**Credentials**" section and click on "**Add**" and then on "**Jenkins**":

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692816370894/c997e80b-3954-4af5-992a-bb5e631e9430.png align="center")

A window will pop up to Add the Credentials i.e. the SSH key. Similar to how we did when we connected the **master** instance to the **agent** instance. We will provide the **private** key to **Jenkins** so that it can connect to the **agent-1** instance.

`Step 16`: In the "**Kind**" section select the "**SSH Username with private key**" option.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692816652446/4319ffdb-64e5-4a09-ae54-0d154d6c6753.png align="center")

`Step 17`: Give the **ID** "**agent-ssh-key**" and the **Description** to identify these credentials, and provide the **Username** of the agent instance i.e. **ubuntu**.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692816780585/92f7edf4-b117-4399-a7c5-ca8081ea127e.png align="center")

`Step 18`: Scroll down to the "**Private key**" section and select "**Enter directly**":

Here we will enter the private key from the **master** instance.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692816852438/316bf158-9dd7-4357-be8e-15908c9bad6d.png align="center")

`Step 19`: Execute the `cat id_rsa` command inside the `.ssh` folder:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692817006134/11359ddb-9c6c-43b5-b54b-d5d416071ed7.png align="center")

Copy the whole key:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692817044472/8ac6fd43-29d9-49c3-95bd-d73ac8ffeafd.png align="center")

Paste it inside the **Key** section in Jenkins and click on "**Add**":

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692817113967/7a6544fc-b63b-4d6c-97ad-e74fd7e39350.png align="center")

Your credentials to connect to the **agent-1** instance have been added.

`Step 20`: Now in the **Credentials** section select the added credentials:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692817243135/f6fb1920-19eb-4de4-8980-f8d6fd691a83.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692817287949/9332f415-7866-4e7e-a6a0-e9efd5f2f972.png align="center")

`Step 21`: Go to the "**Host Key Verification Strategy**" section and select the "**Non verifying Verification Strategy**" It means if the SSH key pair matches then connect to the agent node without any verification.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692817485388/cfdccb22-0c5a-4c9c-9193-c4f0f02ab3bd.png align="center")

Click on "**Save**"

If you see the following image then your Agent has been launched and connected with Jenkins:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692817729862/3a422dc3-d0d6-40f7-85c7-b75fd681d2e8.png align="center")

You can click on the node and select **Configure** if you want to make some changes.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692817833544/0b2c1608-6509-4672-aee5-17382567bbf1.png align="center")

---

# 📍Running a Pipeline Job for Nodejs App on a Jenkins Agent

In the Jenkins **master** server, we will define a pipeline and create a job and the execution will be on the **agent** instance.

`Step 1`: Go to your Jenkins **Dashboard** and click on "**Create a Job**" or "**New Item**"

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692818084474/584c0082-a592-445b-b4be-96af69ce019b.png align="center")

`Step 2`: Enter the Job name "**node-todo-cicd**" and select **Pipeline**:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692818180619/d9464df4-a5d5-4373-be7f-4589bee5eaed.png align="center")

`Step 3`: Give the **Description** and select "**GitHub Project**":

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692818257002/d424caf5-c31c-4195-b1d6-1408fe9af306.png align="center")

`Step 4`: In the "Project url" section copy the GitHub URL of the project repository and paste it.

**GitHub URL**: [https://github.com/LondheShubham153/node-todo-cicd](https://github.com/LondheShubham153/node-todo-cicd)

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692818417060/db25ce7a-f865-4461-a57d-9d924625120c.png align="center")

In the "**Build Trigger**" section you can select "**GitHub hook trigger for GitSCM polling**" and add a **webhook**. Make sure you fork the repository to your GitHub account and also change the GitHub URL you are providing inside the "**Project URL**" section.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692818591718/3d5b1dd8-ef52-444a-8e5d-563a78a9fcd2.png align="center")

I am not selecting it to keep it simple. You can refer to my previous blog on creating a GitHub webhook by [clicking here](https://varunmargam.hashnode.dev/mastering-jenkins-a-comprehensive-guide-to-continuous-delivery-and-deployment).

`Step 5`: Scroll down to the "**Pipeline**" section copy this pipeline and paste it in the **Pipeline script:**

```java
pipeline{
    agent {label 'agent-1'}
    
    stages{
        stage("Clone"){
            steps{
                git url: 'https://github.com/LondheShubham153/node-todo-cicd.git', branch: 'master'
// if you have added webhook then copy the HTTP URL of the your forked Repo.
            }
        }
        stage("Build & Test"){
            steps{
                echo "Building and testing"
            }
        }
        stage("Deploy"){
            steps{
                echo "Deployed"
            }
        }
    }
}
```

Click "**Save**"

`Step 6`: Your Job has been created:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692818841121/8cc7f8a0-3e9b-47a8-8156-f78c3bb860e4.png align="center")

`Step 7`: Click on "**Build Now**"

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692818884166/73b2ada2-5e4b-4120-bec1-a7226554ae53.png align="center")

`Step 8`: You can see the job has been executed successfully:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692818939279/d2dc7617-150c-442b-aa4e-53f6e135d379.png align="center")

`Step 9`: Click on the **#1** build and see the "**Console Output**"

In this **Console Output**, you can see that this job pipeline has been executed on the **agent-1** instance.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692819012242/b46b8248-093d-4c85-80f5-48ed29637270.png align="center")

You can verify this by going to the **agent-1** instance terminal:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692819149372/0b259a40-595e-47ed-ac3e-f8e06c512770.png align="center")

When I do `ls` inside the home directory a directory named `workspace` has been created. This is because while configuring the node we mentioned the working directory as the home directory i.e. `/home/ubuntu`.

Go inside the workspace directory and you can see that the code has been cloned from the Git repository:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692819339806/43c19eb9-8b6e-478c-a37c-3de1173ccee9.png align="center")

We have successfully executed a job build on Jenkins Agent from the Master server.🥳🎉

---

# 📍Conclusion

We have reached the end of this blog we have explored Master-Slave Architecture, Jenkins Agents, and secure connections via SSH. With this understanding, you're now equipped to streamline your development processes and enhance the efficiency of your projects. By implementing what you've learned – from setting up the architecture to deploying a Node.js application – you can now try to run a pipeline for different applications and also add WebHooks. You can try to run the 2-tier Flask Todo Application that we had set up in my previous blog [Click here](https://varunmargam.hashnode.dev/cicd-pipeline-for-2-tier-flask-todo-web-application). Keep building, innovating, and embracing the power of Jenkins in your quest for excellence. Happy coding! 🚀🛠️

Thank you for reading this blog! 📖 Hope you have gained some value. In the future blog, we will be creating and exploring Jenkins pipelines.

If you enjoyed this blog and found it helpful, please give it a like 👍, share it with your friends, share your thoughts, and give me some valuable feedback.😇 Don't forget to follow me for more such blogs! 🌟

---

# 📍Reference

* [ChatGPT](https://openai.com/chatgpt)
    
* [LinkedIn Article of Step-by-Step Implementation](https://www.linkedin.com/pulse/devops-project-4-step-by-step-implementation-chetan-r%3FtrackingId=pXZshJXCRfy0TAzDsPo0nw%253D%253D/?trackingId=pXZshJXCRfy0TAzDsPo0nw%3D%3D)
    

---