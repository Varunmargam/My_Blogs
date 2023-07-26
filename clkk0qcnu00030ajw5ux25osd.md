---
title: "Git & GitHub: A Comprehensive Series on Version Control and Collaborative Development (Part 2)"
seoTitle: "Mastering Version Control with Git & GitHub: A Guide for Developers"
datePublished: Wed Jul 26 2023 17:47:25 GMT+0000 (Coordinated Universal Time)
cuid: clkk0qcnu00030ajw5ux25osd
slug: git-github-a-comprehensive-series-on-version-control-and-collaborative-development-part-2
tags: github, git, devops-journey, 90daysofdevops, day10

---

---

# 📍Introduction

📚 Welcome to Part 2 of my Git & GitHub blog series! From the basic knowledge we have gained about Git & GitHub, it's time to do Hands-on to get comfortable with Git & GitHub. And also understand what collaboration and contributing to a project in real day-to-day life looks like. This blog will help you to learn and refresh your Git & GitHub concepts. Get ready to collaborate, version, and contribute using Git & GitHub! 🚀

Git & GitHub is crucial for DevOps so, continuing this DevOps journey let's take a deep dive into it and accelerate your journey to become a great DevOps engineer! 🚀

---

# 📍Hands On

Let's see how we will be collaborating on projects and contributing to them using GitHub.

Let's do a quick recap of what we learned in the previous blog and our current scenario.

We initialized an empty git repository in the project folder on our local machine. But now how will other people make changes in this project folder if it is stored in my local machine? Basically, how can I share this folder containing a Git repository with my friends so that they can contribute to it at the same time?

To solve this we use GitHub where we can host this `project` folder containing the Git repository. So that whoever wants to contribute can contribute to it by copying this public repository into their local machines and making the desired changes. GitHub also provides a GUI for various git commands.

## ✔Creating your Git repository on GitHub

1. To create a repository on GitHub go to click on the New button.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690274468186/18ac4315-a649-4d36-a1d8-99ce6dead572.png align="center")
    
2. Then give the name of the repository. Repositories in an account are displayed as `repository_owner(account)/repository_name`.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690335266502/189779ba-eb67-445a-9b41-585a98210533.png align="center")
    
    I created a repository named `DevOps` on my GitHub account.
    
3. You have the option to make your repository public or private. (As you can see in the above image)
    
    * **Public**: If you make your repo public anyone in the world can access or clone your repository on their GitHub account.
        
    * **Private**: If you make your repo private then you and those whom you have permitted to contribute to the project.
        
4. You can select `README` file to `Add a README file` in your repository in this you can add what this repository is about, the code of conduct to contribute, documentation, etc. And then click on the `Create repository` button.
    
    There you have it!! You have created your first Git repository on your GitHub!!!🥳
    
    📝Note: In GitHub when you create a Git repository the default branch name is called the `main` branch whereas when you create a Git repository on your local machine the default branch name will be `master`.🖊
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690335347420/0b3cb9a2-f901-4d39-8d2e-9d286c0c4310.png align="center")
    
    You can see that the GitHub default branch when a new repository is created is the `main` branch. You can change to a branch, or create a new branch as well.
    
5. Now you can make changes to this repository directly on GitHub by clicking the
    
    `Add file` button and all the changes and things which we were doing on our local machines using the command line can be done on GitHub on a Graphical Interface.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690335620621/a9e3e433-7ed4-428b-b25b-71216ae40e00.png align="center")
    

---

* Pull request:
    
    A pull request is a request made to the owner of the project to merge the changes you have pushed in your branch into the main branch on GitHub.
    
    For the owner to know that you have made changes to his project in your branch you create a pull request with a description of what changes you have made.
    

---

## ✔ Make changes in your GitHub repository from your local repository.

I created my repository named `DevOps` on my GitHub account. Now I want to connect this GitHub repository to my local repository in the `project` folder. So that I can make changes in my local repo and push the changes to this GitHub repository `DevOps`.

For that, click on the `<> Code` button, and in the clone section copy the `HTTPS` URL of your GitHub repository.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690335790927/9767cd5f-c090-4549-b141-27e3a034f885.png align="center")

1. `#git remote add origin GitHub_repo_URL`: Connects the local git repository to the repository on our GitHub account.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690336003105/3f3928d9-c397-4739-9d90-65025d90617d.png align="center")
    
    *📝Note: By convention, all the repositories which are from my account are named as origin.🖊*
    
2. `#git remote -v`: It gives a list of repositories attached to the folder. The above image is showing the list of repositories attached to my project folder with their names. I have only one repository `DevOps` connected to it with the name `origin`.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690336090460/3d538b38-b990-4d1d-9f15-e2def40533cc.png align="center")
    
    We'll look into `fetch` and `push` shortly.
    
3. `git remote rm <remote_repo_name>`: It removes the remote repository from your local repository.
    
4. `#git push <github_repo_name> <branch_name>`: To push the commits made in our local repository to the Git repository on GitHub. Now, you can see your local commits on your GitHub repository inside `<branch_name>`.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690375193767/36f9f46f-7621-49aa-b57f-02417e63df92.png align="center")
    
    The changes I made were, I created a folder `Git` then inside `Git`, I created a file `Day-02.txt` and committed these changes in my local repo. And then I pushed the local commit to my remote `DevOps` repo on GitHub named `origin` from the `master` branch.
    
    But, as you can see I executed the command:
    
5. `#git push <remote_repo_name> <local_branch>:<remote_branch>`: It is used to push the changes made in a `<local_branch>` to the `<remote_branch>` on GitHub.
    

---

I used the above command because if I had pushed the changes using the command `#git push <github_repo_name> <branch_name>` then it would have created a new branch on the GitHub inside the `DevOps` repository named `<local_branch>` and the commits will be pushed to this new branch.

❓Q) What is the problem if a new branch got created you can simply merge this branch into the main branch via a pull request, couldn't you❓

Ans - Yes, you can merge the commits made on a separate branch into the main branch but, if the main branch is empty (like in our case) it will have nothing to compare the changes made between the `main` branch and the `local branch` created on GitHub. It would show something like this:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690376159203/adc532dd-0ce5-453b-93df-d9108d4f8239.png align="center")

And to create a pull request it needs to compare the changes made from the original file and approve if the changes can merge.

Therefore, I used the command `#git push origin master:main` to make the changes from the master branch to the main branch on GitHub. But it doesn't allow this as you can see:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690376665410/6ce6e341-ca40-40b0-a936-277ad91e230b.png align="center")

So, I used the `--force` the option to forcefully push the changes directly to the main branch on GitHub. This is not a good practice when you contribute to an existing project you should always push the changes in your separate branch and create a pull request to the owner to merge the changes. But since this is our account and the main branch was empty and needed some files to be added to initialize, it can be overlooked.

Now you can see the commit has been pushed to the main branch on the GitHub repository.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690377026959/a87cd69e-369a-49db-b7fc-e74be41cf1b0.png align="center")

OR

You can simply utilize the GitHub GUI feature and add or upload files directly on your main branch. As shown below:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690377150975/253b67e6-92e6-4442-8508-12332dfe5d66.png align="center")

Now that our empty repository on GitHub has been initialized by adding a file `Day-02.txt` inside the `Git` folder. Let's make changes in our local repository and try to merge these changes from a separate branch.

I am creating a file named version01.txt inside the Git folder in my local repo:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690377739432/26f8f4a2-c679-41c0-a9cc-691ac0c6607a.png align="center")

Now, I will commit these changes and push the commit to the remote repo DevOps on GitHub using the command `#git push <github_repo_name> <branch_name>`.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690378076058/7e683dbd-8db2-48fc-9220-d66cc6a02770.png align="center")

You can see the local commit has been pushed to the GitHub repo inside the new branch named `master` since we committed these changes from the master branch.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690378303233/99fb8086-d716-4eb8-9e35-0e1d67e08778.png align="center")

Now you can merge the commit to the main branch via a pull request. You can compare and create the pull requests since this repository is owned by you by clicking on `Compare & pull request` as you can see in the above image.

After clicking on it you will see a screen like this:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690378590338/f5089348-d434-43c9-841f-c89ec6a9f6d6.png align="center")

Since there is a file present in the main branch, it can compare the changes made and check if the changes can merge. In the above image, you can see our changes are ✔able to merge.

Then click on `Create pull request` then you will see a window like this:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690378921933/796aeddb-a5c1-4d5b-84c0-21bc8d02cb4d.png align="center")

Click on the `Merge pull request` if you want you can put some comments and confirm the merge and it will be merged in the main branch.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690379096445/7e58eee9-45fb-4907-8889-bcc339b57d83.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690379199219/665cd658-a7cd-4fc4-b6b5-36bfb21bbec8.png align="center")

Congratulations!!🥳🎉 You have made your first contribution!!!

## ✔Contributing to the Existing project hosted on GitHub

To contribute to someone's project which may be public or private hosted on their GitHub repository. You cannot just add their repository to your local repo as we did with the DevOps repo inside our account. It would be very dangerous if anyone can add your project repo to their local machine and make changes to your project. Therefore, there are some security measures the project owner can take and restrict access for people to add to his/her project. Only selected people decided by the owner can have access to and make changes to the project directly.

### ❓Q) But then, How to contribute to the existing projects, if I do not have access to them❓

Ans - For this, you have to "`Fork`" the project.

### ✔Fork

Forking means you are making a copy of an existing repository from another user's account to your own GitHub account. Now you can add this forked repo to your local repo and make changes.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690381141033/ba2d171e-c97c-4e70-96d4-03388909f0a7.png align="center")

You can see in the above image, we have an existing `90DaysOfDevOps` repository from the `LondheShubham153` account. You can contribute to this repository by forking it. Above the `Code`, there is an option to `Fork`. This will make a copy of this repo into your GitHub account. It will look something like this:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690381406930/ba15f147-2b9e-4be7-8cb5-bc6b276a8d39.png align="center")

You can see the repo has been copied to my account shown at the top left corner. This ensures any changes I make will be made in this repo and the original repo is not affected.

📝**Important Note**: By convention, the name of the repository which we have forked from another user's account is called "`upstream`". Similar to how the repository in our account is called "`origin`".🖊

---

### ✔Cloning the Forked repository.

To make changes from your local machine you should be having a copy of this `forked` repository on your local machine so that any changes you make can be pushed to the forked repository. The command to clone is:

`#git clone GitHub_repo_URL(HTTPS)`: Clones the GitHub repository on your local folder where you have executed this command.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690383775562/ffc8e9df-b568-4107-8142-f545da4997c2.png align="center")

I created a `new_folder` outside the project folder and executed the `#git clone <Forked_HTTPS_URL>` command. And clone command created a new repo named `90DaysofDevOps`.

OR

You can directly clone the original repo from the owner's account using `#git clone <HTTPS_URL_owner>`.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690385399128/462bc9e2-e7f7-4e20-bcf4-3144808eec2e.png align="center")

We also can add the original repo that we have forked from the owner's account using the `#git remote add` command:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690385661868/58ff94f3-93fa-420b-9262-c500309ec0a4.png align="center")

But I have named this command upstream because of the naming convention which we discussed earlier in this blog. By doing this, it gives us an advantage.

Suppose there were changes made in the original repo now I would have to merge that changes in my forked repo so that my forked repo is up to date with the original. To update these changes we have a command:

`#git fetch <original_repo_name>`: It will fetch the changes made in the original repo in your local repository. Therefore, you will execute `#git fetch upstream`:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690387626542/914dd9d0-7545-4d1d-8ada-0397345528ea.png align="center")

It fetches the branches and their respective commits from the upstream repository.

And switch to the local master branch i.e. origin using `#git checkout`:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690388423440/c86e29c3-d8c2-48ec-9c29-239d6ceedd2a.png align="center")

Then merge the changes from the upstream default branch, in this case `upstream/master` - into your local default branch.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690388579891/e0093eac-2411-43fe-896e-ea3aa36f58df.png align="center")

OR

You can use the GitHub GUI `Sync fork`, as GitHub gives a notification if your forked repo is not up to date with the original one. Below `<>Code` button:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690388822649/a63e7646-675e-49c8-a71c-504ee1b93389.png align="center")

---

### A question may arise!❓

If both `#git remote add <repo_name> GitHub_repo_URL` and `#git clone GitHub_repo_URL` is used to add the GitHub repository to our local machine then.

### ❓Q) What is the difference between `#git remote add` & `#git clone`❓

Ans - `#git remote add` - It is used to connect the remote git repository on GitHub to the existing git repository in your local machine inside the folder.

`#git clone` - It creates a new repository on your local folder that does not contain an existing git repository.

We have reached the end of this blog, in my upcoming blog we will cover some advanced concepts like squash, rebase, merge, revert, cherrypick, etc. Stay tuned!

---

# 📍Conclusion

Thank you for reading this blog! 📖 Hope you have gained some value. You now have some hands-on experience. Keep practicing these concepts, learn Git & GitHub best practices, and get familiar with Git & GitHub explore. 💻Stay tuned for more valuable content coming your way!

If you enjoyed this blog and found it helpful, please give it a like 👍, share it with your friends, do share your thoughts, and give me some valuable feedback.😇 Don't forget to follow me for more such blogs! 🌟

---

# 📍Reference

* [GitHub Documentation](https://docs.github.com/en)
    
* [Git & GitHub Masterclass by TrainWithShubham](https://www.youtube.com/watch?v=AT1uxOLsCdk)
    
* [Complete Git & GitHub Tutorial by Kunal Kushwaha](https://www.youtube.com/watch?v=apGV9Kg7ics&list=TLPQMjQwNzIwMjOVxis7w-QMSw&index=1)
    

---