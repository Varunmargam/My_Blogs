---
title: "Jenkins Essentials: A Comprehensive Introduction to Automation"
datePublished: Fri Aug 18 2023 03:10:03 GMT+0000 (Coordinated Universal Time)
cuid: cllg0imu9000b08mn1hdsdms1
slug: jenkins-essentials-a-comprehensive-introduction-to-automation
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1692327706287/f8ff6cdd-64b4-4d01-8bc3-75ea782cc20d.png
tags: automation, jenkins, devops-journey, 90daysofdevops, day22

---

---

# 📍Introduction

Welcome to my Jenkins blog series! Here, we'll dive into a tool that DevOps Engineers love for automating tasks. In this beginner-friendly blog, we'll discover what Jenkins is, learn about CI/CD, set it up, explore the Jenkins Web Interface, and create our very first Jenkins job.

---

## 📍What is CI/CD❓

**CI/CD** stands for **Continous Integration** and **Continous Delivery/Deployment**.

When you look at the DevOps symbol

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692323807701/fd777628-6cbb-4e20-ab08-c0bd7844aee2.png align="center")

You can see there is an Infinite Cycle of the SDLC process from Planning to Deploy, Operate and Monitor. This Cycle that helps us for a faster release of the product should be continuous, automated, and robust. This Cycle is known as Continuous Integration and Deployment.

This is a crucial part of the DevOps practice where the whole process is automated, right when the code was committed to Git till it is deployed.

## ✔Continuous Integration (CI)

Continuous Integration (CI) is a development practice centered around the seamless merging and verification of code changes. When a developer commits or adds new code, CI involves assessing its functionality by confirming that it builds successfully, passes predefined test cases without issues, and operates without errors. If these criteria are met, the code is deemed successfully integrated.

In essence, CI consists of three key steps:

1. **Code Verification:** After a developer contributes new code, CI initiates automated checks to ensure it functions as intended.
    
2. **Merging and Assessment:** The code changes are merged with the existing codebase, creating a unified version. This merged code is then assessed as a whole to confirm it fulfills quality standards.
    
3. **Test and Build:** The integrated code undergoes rigorous testing to ascertain its reliability and compatibility with the larger system. Additionally, the code is built to produce a functional executable.
    

CI serves as an early warning system, detecting potential issues promptly and allowing developers to rectify problems before they escalate. By automating the integration, testing, and assessment of code changes, CI enhances collaboration among developers, minimizes errors, and accelerates the development process.

## **✔Continuous Delivery (CD)**

Continuous Delivery is a software development practice where code changes are automatically prepared, tested, and made ready for deployment to a production environment. In CD, every code change that passes automated tests is potentially deployable to production, but the actual deployment to the production environment is typically triggered manually by a team member or through an approval process. It includes:

1. **Automation and Testing:** Continuous Delivery emphasizes the automation of building, testing, and packaging code changes. This ensures that changes are thoroughly verified before they are considered for deployment.
    
2. **Staging and Pre-Production:** In Continuous Delivery, changes are first deployed to staging or pre-production environments, allowing further testing and validation. If the changes pass these tests, they are ready for deployment to the production environment.
    
3. **Manual Deployment:** While the process leading up to deployment is automated, the decision to deploy to the production environment is made by a human. This human intervention adds an extra layer of control and allows for final checks before releasing changes to end users.
    

## **✔Continuous Deployment**

Continuous Deployment takes the concept of Continuous Delivery a step further by automating the entire process of deploying code changes to production without manual intervention. In this approach, any code change that passes automated tests is automatically deployed to the production environment. It includes:

1. **Automated Deployment:** In Continuous Deployment, the deployment process is fully automated. As soon as code changes pass automated tests, they are immediately deployed to the production environment.
    
2. **Minimal Human Intervention:** Unlike Continuous Delivery, where a human decision is required to trigger deployment, Continuous Deployment eliminates this step. This reduces the time between code changes being ready and them being available to users.
    
3. **Rapid Feedback Loop:** Continuous Deployment allows teams to receive rapid feedback from real-world usage of code changes, enabling faster iteration and response to user needs.
    

---

# 📍Jenkins

Jenkins is a powerful CI/CD tool that automates the software development process. By seamlessly integrating development and operations practices, it accelerates the creation, testing, and deployment of software. With Jenkins, code changes are automatically integrated, tested, and deployed, making the entire development lifecycle faster and more efficient. This automation streamlines tasks, reduces errors, and fosters collaboration between teams.

---

# 📍Installation and Setup

Jenkins is a Java-based application that relies on the Java Virtual Machine (JVM) to execute its code. Therefore, a Java Development Kit (JDK) must be installed on the system before you can run it.

Documentation to install Jenkins: [https://www.jenkins.io/doc/book/installing/](https://www.jenkins.io/doc/book/installing/)

```bash
sudo apt-get update
sudo apt install openjdk-17-jre
java --version # Verify java installation
sudo apt-get install jenkins
```

If the output for the `java --version` command is the following then it means the JDK had been successfully installed:

```bash
openjdk version "17.0.7" 2023-04-18
OpenJDK Runtime Environment (build 17.0.7+7-Debian-1deb11u1)
OpenJDK 64-Bit Server VM (build 17.0.7+7-Debian-1deb11u1, mixed mode, sharing)
```

```bash
# After installation is complete jenkins will be active and running
sudo systemctl status jenkins 
sudo systemctl start jenkins # If inactive
sudo systemctl enable jenkins
```

Since Jenkins is a service a user named "jenkins" is created in the system.

## ✔Jenkins Web Interface Setup:

The default port for the Jenkins web interface is **8080**. This means that when you access Jenkins through a web browser, you would typically use a URL like:

http://localhost:8080

http://aws\_ec2\_ip\_address:8080 ( If you are using an EC2 instance like I am)

Type this URL in your browser you will get this:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692293055594/5a25cfe3-076b-4e84-a259-930329b292a6.png align="center")

Admin initial password is stored in a temporary file inside the `/var/lib/jenkins/secrets/initialAdminPassword` directory path:

Use this command for Linux:

```bash
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```

`Step 1`: Copy the password, paste it, and then press Continue.

`Step 2`: Click on Install suggested plugins.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692293417464/a98bfc17-a7da-470b-9d72-55d29d699a14.png align="center")

Jenkins will automatically install all the necessary plugins usually useful for performing DevOps tasks

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692293638046/2ea5054c-a26e-425b-b0ce-9f04cb5d64cb.png align="center")

`Step 3`: Enter your details to create the first admin user and press Save and Continue.

This **First Admin User** has access to the Jenkins **global configuration**

* The admin user can create, modify, delete user accounts, and assign permissions and roles to other users within Jenkins.
    
* Admins can create, configure, and delete Jenkins jobs (build, test, deployment tasks) for different projects.
    
* And many more privileges like **View Management, Plugin Management, etc.**
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692294074835/3320859b-d445-42b6-b2b6-9b3917c69c75.png align="center")

Then you will get a Jenkins URL to access Jenkins, you can change this URL name as you like.

Your Set-Up is now finished and you will get the **Jenkins Interface** home page:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692294362862/409f83a1-3fb3-47b5-8632-4df55e0345f9.png align="center")

---

# 📍Getting Familiar with Jenkins Interface

There must be many things you are seeing on your Jenkins home page. Let's look at each one of them:

* **Dashboard Overview:** The Jenkins dashboard serves as the main landing page upon logging in. It provides an at-a-glance overview of the status and activity within your Jenkins environment. The components you might find here include:
    
    * **Build History:** A list of recently completed builds and their statuses.
        
    * **Job Status:** The current status of your jobs, indicating whether they are building, stable, or failed.
        
    * **Views:** Links to different views that organize your jobs based on criteria like projects, teams, or functionalities.
        
    
    **Navigation:** Jenkins provides a set of navigation links and menus that help you move around the interface:
    
    * **New Item:** Allows you to create new Jenkins jobs, including freestyle and pipeline jobs.
        
    * **Build Executor Status:** This shows the current usage of build executors (agents/nodes).
        
    * **Manage Jenkins:** Access to the global configuration settings, plugin management, system information, and more.
        
    * **User Menu:** You can see at the left represented as **People**. Contains options for managing your user account, credentials, and log-out.
        
    
    **Build History:** Jenkins keeps a record of job builds, which includes information like:
    
    * **Build Number:** A unique identifier for each build.
        
    * **Status:** Indicates whether the build succeeded, failed, or is unstable.
        
    * **Timestamp:** When the build was executed.
        
    * **Duration:** How long the build took to complete?
        
    
    **Console Output:** We will see this when we create a Jenkins Job. The console output provides a detailed log of the build process. It's a valuable resource for diagnosing issues and understanding the flow of the build. You can access it by clicking on the build number or the build status icon.
    
    **Job Configuration:** When creating or editing a job, you configure various settings:
    
    * **General Configuration:** Naming the job, defining a description, and specifying parameters.
        
    * **Source Code Management:** Configuring the version control system (e.g., Git) and repository URL.
        
    * **Build Triggers:** Specifying conditions that trigger the job (e.g., code changes, scheduled times).
        
    * **Build Steps:** Defining the tasks to be performed during the build process.
        
    * **Post-Build Actions:** Actions to be taken after a build completes, such as notifications or archiving artifacts.
        
    
    **Views:** Views allow you to organize jobs for easier management and navigation:
    
    * **List View:** Displays jobs in a list format. You can create multiple list views based on categories.
        
    * **Dashboard View:** Provides a graphical dashboard with widgets displaying job status, statistics, and trends.
        
    * **My Views:** Custom views that you can create and configure based on your needs.
        

---

# 📍**Jenkins Plugins**

## **✔What Are Plugins❓**

Plugins in Jenkins are modular extensions that enhance and expand its capabilities. They can add functionalities such as integrating with version control systems, automating builds, sending notifications, and more. Plugins are crucial for adapting Jenkins to your specific requirements without modifying its core code.

**Installing Plugins:** Jenkins provides a Plugin Manager that simplifies the process of finding, installing, and managing plugins:

* **Plugin Search:** You can search for plugins by name or functionality using the Plugin Manager's search bar. You see this search bar by clicking on "**Manage Jenkins**" at the left.
    
    From the dropdown menu that appears when you click "**Manage Jenkins**", select "**Manage Plugins**."
    
* **Installation:** When you find a plugin you need, you can install it with a single click. Jenkins will download and install the plugin for you.
    
* **Updating Plugins:** The Plugin Manager also helps you keep your plugins up to date by notifying you when updates are available.
    

**Commonly Used Plugins:** Highlighting a few essential plugins can help readers grasp the breadth of functionality plugins provide:

* **Git Plugin:** Integrates Jenkins with Git repositories, enabling automatic builds triggered by code changes.
    
* **Docker Plugin:** Facilitates Docker integration, allowing Jenkins to build, test, and deploy Docker containers.
    
* **Pipeline Plugin:** Introduces Jenkins Pipeline, enabling you to define complex build and deployment workflows as code.
    

**Plugin Configuration:** After installing a plugin, you often need to configure it to suit your needs:

* **Global Settings:** Some plugins have global settings that affect the entire Jenkins instance.
    
* **Job-specific Configuration:** Plugins might introduce new configuration sections within job settings, allowing you to tailor their behavior per job.
    

**Customization:** Plugins empower you to customize Jenkins to align with your specific use cases:

* **Tailored Workflows:** You can combine various plugins to create workflows that meet your automation and deployment needs.
    
* **Visualizations and Reporting:** Plugins can introduce graphs, charts, and reports that help you analyze build trends and project health.
    

**Plugin Compatibility:** It's important to keep plugins up to date for several reasons:

* **Bug Fixes and Enhancements:** New versions might include bug fixes, performance improvements, and new features.
    
* **Security Updates:** Plugin updates might address security vulnerabilities, helping keep your Jenkins instance secure.
    

**Removing Plugins:** Removing unnecessary plugins can help maintain a clean Jenkins environment:

* **Backup:** Always make backups before removing plugins to ensure you can revert changes if needed.
    
* **Disruption Prevention:** Remove plugins carefully, as some jobs might rely on their functionality. Analyze potential impacts before deletion.
    

**Managing Dependencies:** Some plugins depend on others to function properly:

* **Plugin Interactions:** Some plugins might require specific core or other plugins to work correctly.
    
* **Dependency Handling:** Jenkins' Plugin Manager often handles plugin dependencies automatically, installing required plugins when you install one that depends on them.
    

---

# 📍Jenkins Job

A Jenkins job is a sequence of steps, commands, or actions that need to be executed as part of an automation workflow. Jenkins jobs automate repetitive tasks such as compiling code, running tests, packaging applications, and deploying software.

A Jenkins job is a way to automate a specific task or process in a software development workflow. Jobs encompass everything from source code management to build processes, testing, and deployment. The ability to define, configure, and automate jobs is a central feature of Jenkins, enabling teams to streamline their development and deployment processes.

**There are 3 types of Jobs:**

1. **Freestyle Jobs:** Traditional build jobs where you define a series of build steps, triggers, and actions.
    
2. **Pipeline Jobs:** Introduced by the Jenkins Pipeline plugin, they enable defining entire build and deployment workflows as code in a Jenkinsfile.
    
3. **Matrix Jobs:** Used for testing a combination of different parameters, such as various OS versions or browsers.
    

---

# 📍**Creating Your First Jenkins Job**

`Step 1`: Click on "**Create a Job**" at the center or "**New Item**" at the left.

`Step 2`: Give a name to the Jenkins Job and select "**Freestyle project**" and Press "**OK**".

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692296123359/f13fa832-7d5c-44df-9710-3958388687bf.png align="center")

`Step 3`: Add some description of what this job is doing.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692296461489/2a1d47da-4785-414c-a17d-cf7f07aaccfb.png align="center")

`Step 4`: Scroll down and in the Source Code Management Section select None.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692296226539/d8e96bd3-7780-4a6a-8877-5dd5cee1ac17.png align="center")

`Step 5`: Scroll down a little and go to the Build Steps section. It is a dropdown menu to select a shell where you can execute your build and deploy commands or any other command you want to execute during the build process.

Select the "**Execute** **Shell**" option:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692296698956/b4ff3f37-64b3-460c-9686-db382d753142.png align="center")

After selecting you will get a shell where you can write the commands.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692296778677/948c8db7-8937-4d64-971b-64aa9474439a.png align="center")

`Step 6`: Click "**Save**" and your Job has been created.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692296933561/69919f7b-da4c-4e45-b398-e2246fad9a9b.png align="center")

`Step 7`: Click on "**Build Now**" at the left to start the build of the Job.

You can see that your build has been executed successfully since we can see a green tick mark.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692297557553/2b27bb17-2469-4bec-bb39-961342868ef4.png align="center")

`Step 8`: Click on that build "**#1**" You will see this:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692297683872/2f6317b3-1442-4234-b273-de83c9a7d6fa.png align="center")

`Step 9`: Click on "**Console Output**" To see all the steps it performed in the build process:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692297790182/f19e0a9b-269f-4dec-8508-9fe6b198ed02.png align="center")

If the build fails, you can review the console output to pinpoint the exact point, step, or code where the failure occurred.

📝**Note**: All these Jenkins tasks are performed by the "jenkins" user in the system.

---

# 📍Conclusion

In this Introductory blog on Jenkins, we have seen Jenkins stands as the bridge that connects development and operations, facilitating seamless integration, testing, and deployment of code. Jenkins fuels DevOps by automating the SDLC with Continuous Integration and Deployment (CI/CD). We are now familiar with the Jenkins web Interface and used some of its basic features.

We will learn more about its features as we move along in this journey of exploring Jenkins.

Thank you for reading this blog! 📖 Hope you have gained some value.

If you enjoyed this blog and found it helpful, please give it a like 👍, share it with your friends, share your thoughts, and give me some valuable feedback.😇 Don't forget to follow me for more such blogs! 🌟

---

# 📍Reference

* [ChatGPT](https://openai.com/chatgpt)
    
* [Google](http://google.com)
    

---