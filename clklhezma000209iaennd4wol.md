---
title: "Mastering Git & GitHub: A Comprehensive Series on Version Control and Collaborative Development (Part 3)"
datePublished: Thu Jul 27 2023 18:22:15 GMT+0000 (Coordinated Universal Time)
cuid: clklhezma000209iaennd4wol
slug: mastering-git-github-a-comprehensive-series-on-version-control-and-collaborative-development-part-3
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1690482044031/a612e6d7-e2f2-410b-a339-390c493bf71f.png
tags: github, git, 90daysofdevops, day11, devopsjourney

---

---

# 📍Introduction

📚 Welcome to Part 3 of my Git & GitHub blog series! From some intermediate knowledge we have gained about Git & GitHub in my previous blog, it's time to dive deep into branches, best practices, merging, rebase, and some more advanced concepts of Git & GitHub. Get ready to collaborate, version, and contribute using Git & GitHub! 🚀

Git & GitHub is crucial for DevOps so, continuing this DevOps journey let's take a deep dive into it and accelerate your journey to become a great DevOps engineer! 🚀

---

# 📍Branching

## ✔Best Practices

* To add any new feature or solve an issue/bug you should make a new branch and commit those changes in the branch and then after finalizing the changes merge the commits into the main branch via a pull request with a short and accurate description of your changes.
    
* Remember one pull request one commit or commits under a single topic rule. If you make many changes in your branch and commit them and create a pull request to merge those changes. It will be very difficult for the owner to review those changes.
    
    Therefore, one should always stick to one commit or commits that come under the same topic in a pull request.
    

## ✔Understanding git branches in-depth.

* "**HEAD**" - The HEAD branch represents the currently active or checked-out branch
    
* A **default** branch is present in every repository called `main` in the GitHub repo and `master` in the local Git repository where all the changes in the project are tracked via a commit after finalizing the changes by the owner of the project.
    
* **Local & Remote branches** - Local branches are the branches created on our local repository. Remote branches are the branches created on the GitHub repository they are mostly for synchronizing with the local branches. We mostly work on our local branches and push or publish these branches on our GitHub.
    
* A **copy** of the main branch is created when you create a branch from the main branch.
    

## ✔Branch commands:

1. `#git branch <branch_name>`: Creates a new branch
    
    If you want to create a branch at a particular commit you can do this:
    
2. `#git branch <branch_name> commit_id`: It creates a branch from this `commit_id` commit. This branch will have a copy of the main branch from the point where this `commit_id` commit was made.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690446471252/08c10d98-ff16-4323-adaf-3dd0b6d43906.png align="center")
    
    2 commits were made in my local repo, I wanted to create a branch from the point where the first commit was made where the file `Day-02.txt` was added. Therefore, I copied that `commit id` and pasted it into the branch command
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690446613738/561f7e7a-6af4-486e-a6da-049caeaa98e5.png align="center")
    
    You can see I have a copy of the project from the main branch when `Day-02.txt` was added.
    
3. `#git branch -d <branch_name>`: Deletes the branch. It should not be the branch that you are in i.e. currently active. If you try to delete a branch you are currently active in it will give an error:
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690446840815/cc78352d-7db6-4823-9f55-771716536ce4.png align="center")
    
4. `#git branch <remote_repo> --delete <remote_branch>`: Deletes the remote branch from your local repository.
    
    Keep in mind if you are deleting a remote branch then you should also delete the local branch which is tracking the deleted branch.
    
5. `#git checkout <branch_name> or #git switch <branch_name>`: Switch to branch `<branch_name>` from the currently active branch. Use the `switch` command to switch branches as it is its only purpose, unlike `checkout` where you can create as well as switch to a new branch simultaneously using the `-b` option.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690447555501/a3c4799a-a335-4a0f-9c62-1664cb5c836a.png align="center")
    
6. `#git branch -m <old_branch_name> <new_branch_name>`: Renames the `<old_branch_name>` to the `<new_branch_name>`. If `old_branch_name>` is not mentioned it will rename the HEAD (currently active) branch.
    
7. `#git push -u <remote_repo_GitHub> <local_folder>/<local_branch_name>`: It publishes the local branch on the remote repository on GitHub. The `-u` flag is used to obtain a tracking connection between the local and the remote repository.
    
    (📝Note: To execute this you need a remote repository added to your local repository. (Explained in the Part1 add link) You can create remote branches by uploading these local branches to the remote repository using `#git push`. But, you cannot directly create a remote branch from your local repository.)
    
    Now I have the branch on my remote GitHub repository:
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690454200920/69f3cc5d-dda4-4824-ab7e-e2149670d501.png align="center")
    
    Since we used the `-u` flag with the command it tells git to establish a tracking connection this will be very useful for us as we can now directly use the git pull or push command without specifying the local and remote branches.
    
    We can also download a remote branch into our local repo by:
    
8. `#git branch --track <remote_branch> <remote_repo>/<remote_branch>`: This will create a local branch named `<remote_branch>` same as the one in the remote repository and this local branch will track the remote branch. Example:
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690455368735/9959c405-1764-4757-a5ce-99fbe205ea95.png align="center")
    
    I created a new branch named `new_branch` on my GitHub repo which is connected with my local repo. To update the changes made in this remote repo I will execute the `#git pull` command on my local repo. Then I will use the above command:
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690455537303/3e3c7184-8657-48a6-982e-b87a56ab8d77.png align="center")
    
    You can also use `#git checkout` to download the remote branch and you do not even have to give the name of the branch you want to download. For example for the same situation above I will use the:
    
    `#git checkout --track origin/new_branch`: This will also create a local branch of the same name as the remote branch we are downloading.
    
9. `#git push`: Used to update the changes made in the local branch to the remote branch.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690456539648/582c5b6e-c3bb-4e8d-a29c-bb7d3ceefcdf.png align="center")
    
    Now these commit on the local branch are pushed to the remote branch:
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690456619399/7dd9db70-001c-48e6-8cc6-956fe4b140cb.png align="center")
    
    As you can see `branch1` branch in the remote branch has a `test.txt` file.
    
10. `#git pull`: Used to update the local branch from the changes made in the remote branch.
    
    Similarly, the changes made by any branch on the remote repo can be updated to the local branch by the `pull` command.
    
    Since we have already established a tracking connection between these branches using the `-u` flag once now there is no need to specify any parameters.
    
11. `#git branch -v`: Lists all the branches present in the local repo and also displays if it is ahead or behind the remote branch.
    

## ✔Merging Branches

Integrates the changes from another branch into your current HEAD branch. For that, you must be at the branch where you want to receive the changes.

1. `#git merge <branch>`: Merges the changes in the `<branch>` branch with the current HEAD branch.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690458229730/3f598aa6-a078-43b1-94b0-1cb9295c8367.png align="center")
    
    You can see that `new_branch` does not contain a `test.txt` file in it. I want to integrate the changes in the `branch1` branch inside the `new_branch`. Therefore, I will switch to the `new_branch` and then execute the command `#git merge branch1`:
    
    But it is giving me this commit message window:
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690458663213/f4c48d4e-bebe-4800-9dca-f78cf5f7adbd.png align="center")
    
    Because merging produces a merge commit (not always) therefore, it is showing me this commit message in the editor to edit this commit message. I can save this by doing `:wq`. Then it will be merged successfully.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690458919828/ff583557-4543-4f53-ad73-0723e4647fa3.png align="center")
    
    As you can see this will not delete the branch, it will just merge the changes.
    

## ✔Rebasing branches

Rebase does a similar thing as merging but the branch after merging the commits of that branch it will look like a straight line. Let's understand it better by doing the same thing we did using merge, with rebase.

Here, we have a similar situation as before used where `branch1` contains a `test.txt` file that is not present in `new_branch`. I will merge the changes in `branch1` into `new_branch` using rebase. Unlike in merge here I will be on the branch from which the changes are merged and mention the branch receiving the changes inside the command:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690461516490/20e57a2a-961a-4333-9ed0-7fb2cc229c39.png align="center")

---

# 📍Rebase vs Merge

## ✔Merge

Merging a command means that there will be a new commit created i.e. a merge commit where the commits of the other branch will merge with the main branch. For example:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690480502163/59d2b1db-cf25-40d7-ab29-311363765e7f.png align="center")

Here, the commits made in the feature branch will merge into the main branch as a new merge commit - in this case, C6. But the commits in `#git log` will be shown as C1-&gt;C2-&gt;C3-&gt;C4-&gt;C5-&gt;C6. This is how the commits will be merged when `#git merge` is used.

## ✔Rebase

Rebasing is similar to merging but it will be more in a straight line i.e. it will move the entire feature branch at the tip of the main branch.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690481161815/ecfd2c7d-8268-456a-a2fb-f19fc85f87e2.png align="center")

C3 and C4 were the commands in the feature branch which is now rebased at the tip of the main branch. The flow of the commit in the git log will still be C1-&gt;C2-&gt;C3-&gt;C4-&gt;C5-&gt;C6. But the history of the commits that were made in the `feature` branch will be gone whereas the `merge` command preserves the history.

---

# 📍Merge Conflict

A merge conflict can occur when the same changes were made in the same file by two separate branches so while merging it will throw a merge conflict since it does not know which one to pick.

You have to manually resolve this merge conflict by making some changes.

*(I'll soon update the hands-on part)*

---

# 📍Revert & Reset

## ✔Reset

If you want to go back to the previous version of your file and undo your commit you can use the `#git reset <commit_id>` command.

Let's take an example: I made 3 commits in my master branch:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690478114817/0db07b31-bd41-4094-a281-ab07cdca5ae3.png align="center")

But now I want to undo the commits and go back to the file when the m1 file was added for that I will copy the commit\_id of the commit where the m1 file was added and execute the command:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690478325740/68895f6c-5520-4ee0-84fe-9f84fe06af5e.png align="center")

Now my file is at the stage when the m1 file was added and the other 2 commits were added to the unstaged area in the untracked files. I can remove these changes and not track them by doing `#git add .` then `#git squash` and `#git squash clear`, or I can commit those changes again.

## ✔Revert

If we made a commit to the repository and then I realize that the changes made were not desired changes but the changes are committed so to take back this commit we can use the revert command.

📝Note: We can remove not only the latest but any commit we want to, using the revert command.

`#git revert <commit_id of the commit you want to remove>`

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690479463672/abd3395f-c0cb-424b-b786-c1cdf1d45dff.png align="center")

Here, I reverted the commit where the m1 file was added. This will not delete the commit instead create a new commit saying the reverted commit was removed:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690479572624/7bc3135b-20e7-4fa8-9a64-e618f4d91764.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690479661191/869b6745-668d-4b6c-8654-2bc519c238ef.png align="center")

Now you can see the master branch only contains files m2 and m3.

---

# 📍Cherrypick

Whenever you integrate commits you do it on a branch level using commands like merge or rebase to integrate changes from one branch into your current branch. But in some situations, you might only want to commit some changes rather than all the changes from a branch.

### Q) When to use cherrypick?

Ans - A situation where you accidentally commit the changes to the branch you are not supposed to, in this scenario you can use cherry-pick command. Let's see an example:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690463052086/0c6763fe-1eb2-4ea6-8cb5-79133b08268a.png align="center")

Here, branch1 has committed the changes to the master branch instead of new\_branch which was not supposed to happen. Therefore I will use cherry-pick for that, I will go to the branch where the commit was supposed to happen and then execute the command:

`#git cherry-pick <commit_id>`

---

*(I apologize for the explanations not being up to the mark. I know this blog lacks some practical hands-on scenarios which would have helped you to understand it better...I'll keep learning and gain more knowledge and soon update this blog with some more hands-on)*

---

# 📍Conclusion

Thank you for reading this blog! 📖 Hope you have gained some value. You now know some advanced Git & GitHub concepts. Keep practicing these concepts, learn Git & GitHub best practices, and get familiar with Git & GitHub explore. 💻Stay tuned for more valuable content coming your way!

If you enjoyed this blog and found it helpful, please give it a like 👍, share it with your friends, do share your thoughts, and give me some valuable feedback.😇 Don't forget to follow me for more such blogs! 🌟

---

# 📍Reference

* [Git Branches Tutorial by freecodecamp](https://www.youtube.com/watch?v=e2IbNHi4uCI&list=PLLJ1hZKyeCH1I8dP0UNTpWoIhsl6KpVbu&index=3)
    
* [GFG- Git Tutorial](https://www.geeksforgeeks.org/git-tutorial/?ref=lbp)
    

---