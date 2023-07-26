---
title: "Git & GitHub: A Comprehensive Series on Version Control and Collaborative Development (Part 1)"
seoTitle: "Mastering Version Control with Git & GitHub: A Guide for Developers"
datePublished: Tue Jul 25 2023 14:06:47 GMT+0000 (Coordinated Universal Time)
cuid: clkidercy00050amj1i5se4e1
slug: git-github-a-comprehensive-series-on-version-control-and-collaborative-development-part-1
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1690284082518/7bcff7de-879d-402b-b691-0276718bbd8a.jpeg
tags: github, git, devops-journey, 90daysofdevops, day9

---

---

# 📍Introduction

📚 Welcome to my blog series on Git & GitHub! Every programmer beginner or experienced should have an understanding of Git & GitHub concepts and should be comfortable with them. This blog will help you to learn and refresh your Git & GitHub concepts. Get ready to collaborate, version, and contribute using Git & GitHub! 🚀 My series will start with the basics and gradually progress to advanced topics, making it easier for you to grasp the concepts and build upon them.

Git & GitHub is crucial for DevOps so, continuing this DevOps journey let's take a deep dive into it and accelerate your journey to become a great DevOps engineer! 🚀

---

# 📍Scenario

Let's assume a scenario that will be helpful to understand these Git & GitHub concepts, features, and their utility in a real-world scenario. This scenario will be used as an example throughout this Git & GitHub blog series.

Together with some of my college friends, I decided to build a website. Since each of my friends has their share of knowledge in UI/UX, frontend, backend, databases, cloud, DevOps, etc. Any website we decided to build would be much more enhanced and sophisticated if we work on it together. For this, we needed a place or a platform where we can collaborate and work on our website individually at the same time. We also needed a utility or some software that can track the changes made to our website by telling who made the change, at what time, and the date. Also, it would be great if we can also version our website so that as our knowledge in our respective technical stack increases we can add some new features to our website and release it as a new upcoming version.

Guess what??

Yes!!!! There is a utility and a platform where all my friends and colleagues can collaborate known as Git & GitHub. Since a similar is the case in big tech companies where 1000s or more employees are working on a single project at the same time they use this tool called Git & collaborate using GitHub. Therefore, we say every programmer must know about Git & GitHub.

Let's just now dive deep into understanding Git & GitHub.🚀

---

# 📍Git

## ❓Q) What is Git❓

Ans - Git is a utility or a tool that is used to version our file or folder. This folder can be anything it can be a source code for a website, an application, a Python file, or simply a text file. Using the Git tool, we can version this file i.e. we can track and save changes done to this file, and we can know who made the changes, at which date & time, and what changes were made, we can also revert to the previous versions of a file if there is a need or an error occurred. These features are utilized via Git commands.

Therefore, Git is called a VCS - Version Control System. So, Git is a version control tool that provides various features like versioning and many others using Git commands.

---

# 📍GitHub

We have a folder that has git initialized in it, but whatever changes I do in this folder will be happening locally and all the git versioning features will happen and be stored locally.

❓Q) How will others work on this same folder at the same time❓

Ans - To achieve this collaboration of multiple individuals to the same file/folder, or a project. We need a platform where this project can be stored and which utilizes the Git features so that, we can copy this project in our local computers make changes in it, and push these changes (made on our local computer) to the platform where the original project folder is stored.

For this, there are many platforms like:

* Bitbucket
    
* GitHub
    
* GitLab
    
* Beanstalk
    
* Amazon AWS CodeCommit
    
* Codebase, etc.
    

We will be learning GitHub because it is the most widely used and provides many interesting features along with it. GitHub's website looks like this:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690269131127/470a4f8f-12f1-4b92-b57e-aa7103650782.jpeg align="center")

## ❓Q) What is GitHub❓

Ans - GitHub is a platform where programmers can collaborate on a particular project. It is a website that helps us to host our projects as a Git repository. Where it provides various features to share, and collaborate in this project folder and store the versions of this project folder using git features inside a Git repository.

### ❓Q) What is a Repository❓

Ans - A repository (or repo) is a folder, a centralized space where all the data is stored, organized, and managed.

The folder in our local machine which we read in the Git section can use Git features only when this folder contains a Git repository where it can store the history of the changes made in our project and version of the project. This Git repository is saved as a `.git` folder in which the data will be stored, organized, and managed. In Linux and MacOS the files that start with `.` are hidden files.

You can see the hidden file using the command `#ls -a`. Windows users can execute the Linux commands using GitBash.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690292158582/0c776cfe-9840-4062-a1b1-ad53baaec5ac.png align="center")

Let's see how to use the Git & GitHub features using Git commands.

---

# 📍Difference between Git & GitHub

Git is a VCS - Version control system that helps us to version any folder by tracking the changes made to the folder over time and also resetting the folder as it was at a particular time. We can achieve this by using git commands, to run git commands git should be installed in your system.

GitHub is built on top of Git which is a website and provides a platform for developers to host their projects as a Git repository for free. GitHub provides a GUI using which all the git operations performed on our local system using the git commands can be done in it. By hosting the git repository on GitHub developers can share their code so that other developers can contribute to it.

---

# 📍Git Terminologies

Before jumping into git commands there are some basic git terminologies that you need to get familiarized with for a better understanding.

1. **Branch**:
    
    * **Main or master branch**: This is a branch that contains the original folder, and the changes made are committed in this main branch only after properly testing and finalizing the changes.
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690270191310/2caa7820-f846-4de7-a5a8-a8848ffbcfce.png align="center")
        
        This is the flow of the main branch where C1, C2, and C3 are the changes committed to this branch. Only the owner and the people who have access to a project can commit changes directly to the main branch.
        
    * **Other branches**: These branches are coming from the main branch created by a collaborator who wants to add a new feature or fix an issue or a bug. Since this branch originated from the main branch, it will have a copy of the main branch so that the user can make whatever changes he/she wants and the original folder in the main branch will not be affected.
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690270343958/2981ff74-3873-47eb-bf45-1328a985c3f4.png align="center")
        
        So, here a varun branch is created separate from the main branch which will have a copy of the main branch till C2, and now we can make whatever changes and commits we want in this varun branch as this will not affect the main branch. You can update your copy of the project from the main branch if any changes are made in the main branch.
        
        📝Therefore, it is said that whenever you are collaborating on a project and making any changes to it create a separate branch and see it's working with the copy of the main file in your branch before merging the changes in the main branch.
        
2. **Staging Environment**: When the changes made to the folder by the collaborator are completed. We want to add these changes to the main folder. For this, we have to do two things:
    
    1. **Stage**
        
    2. **Commit**
        
        Before committing the changes the changed files should be moved to the staging environment. After that, these files are ready to be committed
        
3. **Commits**: Commits are nothing but to save the changes made in our repository.
    
    For example, I made a change in the project file, but these changes are not stored in my Git repo. For that, I add these changes to a Staging environment. Then from the stage, I commit these changes so that these changes get recorded and stored in my Git repository. Now, if I share this project folder with someone then the updated folder with the changes committed will be sent. Therefore people can see the updated folder as well as see who made these changes.
    
4. **Untracked files**: These files are the files that have been added or modified but not saved. To save these we would have to commit these changes.
    

---

# 📍Git Commands

These git commands are executed on your local computer. To execute git commands git should be installed on your machine. In Linux & MacOS git is already installed for Windows you can install git by visiting this [website](https://git-scm.com/download/linux).

1. `#git init`: To initialize an empty git repository inside a folder.
    
    I have initialized an empty git repository in my `project` folder. Now, I can track the changes made inside this project folder.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690271093846/18738f17-aca1-4cac-bc90-a1d3a33f4e06.png align="center")
    
    *📝Note: When I do* `#git init` *in my project folder, then the git will only monitor the changes made in this project folder. It will not affect the folders outside this project folder.🖊*
    
2. `#git status`: Displays if there are any changes made in the folder containing the git repository.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690271364922/c06f2538-bac9-44bd-a047-5d8f71fd387e.png align="center")
    
    Since I haven't made any changes it is an empty repository therefore, it is showing this prompt.
    
    I will create a folder named `test.txt` which will be seen by Git and then the `#git status` command will give detailed information on the changes I have made in this project folder.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690271707665/12221489-e4ad-4cd8-a083-2c2a966087c1.png align="center")
    
    `#git status` is displaying the prompt telling the changes have been made but these changes are not saved in the history of the git repository i.e. not committed and these non-committed files are shown under `Untracked files`.
    
3. `#git add <untracked file_name> or '.' (character for all the untracked files)`: This adds the untracked files in the staging environment.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690271993294/5354b0fc-a978-49e8-8a1a-1efe237a4056.png align="center")
    
    The Untracked file `test.txt` has turned green which means it is now in the staging environment and ready to be committed.
    
4. `#git commit -m "message you want to display in the repo"`: These will save the changes made to the folder in the git repository. `-m` is used to print the message you want to display along with your commit.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690272269342/04ba94a4-d0f0-481b-97bf-81a75738317b.png align="center")
    
    Now, when I do `#git status` It is showing the prompt no untracked files or no files ready to be committed.
    
5. `#git restore --staged <file_name in the stagged environment>`: If you want the file to remove from the stagging environment.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690272423154/245bc953-2dd8-40b8-972d-23041368ba70.png align="center")
    
6. `#git log`: Displays the history of the project. Lists all the commits made with time.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690272559462/7b0ebce3-8a53-45e3-9c9a-5213da26ff7a.png align="center")
    
7. `#git reset <commit id>`: If you want to restore your project as it was at a particular time you can do it using this particular command. Paste the commit id of the project you want to restore.
    
    All the other commits done after that commit will be restored to the staging area.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690272701875/ede886c5-2ab1-47de-91cd-f3fc0606e6b0.png align="center")
    
    I wanted to reset my project folder at a time when it only contained the `test.txt` file. So I copied the commit id where I added the `test.txt` file and used the `#git reset` command to restore my folder as it was before.
    
    Now, as you can see the test2.txt file that was committed has been removed and is now under the untracked files list i.e. outside the staging environment.
    
    Therefore, this command `#git reset <commit id>` is also used to remove the commits which were made by mistake.
    
    Now when I do the git log I will only see the commit with `<commit id>` mentioned in the command. It means the project folder was restored to the time when this `<commit id>` was made.
    
8. `#git stash`: It deletes all the tracked files i.e. the files which have been added to the staging area. Because there are times when we don't want some changes to commit but we also don't want to lose them. For this, the `#git stash` command is used and we can restore these changes using the next command.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690273190470/cb66cd5c-9b61-49c8-afe0-79133b2cf6ed.png align="center")
    
    As you can see the test2.txt file which was in the staging area I did not want to commit so I moved it to the stash and now `#git status` shows `nothing to commit`.
    
9. `#git stash pop`: It restores all the deleted tracked files done by `#git stash` and takes them back outside the staging environment.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690273363580/5c5fd549-ee80-4985-b823-615dbeee16d5.png align="center")
    
    Now the files which were deleted and moved to the stash are restored to the staging environment.
    
10. `#git stash clear`: Deletes the changes stored in the separate structure by `#git stash` so now we cannot restore them using `#git stash pop`.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690273583855/68c8f119-dad3-41ec-a7db-faff61c9dcfc.png align="center")
    
    After doing `#stash clear` now the test2.txt file has been permanently removed.
    
11. `#git branch`: Lists all the branch present in our repository.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690273903232/be0cacc6-4985-4735-8ad0-690c0036e933.png align="center")
    
    You can see our repository contains only the `master` branch this is the default branch created when the git is initialized. It is mentioned in the command line in blue color `(master)` and also the `*` with branch name in `green` denoting which branch you are currently in.
    
12. `#git branch <branch_name>`: Creates a new branch with the name `<branch_name>`. This is done by the contributor so that it can make changes in a copy of the main file stored in this `<branch_name>` branch thereby not affecting the main branch where the original folder is kept and maintained.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690274057639/52096fb5-fba3-473b-871f-ffa16160a5df.png align="center")
    
13. `#git branch -d <branch_name>`: Deletes the branch `<branch_name>`.
    
14. `#git checkout <branch_name>`: This will make the HEAD pointer pointing to the main branch point to the branch `<branch_name>` i.e. we will switch to the branch `<branch_name>`.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690274147797/aea6c103-6aad-45dd-95fa-200b3fe82704.png align="center")
    
    As you can see the `*` pointer pointing to the master branch previously is now pointing to the `varun` branch.
    
    Now, whatever changes are made and committed will be committed to this `varun` branch and changes will be made in the copy of the project folder which we got from the main branch.
    

The next blog will be exploring Hands-on GitHub practices and understanding some advanced Git & GitHub concepts. Stay tuned for that!😉

---

# 📍Conclusion

Thank you for reading this blog! 📖 Hope you have gained some value. You are now familiar with Git & GitHub basic concepts and the git commands. Keep practicing these commands, and get familiar with Git & GitHub explore more and get your hands dirty by doing hands-on. 💻Stay tuned for more valuable content coming your way!

If you enjoyed this blog and found it helpful, please give it a like 👍, share it with your friends, do share your thoughts, and give me some valuable feedback.😇 Don't forget to follow me for more such blogs! 🌟

---

# 📍Reference

* [Git & GitHub Masterclass by TrainWithShubham](https://www.youtube.com/watch?v=AT1uxOLsCdk)
    
* [Complete Git & GitHub Tutorial by Kunal Kushwaha](https://www.youtube.com/watch?v=apGV9Kg7ics&list=TLPQMjQwNzIwMjOVxis7w-QMSw&index=1)
    
* [Git Terminologies](https://www.atlassian.com/git/glossary/terminology)
    
* [Git remote add vs clone StackOverflow.](https://stackoverflow.com/questions/7574127/whats-the-difference-between-adding-and-cloning-a-remote-repository)
    

---