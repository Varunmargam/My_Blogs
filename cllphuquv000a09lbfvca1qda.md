---
title: "Jenkins Important interview Questions"
datePublished: Wed Aug 23 2023 18:30:00 GMT+0000 (Coordinated Universal Time)
cuid: cllphuquv000a09lbfvca1qda
slug: jenkins-important-interview-questions
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1692901466226/0a2c3778-2b4d-4298-a055-445636b83292.png
tags: jenkins, devops-journey, 90daysofdevops, day29, jenkisninterviewquestions

---

---

1. **What’s the difference between continuous integration, continuous delivery, and continuous deployment?**
    
    **Ans**:
    
    **Continuous Integration:** It includes stages like Cloning the updated code, Building, and Testing. Its main goal is to continuously integrate the changes made to the main code and identify issues in the early development process.
    
    **Continuous Delivery:** It extends CI by making the Integrated code production ready i.e. ready to be deployed. It automates the deployment process to the staging or preproduction server. Continuous Delivery requires a manual trigger or approval from the manager, team lead, or a senior responsible for the project in an organization.
    
    **Continuous Deployment:** Similar to Continuous Delivery automates the Deployment process. The only difference is that the deployment occurs automatically without any manual intervention. This approach requires a high degree of confidence in the automated testing and deployment processes, as any code passing the automated tests is immediately deployed.
    
2. **Benefits of CI/CD**
    
    Ans:
    
    * Reduces the time taken in the process from Code to Deploy
        
    * Reduces Manual errors
        
    * Automates repetitive tasks
        
    * Ensures Faster deployment with quality assurance of the code
        
    * Bridges the gap between the Development and Operations team
        
    * Makes the software development process smoother.
        
    * Facilitates Rollbacks
        
    * Rapid Feedback
        
    * Supports Agile and DevOps Practices (Last 3 points added from ChatGPT)
        
3. **What is meant by CI-CD**?
    
    Ans:
    
    CI-CD stands for Continuous Integration and Continuous Deployment or Delivery. In an organization, multiple people are working on a particular software simultaneously and many code changes are committed and managed via Git a Source Code Management Tool. Now, to integrate these changes with the actual software running in the production environment, we need to go through the process of SDLC. This has to be done for every code change that occurs because if there is an issue in the testing phase it is easier to troubleshoot the problem. However in an organization, a large number of code changes occur daily, so it becomes very difficult to go through the whole process of Integrating the code changes to Deploying manually. Therefore, using Jenkins, we automate this whole process using Jenkins Pipeline, which is written in Groovy syntax. This automation is called CI-CD i.e. Continuous Integration and Continuous Delivery or Deployment.
    
4. **What is Jenkins Pipeline**?
    
    Ans:
    
    Jenkins Pipeline is one of the features of Jenkins Job that automates the process of Integrating the changes in the code to Deploy it on a production server i.e. it facilitates CI/CD. It is written in Groovy syntax.
    
    A pipeline is defined in various stages that perform the tasks of the entire software development process. This also helps in troubleshooting if any issue occurs or the build fails since the pipeline fails if an issue occurs in any of the stages. The pipeline structure is defined using keywords which are:
    
    1. `pipeline`: Indicating this is a pipeline script and defines the start and the end of the pipeline
        
    2. `stages`: Used to define and include the stages.
        
    3. `stage()`: Stage is defined and named in the `()` parentheses and includes the steps/tasks to perform inside this stage.
        
    4. `steps`: This is where we write the Groovy code to define the tasks we want to perform in this stage.
        
    
    Most of the time CI/CD Pipelines are used as Jenkins Job for automation since they can be visualized and managed better.
    
    There are two types of Jenkins Pipeline:
    
    * **Scripted Pipeline**: This is more flexible and provides more control by allowing us to script logic, conditional statements, etc. This is a traditional way of defining a pipeline and requires advanced knowledge. But also provides advanced scripting capabilities that can be useful for complex scenarios. It can be difficult to maintain as the complexity grows.
        
    * **Declarative pipeline**: This is simpler than scripted as it abstracts the complexity of defining a pipeline by giving a structure and using keywords. It is easy to write as it provides a predefined structure for a pipeline. Easy to maintain and visualize the pipeline. Ideal for scenarios where readability is important.
        
5. **How do you configure the job in Jenkins?**
    
    Ans:
    
    Click on "Create a Job" or "New Item" to create and configure the Job. If you want to configure an already defined Job then select the job, and click on "Configure" on the left-hand side of the Jenkins Web Interface. Configuration includes options like Build Triggers, Source Code Management, Build Environment, Build Steps, Post-Build Actions, and Save Configuration.
    
6. **Where do you find errors in Jenkins?**
    
    Ans:
    
    The error can be found at "**Console Outputs**" which can be seen by clicking on the build at the bottom left corner and then selecting "Console Output". It provides a detailed log of all the steps it performs during the build process.
    
    **Pipeline Stage Logs**: If it is a pipeline you can also see the logs of a particular stage by clicking on that particular stage of the visually represented pipeline.
    
7. **In Jenkins how can you find log files?**
    
    Ans:
    
    In Jenkins log can be found in "Console Output".
    
    (Things I learned now after searching for this answer):
    
    (Added form ChatGPT)
    
    1. **Log Files Directory (File System):**
        
        * Jenkins also stores log files on the file system of the server where Jenkins is installed.
            
        * The location of these log files can vary depending on the installation and configuration of Jenkins.
            
        * The most common location for log files is within the Jenkins home directory under a subdirectory named "logs."
            
    2. **Job Workspace (For Pipelines):**
        
        * For pipeline jobs, logs related to individual stages and steps can be found in the workspace directory of the job.
            
        * During the pipeline execution, each stage may generate its log files that can be located in the respective workspace directories.
            
8. **Jenkins workflow and write a script for this workflow?**
    
    Ans:
    
    A simple Jenkins workflow that includes basic stages of cloning, building, testing, and deploying an application
    
    ```java
    pipeline {
        agent any
        
        stages {
            stage('Clone') {
                steps {
                    // Cloning the source code from version control
                    // For example, using Git
                    git url: 'GitHub_Repo_URL', branch: 'main'
                }
            }
            
            stage('Build') {
                steps {
                    // Compile and build the application
                    sh 'npm install' // Assuming a Node.js application
                    // using docker
                    sh 'docker buid . -t app:latest'
                }
            }
            
            stage('Test') {
                steps {
                    // Run tests
                    sh 'npm test'
                }
            }
            stage('Deploy') {
                steps {
                    // Manual approval or trigger
                    input message: 'Deploy to production?', ok: 'Deploy'
                    
                    // Deploy to production environment
                    sh 'npm run deploy:production'
                    // using docker
                    sh 'docker run app:latest'
                }
            }
        }
        // It includes Archives artifacts, sends notifications, and performs cleanup
        post {
            always {
                // Archive build artifacts, clean up, etc.
            }
            success {
                // Send notifications or perform actions on success
            }
            failure {
                // Send notifications or perform actions on failure
            }
        }
    }
    ```
    
    Note that this is a simple pipeline and the real-world scenarios may involve complex scenarios.
    
9. **How to create a continuous deployment in Jenkins?**
    
    Ans:
    
    **Configuring Job**: Select the Project as a GitHub Project, In the SCM (Source Code Management) select GitHub Github webhooks by GitScm in the Build triggers section and you have to give the project URL i.e. the HTTP URL used for cloning the repository, and the branch name you want to clone in a freestyle project.
    
    **GitHub WebHook**: In the GitHub repository, you must also generate a WebHook and make sure that it is active. Since Continuous deployment means the build process starts automatically when any code commit occurs we are achieving it via webhooks that trigger the build process for any event that occurs in the GitHub repo. You can select on which event the build process should be triggered by configuring the webhook.
    
    **Test and Verify**: You can make some changes to the code, commit those changes, and you can see whether the build process is being triggered or not.
    
10. **How to build a job in Jenkins?**
    
    Ans:
    
    In the Jenkins Web Interface Dashboard, click on "**New Item**" or "**Create a Job**". Give the Job a name and select the type of Job Freestyle, Pipeline, etc. Give the Job a Description, select the type of project like Git project, etc., and provide the necessary URL of the project. You can select any Build Triggers. You can also select when to run the job in the Build Triggers section. It can be a cron job for periodic intervals, GitHub webhooks, etc. If a freestyle project you can define the job by selecting the shell and providing shell commands, if it is a pipeline you would have to define a Pipeline script that is groovy syntax. Click on Save. Your Jenkins job is created.
    
    ( A more structured and detailed answer from ChatGPT ):
    
    1. **Access Jenkins Dashboard:**
        
        * Open a web browser and navigate to the Jenkins server's URL to access the Jenkins dashboard.
            
    2. **Create a New Job:**
        
        * Click on the "New Item" or "Create a Job" option on the Jenkins dashboard. The wording might vary based on your Jenkins version.
            
    3. **Job Configuration:**
        
        * Give the job a meaningful name that reflects its purpose.
            
        * Choose the appropriate job type based on your project's requirements. Options include Freestyle project, Pipeline, Multibranch Pipeline, etc.
            
    4. **Job Description:**
        
        * Provide a brief description of the job to convey its purpose and functionality.
            
    5. **Source Code Management (If Applicable):**
        
        * If your job involves source code, select the type of project (e.g., Git, Subversion).
            
        * Provide the URL of the project's repository where Jenkins will fetch the code.
            
    6. **Build Triggers:**
        
        * Specify when the job should be triggered. Options include:
            
            * Manual build: Triggered by users manually.
                
            * Build periodically: Using cron syntax for scheduled builds.
                
            * GitHub webhook: Triggered by code commits or other events in a GitHub repository.
                
            * Trigger builds remotely: Allows triggering via an HTTP request.
                
    7. **Build Steps:**
        
        * Configure the build steps according to your job's requirements:
            
            * For a Freestyle project, you can add build steps like executing shell commands, running Windows batch commands, invoking scripts, etc.
                
            * For a Pipeline project, define stages and steps using Groovy syntax in the pipeline script.
                
    8. **Post-Build Actions (Optional):**
        
        * Configure actions to be taken after the build completes:
            
            * Archive artifacts: Store build artifacts for future reference.
                
            * Send notifications: Notify team members about the build status.
                
            * Publish reports: Publish test results, coverage reports, etc.
                
    9. **Save and Run:**
        
        * Click on the "Save" or "Apply" button to save the job configuration.
            
        * If you want to immediately build the job, click on the "Build Now" button.
            
    10. **Monitor Build Progress:**
        
        * On the Jenkins dashboard, you can monitor the build progress in real time.
            
        * Click on the specific build to access detailed build logs, console output, and other information.
            
    
    **Best Practices:**
    
    * Keep your job configurations concise and well-organized.
        
    * Utilize parameters and environment variables to make your jobs more flexible.
        
    * Regularly review and update your job configurations as project requirements evolve.
        
11. **Why do we use a pipeline in Jenkins?**
    
    Ans:
    
    Since pipelines in Jenkins are defined in stages, it is easy to troubleshoot if the build fails as we can see in the logs of only the stage that has failed. You can use a scripted or declarative pipeline suitable to your needs. Pipelines are a lot more organized and easy to manage.
    
    Some key points for a more organized answer:
    
    * **Structured Workflow**
        
    * **Improved Visibility**
        
    * **Granular Troubleshooting**
        
    * **Parallel Execution:** Pipelines offer the ability to run multiple stages concurrently, leading to faster build times. This is especially advantageous in complex projects with multiple stages that can be executed independently.
        
    * **Reproducibility:** Pipeline configurations are stored as code (either scripted or declarative), making them versionable and repeatable. You can track changes, roll back, and precisely recreate previous builds.
        
    * **Flexibility**
        
    * **Automation and Consistency**
        
    * **Standardization**
        
    * **Integration with DevOps Practices**
        
    * **Declarative Syntax**
        
    * **Code Review and Collaboration**
        
    * **Visualization and Reporting**
        
12. **Is Only Jenkins enough for automation?**
    
    Ans:
    
    No, Jenkins does automate the software development process, but we still have to set up the system in which Jenkins is running for the application to run. We have to install all the dependencies and the libraries manually in the system. This can also be automated by using Docker. So Jenkins when Integrated with Docker takes care of all the dependencies and the libraries required for the application to run and truly automates the process.  
    Although my answer is correct I suggest you look for a more comprehensive answer
    
    <details data-node-type="hn-details-summary"><summary>ChatGPT Answer</summary><div data-type="detailsContent"><strong>Jenkins and Automation:</strong> Jenkins is a powerful automation server that plays a central role in automating various aspects of the software development and deployment process. It allows you to automate tasks such as code integration, building, testing, and deployment, enabling continuous integration and continuous delivery (CI/CD) practices. <strong>However, Jenkins Alone Is Not Always Enough:</strong> While Jenkins is a critical component in the automation process, it's important to recognize that it's not the only consideration when it comes to achieving comprehensive automation. A few points to consider: <strong>Infrastructure and Environment Setup:</strong> Jenkins itself needs to be set up and configured on a server or virtual machine. Beyond that, if your application relies on specific environments, databases, configurations, and dependencies, you need to ensure that these are correctly set up as well. This is where tools like Docker can be valuable. <strong>Dependency Management:</strong> Jenkins can automate the execution of various tasks, but managing dependencies and libraries required by your application is often not its primary focus. Tools like package managers or dependency management systems (e.g., npm, pip, Maven) are commonly used to handle this aspect. <strong>Testing and Quality Assurance:</strong> While Jenkins can run tests, you might need additional tools for more advanced testing, such as load testing, security testing, and automated UI testing. <strong>Deployment and Orchestration:</strong> Jenkins can handle the deployment of your application, but for more complex deployment scenarios involving microservices, scaling, and orchestration, you might need tools like Kubernetes or Docker Swarm. <strong>Docker and Jenkins Integration:</strong> Docker is indeed a powerful tool to enhance automation by providing containerization. Containers encapsulate applications and their dependencies, ensuring consistency across different environments. Jenkins can integrate with Docker, allowing you to automate the creation of containers, manage dependencies, and ensure consistent environments for development, testing, and deployment. <strong>In Conclusion:</strong> While Jenkins is a cornerstone of automation in the software development lifecycle, it's often used in conjunction with other tools and practices to create a comprehensive automation strategy. This strategy encompasses environment setup, dependency management, testing, deployment, and more. The integration of Jenkins with tools like Docker can provide a more complete and efficient automation solution.</div></details>
13. **How will you handle secrets?**
    
    Ans:
    
    Assuming by secrets you mean the Credentials that may be needed for certain steps, we can manage it by adding the credentials to Jenkins, Going to Dashboard, clicking on manage Jenkins, Go to the Security section, and clicking on Credentials, Click on global and then on Add credentials, You can add the whatever credentials you require for running the job. The credentials are identified by Credentials\_ID. In a Pipeline script, you can use the withCredentials() function to inject the credential in the code.
    
    Example:
    
    ```java
    pipeline {
        agent any
        environment {
            MY_CREDENTIAL = credentials('my-credential-id')
        }
        stages {
            stage('Example') {
                steps {
                    withCredentials([usernamePassword(credentialsId: 'my-credential-id', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                        sh 'echo $USERNAME'
                        sh 'echo $PASSWORD'
                    }
                }
            }
        }
    }
    ```
    
14. **Explain different stages in CI-CD setup.**
    
    Ans:
    
    Generally, the basic structure for the CI-CD setup includes the following stages:
    
    * Clone: Cloning the code from the Git repository
        
    * Build: Building the Code using Docker, or a Build tool like Maven, Graddle, etc.
        
    * Test: Running some test cases, checking bugs or issues, can use SonarQube for Quality assurance.
        
    * Deploy: Deploying the built and tested application on the server can be a Cloud service.
        
    
    My explanation provides a basic overview of the typical stages in a CI/CD setup. You can expand each point or add some extra points like **Quality Assurance, Automated Testing, Release, and Monitoring,** and **Rollback and Recovery (Contingency)**
    
15. **Name some of the plugins in Jenkin.**
    
    Ans - Sonaqube scanner, Ocean Blue
    
    I only knew these two plugins😅
    
    Here's what I got from ChatGPT:
    
    * **SonarQube Scanner:** Integrates Jenkins with SonarQube, a platform for continuous code quality and security analysis. It helps identify code smells, bugs, vulnerabilities, and ensures high-quality code.
        
    * **Blue Ocean:** A modern, user-friendly user interface for Jenkins pipelines. It provides a visual representation of pipeline stages, logs, and a better overall pipeline visualization.
        
    * **GitHub Integration:** Plugins like GitHub Integration or GitHub Pull Request Builder enable Jenkins to automatically trigger builds based on code commits, pull requests, and status changes on GitHub.
        
    * **Docker:** Plugins like Docker Pipeline or Docker Build and Publish integrate Jenkins with Docker, allowing you to build, package, and deploy Docker containers seamlessly.
        
    * **JUnit:** The JUnit plugin helps analyze and display test results in Jenkins, making it easier to track test outcomes and identify failures.
        
    * **Deploy to Container Platforms:** Plugins like Kubernetes Continuous Deploy and Docker Swarm Plugin assist in deploying applications to container orchestration platforms like Kubernetes and Docker Swarm.
        
    * **Slack Notification:** Plugins like Slack Notification allow Jenkins to send notifications to Slack channels, informing teams about build and deployment status.
        
    * **Email Extension:** This plugin enables Jenkins to send customizable email notifications for build and test results.
        
    * **Artifactory Integration:** Plugins like JFrog Artifactory provide integration with artifact repositories, allowing you to store and manage build artifacts efficiently.
        
    * **Pipeline Utility Steps:** Provides additional functionality in Pipeline scripts, allowing you to interact with the build environment, manage credentials, and manipulate data.
        
    * **Pipeline AWS:** Integrates Jenkins pipelines with Amazon Web Services (AWS), enabling you to provision resources, deploy applications, and manage AWS services from within Jenkins pipelines.
        
    * **Git Plugin:** The Git plugin enables Jenkins to interact with Git repositories, fetching code, and managing branches and commits.
        
    * **Credentials Binding:** This helps secure credentials by allowing you to inject them directly into your pipelines without exposing sensitive information in logs.
        
    * **SSH Agent:** Allows you to use SSH keys for authentication within your pipelines, simplifying secure access to remote systems.
        
    * **Nexus Integration:** Plugins like Nexus Platform Integration help integrate Jenkins with the Nexus repository manager for artifact management and distribution.
        

---

# 📍Conclusion

Thank you for reading this blog! 📖 Hope you have gained some value. In the future blog, we will be creating and exploring Jenkins pipelines.

If you enjoyed this blog and found it helpful, please give it a like 👍, share it with your friends, share your thoughts, and give me some valuable feedback.😇 Don't forget to follow me for more such blogs! 🌟

---

# 📍Reference

* [ChatGPT](https://openai.com/chatgpt)
    

---