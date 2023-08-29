---
title: "Git & GitHub Cheatsheet: Compiling my Knowledge"
seoTitle: "Your Go-To Git & GitHub Cheatsheet: Boosting Productivity in Developme"
datePublished: Wed Aug 02 2023 03:44:11 GMT+0000 (Coordinated Universal Time)
cuid: clkt6owss000209ifalnrapav
slug: git-github-cheatsheet-compiling-my-knowledge
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1690946172737/82fdce1b-088c-48bc-8cae-b74cba8bddb7.png
tags: gitcheatsheet, devops-journey, 90daysofdevops, day12, trainwithshubham

---

---

# Git & GitHub Terminologies

* **VCS**: Version Control System that tracks the changes made to a file and for every changed file creates a new version of it. It also allows us to go to the previous versions of the file.
    
* **Git**: It is a VCS tool that stands for **Global Information Tracker** and allows us to maintain a version history in a folder for our files. It is primarily used for code management and allows you to collaborate.
    
* **Repository**: It is a 'root/base' folder where Git is initialized and now, any changes made in this folder will be tracked by the git. The `.git` folder is created when we do `git init` making the folder a Git repository.
    
* **Branch**: It is a flow where the version history i.e. the changes made in the project are tracked. The default branch is the main or master branch. Developers who want to make changes in the file create a separate branch from the default branch and make changes so that the project inside the main branch is not affected.
    
* **Untracked files**: The files whose changes are not preserved in the repository come under untracked files.
    
* **Commit**: These are the saved/tracked changes in the repository. The versions maintained inside the repository are nothing but a hash i.e. commit\_id for these commits. These commits are shown on the branch of the project.
    
* **Stage**: It is an environment between the file system where there are untracked files and VCS where the version history is maintained. To commit the changes so that it goes to the VCS environment we have to put the file in this Stagining environment. Here we decide whether to track or untrack these changes.
    
* **HEAD**: It is a pointer that points to the currently active branch's latest commit i.e. it points to the current version of your file.
    

---

# Git commands

* `git init`: To initialize a Git repository inside a folder.
    
* `git status`: To check for any changes made inside the repository.
    
* `git add <filename> or .`: To add a particular file by typing `<filename>` or `.` for all the untracked files to the staging environment.
    
* `git rm --cached <filename> or git restore --staged <filename>`: To remove the files from the staging area and put them back as untracked files.
    
* `git commit -m "message"`: To commit the changes made with a message. Once committed it will be considered as the new version. It will commit all the changes in the staging area.
    
* `git restore <filename>`: To restore the previous version of the file `<filename>` if the changes were not committed. Even if the file was deleted we can restore that file using this command.
    
* `git log`: It will list all the changes committed inside the repository along with some metadata like time, author, date, message you gave along with the commit, etc. Along with the commit id, it is in hash format because every commit needs to be unique. This commit id represents the version of that file.
    
* `git log --oneline`: It will list all the commits made in one line and it will also make the commit id small, but it will only show the commit message along with it.
    
* `git log --oneline --pretty`: It will list all the commits just like `git log` along with the metadata but the commit id will be small.
    
* `git log --all --pretty --graph`: It will visualize all the commits in all the branches along with the merge commits in a graph format.
    
* `git config --global user.name "Username"`: This will set the author as `"Username"` in the commit block. Use your GitHub account username.
    
* `git config --global user.email "GitHub-email"`: This will set the author's email as `"GitHub-email"`. Use the email through which you have a GitHub account.
    

---

# Git Branching commands

* `git branch <branch_name>`: Creates a new branch from your current active branch with the name `<branch_name>`.
    
* `git checkout <branch_name>`: You will switch from the current branch to the `<branch_name>`. Your HEAD pointer will now be pointing to `<branch_name>` branch.
    
* `git checkout -b <branch_name>`: It will create a branch and will be the currently active branch.
    
* `git branch`: Gives you the list of branches currently existing in your repository and also points to the current active branch using the `*` pointer.
    

---

# Remote Repository on GitHub

* `git clone <HTTPS_URL>`: It will clone the GitHub repository with `<HTTPS_URL>` URL into your local folder where a Git repository has not been initialized.
    
* `git remote -v`: Shows all the remote repositories in your local repository.
    
* `git push <remote_repo_name> <branch_name>`: It pushes the changes made in your local repository to your remote repository at the `<branch_name>` branch.
    
* `git pull <remote_repo_name> <branch_name>`: It is used to pull the changes committed in the remote repository to your local repository from `<branch_name>` particular branch.
    
* `git fetch <remote_repo_name>`: It is used to pull all the changes committed in the remote repository to your local repository from all the branches.
    
* `git remote set-url <remote_repo_name> <new_url>`: It is used to change the URL of the `<remote_repo_name>` repository.
    
    *📝Note: When you clone or add a remote repository public or private you are not allowed to push the local changes to the remote repository to do that you have to ask the project owner to give you a* `Personal Access Token (PAT)`*. You can add this token to your remote repo URL like this:* `https://<token>@<github_account_name>` *and set this URL as your remote repository URL using the above or below commands.🖊*
    
* `git remote set-url --add <remote_repo_name> <new_url>`: It is used to add a new URL to the existing URLs for the remote repository.
    
* `git remote set-url --delete <remote_repo_name> <url>`: It will delete the `<url>` URL of the repository.
    
* `git remote add <repo_name> <repo_url>`: To add a remote repository to your **existing** Git repository in your local system.
    
* `git revert <commit_id>`: Goes back to the previous version of `<commit_id>` and creates a new revert commit for reverting this `<commit_id>`, preserving the history of the file.
    
* `git reset <commit_id>`: It goes back to this `<commit_id>` version and erases the history of all the commits made after this `<commit_id>`.
    
* `git merge <branch>`: It will merge the latest commit from the `<branch>` branch to the current active branch as a new merge commit.
    
* `git merge <branch> --squash`: It will merge all the changes from the `<branch>` branch to the current active branch at the staging area.
    
* `git merge <branch> --rebase`: It will merge all the commit history in sequence from the `<branch>` branch at the end of the latest commit in the currently active branch.
    
* `git cherry-pick <commit_id>`: It will only merge `<commit_id>` to the currently active branch.
    

---

# 📍Conclusion

Thank you for reading this blog! 📖 Hope you have gained some value.

If you enjoyed this blog and found it helpful, please give it a like 👍, share it with your friends, do share your thoughts, and give me some valuable feedback.😇 Don't forget to follow me for more such blogs! 🌟

---