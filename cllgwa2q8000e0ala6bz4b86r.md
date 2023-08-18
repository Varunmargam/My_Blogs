---
title: "Mastering Jenkins: A Comprehensive Guide to Continuous Delivery and Deployment"
datePublished: Fri Aug 18 2023 17:59:11 GMT+0000 (Coordinated Universal Time)
cuid: cllgwa2q8000e0ala6bz4b86r
slug: mastering-jenkins-a-comprehensive-guide-to-continuous-delivery-and-deployment
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1692381423778/dbc4d964-8925-466d-a5a0-6bbfdc8fc733.png
tags: jenkins, devops-journey, 90daysofdevops, day23, freestyle-jenkins-project

---

---

# 📍Introduction

Welcome to my Jenkins blog series! In this guide, we'll explore the world of Continuous Delivery and Deployment using Jenkins. From implementing Continuous Delivery for a Django todo app to achieving Continuous Deployment for a Node.js application, you'll gain practical insights into setting up Jenkins jobs, configuring webhooks, and orchestrating deployments. Whether you're a seasoned developer or a newcomer, join me on this journey to streamline your development workflow and master the art of automated application delivery with Jenkins. Let's dive in!

---

# 📍Implementing CI/CD (Delivery) with Jenkins: Django Todo App Freestyle Project

We're setting up a Jenkins Job for deploying the Django todo app with Continuous Delivery. i.e. for every change committed to the code, we would manually have to run this Jenkins job to start the process of cloning, building, and deploying.

`Step 1`: Click on "**New Item**"

Change the Photo

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692352220198/cab91ec8-d48b-40e5-9c19-07870f88bc24.png align="center")

`Step 2`: Name the job "**django-todo-app-delivery**", select "**Freestyle project**", and click "**OK**".

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692352446702/e9526cde-c64d-44ec-b15a-9f4cc3ef1a87.png align="center")

`Step 3`: Add this Description:

```plaintext
This project/job is the delivery of my Django-todo-app. I am using Jenkins to automate the task of getting the code from GitHub, building, and deploying it.
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692352553552/66b1d4fa-60fe-4115-a4c4-07d87f23c861.png align="center")

`Step 4`: Since this is a GitHub project click on the "**GitHub project**" and add this URL([https://github.com/LondheShubham153/django-todo-cicd](https://github.com/LondheShubham153/django-todo-cicd)) in the "**Project url**" section.

This is the repository:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692353776115/18f002c3-e91b-4e80-a0fc-281480d3e6f4.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692380270892/2ec6219b-6722-40cb-b696-da3a5622e3ff.png align="center")

You can see what the other project options mean by clicking on them.

`Step 5`: Come to the "Source Code Management" section and select "Git".

It will ask you for the repository URL i.e. the **HTTPS URL** that is used to **clone** the repository.

HTTPS URL: [https://github.com/LondheShubham153/django-todo-cicd.git](https://github.com/LondheShubham153/django-todo-cicd.git)

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692355549984/405aa20b-3c2b-4625-939d-84505e1f1ed6.png align="center")

In the "**Credentials section,**" you need to give the credentials like "**PAT (Personal access token)**" or "**ssh-key**" for private repositories. Since GitHub has now removed accessing the repository through username and password for other users.

We don't need to provide any Credentials since this is a Public Repository.

`Step 6`: In the "**Branches to build**" section we have to specify the branch we want to build.

Since the code resides in the "**develop**" branch:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692353675266/c7530620-9ad1-41a0-b6bd-232c4257eba1.png align="center")

In this Section at the bottom, you will see the "**Additional Behaviours**" with the "Add" dropdown, here you can select any option and do things like To copy, run a particular file of another branch or particular commit, etc. can be done.

`Step 7`: Go to the "**Build Steps**" section where you can specify the actions or commands to execute the code which you have cloned.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692355207471/669e5439-ffe5-4adf-874f-fba7a638fb56.png align="center")

`Step 8`: Click on the "**Add build step**" and select "**Execute shell**" and add these commands:

```bash
echo "This job worked and successfully cloned the code."
whoami
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692355719104/409911c3-1a00-40ec-83c7-c3470b9aaebe.png align="center")

`Step 9`: And Click "`Save`".

Your job has now been created:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692355899931/801264ca-34f4-487b-a07e-ab46c033178e.png align="center")

At the extreme right of where your job is displayed, you can see a green triangle. That sign represents starting the "**Build**" process.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692356047608/32244747-ec52-4db5-b7fe-64cd32d59ca2.png align="center")

`Step 10`: Click on that icon and your build process will start. You can see the build process on the bottom left side of the screen in the "**Build History**" section.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692356312280/5d25aafc-5b31-40ac-9c3e-2738f0ab372f.png align="center")

You can see our build has been successful, now click on the **#1 tick icon** in the "**Build History**" section to see the "**Console Output**":

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692356773201/b4206ea8-58d3-4964-b279-ef9306cb8d3d.png align="center")

You can see all the steps it executed during the build process:

1. Cloning the code from the git repository.
    
2. Executing the command we had written in the build steps.
    
3. The output for the command `whoami` is jenkins.
    

Therefore, this tells that all Jenkins's actions during the build process are done by the "**jenkins**" user.

You can also see the cloned repository in your terminal. As in the "Console output it specifies Building in workspace `/var/lib/jenkins/workspace/django-todo-app-delivery`.

To see the use the command:

```bash
ls /var/lib/jenkins/workspace/django-todo-app-delivery
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692357238702/0097c165-4332-4ecc-98b7-348502438add.png align="center")

You can see it has automatically cloned this repository as we have mentioned the URL while configuring this job.

Let's build and deploy this Django-todo-app using Jenkins. For that:

`Step 1`: Go to your Job "**django-todo-app-delivery**" and Click on "**Configure**".

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692357465501/f46de502-997b-4822-aec1-d903bf4d5053.png align="center")

You will see the same screen as we saw while Configuring/Defining the New Job after clicking on Configure. Go to the "Build Steps" section and type these commands and Save it:

```bash
docker build . -t django-app
docker run -d -p 8000:8000 django-app:latest
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692357644641/038741c3-92c6-4975-adce-c0861ec2a93e.png align="center")

But before running the build process we know that all these processes and commands are executed by the "**jenkins**" user. Therefore, we have to make sure that the "**jenkins"** user has permission to execute these docker commands.

Therefore:

`Step 2`: Go to your terminal and add the "**jenkins**" user to the docker group.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692357898420/910eb153-26a1-421b-b1b8-baddf147b28e.png align="center")

`Step 3`: Since we have rebooted the system, refresh the Jenkins Web Interface Page and log in to Jenkins

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692358052529/6ca11ca3-f44e-4d9d-a1f4-bf85c5ffd44b.png align="center")

`Step 4`: Now Click on the "**Build Now**" button above "**Configure**".

You can see the Build has been successful and it is shown as **#2** since this is the 2nd build of the job.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692358277213/19e42b6d-52a0-4f03-8080-d67f1d3710fa.png align="center")

You can see on the same port where your Jenkins Web Interface is running at **port 8000** Django-todo-app has been deployed and running:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692358456327/e0ae08fc-b47c-45ab-a9e2-5f3e73c1cf41.png align="center")

📝Note: Make sure you have updated the Inbound rules of your AWS EC2 Instance's Security Group allowing access to port 8000.

You can see the Console Output and see all the steps executed.

Now, If I built this Job again there would be a "**port conflict error**" because there is still a container running on port 8000 and now you are trying to run a new container on the same port.

For the new container to run you would have to stop and remove the previous container and only then you can create and run a new container.

To achieve this we can use **Docker-compose** since `docker-compose` has a command called `docker-compose down` that stops and removes the existing containers created by the **docker-compose.yml** file.

`Step 1`: Go to "Configure" of your "**django-todo-app-delivery**" job and scroll down to the "Build Steps" section and replace the docker commands with these docker-compose commands and click "**Save**":

```bash
docker-compose down
docker-compose up --no-deps --build web
# web is the name of the service you can check the docker-compose.yml file.
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692367071309/aa5a6306-894c-4992-a450-33d47a7845cd.png align="center")

Here, is why I did not simply write `docker-compose up` command:

`docker-compose up --no-deps --build web`

The command `docker-compose up --no-deps --build web` is used to start the `web` service defined in the Docker Compose configuration. The `--no-deps` flag ensures that dependent services are not started automatically. The `--build` flag indicates that the specified service (`web` in this case) should be rebuilt before starting.

The reason for specifying `--build` is that, during repeated builds, Docker tries to leverage cached layers from previous builds to improve build speed. However, in some cases, especially when there are changes in the project's source code or build context, the cached layers might not reflect the latest changes accurately. By using `--build`, you ensure that the `web` service is built from scratch, disregarding the cache and incorporating any recent changes. This guarantees that the resulting image is up to date and includes the latest modifications to the project. This is particularly important when you want to see immediate changes reflected in the service's behavior, as relying solely on cached layers might not always capture all updates.

`Step 2`: Start the Build of the modified "**django-todo-app-delivery**" job.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692367780585/eafafda1-5955-4f0f-b9dc-edd0d03ea909.png align="center")

You can see the #3 build has been successful, now I can build this job as many times as I want and there will be no "**port conflict error**".

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692367905907/01180e4a-267c-4599-8002-aa9f87cce5cf.png align="center")

---

# 📍Exercise

Here is a fun exercise for you:

1. Fork this repository [Django-todo-cicd](https://github.com/LondheShubham153/django-todo-cicd) to your GitHub.
    
2. Make some changes in the index.html file (or preferably changes that are instantly visible like HTML or CSS).
    
3. Commit these changes.
    
4. Build this Jenkins Job and see if the changes are instantly visible or not.
    

📝**Note**: Make sure the link you have provided while Configuring the Jenkins job is the link to your GitHub repository where you will make the changes.

---

# 📍Implementing CI/CD (Deployment) with Jenkins: Node Todo App Freestyle Project

We're setting up a Jenkins Job for deploying the Nodejs todo app with Continuous Deployment. This will automatically trigger the action to build the Jenkins job as soon as changes are committed to the code.

`Step 1`: Fork this GitHub Repository [https://github.com/LondheShubham153/node-todo-cicd](https://github.com/LondheShubham153/node-todo-cicd) to your GitHub account.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692370975836/dd006e1c-fc4b-4918-8f0f-de58b73289f8.png align="center")

`Step 2`: Create a new job by clicking on "**New Item**", give a name to the job "**node-todo-app-deployment**", and select "**Freestyle Project**"

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692372016906/c63f28ff-2381-43d5-8f93-d1b6b26e4d79.png align="center")

`Step 3`: Add a Description about this Jenkins job and select it as a "**Git Project**" and provide the URL of your forked GitHub repository in the "**Project URL"** section.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692372396507/33d85601-d98c-482c-a471-42d1514845da.png align="center")

`Step 4`: Go to the "**Source Code Management"** section and select "**Git**" Add the **HTTPS** URL in the Repository URL field.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692372700140/0ce9362e-0d00-4af2-8aca-5cd8bf2869e7.png align="center")

Add the branch you want to build here there is only one branch master.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692372765729/b828b9ce-b077-490b-830f-6fb284712c30.png align="center")

`Step 5`: Scroll down to the "**Build Triggers**" section and select "**GitHub hook trigger for GITScm polling**"

This option is available because we have a GitHub plugin installed.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692373434590/39a182b6-092c-4601-88be-45ae5d74b078.png align="center")

`Step 6`: Go to your GitHub repository "**Settings**"

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692373509660/979a35e6-dffd-44e8-b05e-34fd355b242a.png align="center")

`Step 7`: Select "**Webhooks**" at the left and select "**Add webhook**".

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692373567933/21354155-8a7a-4b93-8bd7-03237213fff7.png align="center")

`Step 8`: In the Payload URL add the URL of your Jenkins Web Interface in this format:

* `<jenkins_url>/github-webhook/` and select the push event as the trigger for this webhook.
    
* Select this option: **Just the push event**.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692373704330/36df99c5-82a0-449a-9ff5-f7488a1529f6.png align="center")

`Step 9`: Add click on "**Add webhook**" Your webhook has been added.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692373993127/290c22dd-01d3-479a-ab96-1eace3a264ce.png align="center")

Refresh the page and you will see a tick mark at the beginning of your Webhook indicating that it is active.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692374190720/26393c28-85dd-4655-aba6-421bb5fbb1d1.png align="center")

`Step 10`: Come to the Jenkins server in the "**Build section**" and select "**Execute shell**"

We will be writing the same commands as we did for the Django-app

```bash
echo "Code cloned"
docker-compose down
docker-compose up -d --no-deps --build web
# Check in the docker-compose.yml file the service name is "web".
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692374290911/aac94517-7adf-4bc7-ae5d-3d613dab9977.png align="center")

Click "**Save"** Your Job is created:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692374530913/e42aa4e8-439c-4a81-ad5e-36e184150055.png align="center")

Now let's make commit some changes to the code.

While committing the code keep the Jenkins tab and the GitHub tab side-by-side like this:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692374755912/006702ee-d688-4b6a-a613-d4f050efe03e.png align="center")

Making changes:

Going into the `todo.ejs` file inside the **views** directory.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692379363586/68563a46-d87b-4285-96c8-353380257ae0.png align="center")

Changing the `<h1>` tag:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692379503770/12d059d5-c7e3-487c-a765-79c0bf44b638.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692379546710/441d4404-6945-4762-92fd-9bdf4cce0978.png align="center")

Committing the changes:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692379597768/33c1489a-2fc7-43f7-88b7-fe39af750788.png align="center")

You can see as soon as you commit changes the build process has been automatically started via Webhooks.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692379686300/f999682c-052b-4b71-a48a-f9790ee397d8.png align="center")

After the build is successful you can see the app has been deployed with the latest commit.

I apologize for the inconvenience but the changes made in this file were not being reflected therefore I configured the "**django-todo-app-delivery**" job by adding Webhooks following the same steps as we discussed earlier.

Try to configure this Django job by yourself.

Made changes in the `index.html` file by adding `!!!!`

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692380035777/4c3b5386-449e-4b4b-b930-13f94c50bb03.png align="center")

The Jenkins job was automatically built and the changes were reflected:

This **#6**th build was automatically triggered as soon as the changes were committed.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692380147033/3a4660f9-f639-44a5-a395-21ef0484e9b1.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692380095086/15ee15dd-0e57-4409-bbc6-5407c5db0a47.png align="center")

---

# 📍Conclusion

Thank you for reading this blog! 📖 Hope you have gained some value. In the future blog, we will be creating and exploring Jenkins pipelines.

If you enjoyed this blog and found it helpful, please give it a like 👍, share it with your friends, share your thoughts, and give me some valuable feedback.😇 Don't forget to follow me for more such blogs! 🌟

---