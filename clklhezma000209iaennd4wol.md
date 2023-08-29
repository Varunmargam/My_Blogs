---
title: "Exploring Git & GitHub: Learning Version Control and Collaborative Development (Part 3)"
datePublished: Thu Jul 27 2023 18:22:15 GMT+0000 (Coordinated Universal Time)
cuid: clklhezma000209iaennd4wol
slug: exploring-git-github-learning-version-control-and-collaborative-development-part-3
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
    

📝Note: Every branch has its HEAD pointer pointing to the latest commit on that particular branch.

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
    

---

# 📍Revert & Reset

## ✔Revert

Let's understand the `git reset` command with an example:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690902900071/6da9e937-ecad-4659-a92e-9a8461bc483f.png align="center")

I created an empty repository on my GitHub named `Learning_Git` and added it to my existing local repository. Created a commands.txt file and pushed the changes to my remote repository on the master branch.

Then I created a new branch from my master in the local repo and made 3 commits as you can see in the above image but, the latest commit I made is a faulty commit and this commit is now the latest version of the file. Now, I want to return to the previous version of the file where there were no faulty `feature2.txt` files. For this, I will use the `git revert <commit_id>` command. The `<commit_id>` will be of the commit to which I want to revert i.e. return.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690903580264/8dc9755c-66c6-464a-8f1f-068470098736.png align="center")

When I execute the `git revert` command a default editor will open with a commit message that we have to confirm this revert action by saving the file:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690903510456/c84ad19e-beca-45da-b52d-a6de553ad01a.png align="center")

Now when you do `git log --oneline`:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690903844501/2ac69fe4-c3e0-4646-b10b-b983db3848f3.png align="center")

You can see that the revert command created another commit saying the faulty commit was reverted preserving the history of the file. This is good as it provides transparency while working with a team on all the changes made to the file. Along with the new commit, it also went to the previous version where there was no faulty feature added.

This `git revert` command will be very useful since you if there is a scenario where a file was modified with a faulty functionality but the rest of the content was good, you don't want to delete the whole file. Here, you can use this git revert command to go back to the version where there was no faulty functionality added.

## ✔Reset

It is advisable to not use the `git reset` command or you should only use it in some rare emergencies as it removes the file's history. Let's take an example of such a scenario where you have to use the git reset command.

I created a `keys.txt` file where I stored some of my confidential credentials in it. then I created a `feature2.txt` file then added it, and committed these changes without realizing that the `keys.txt` file was also committed with it.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690910158480/d9fbeb52-107e-4d44-9945-d029a8a0ef8f.png align="center")

In this scenario, if I do git revert then the changes will be saved in the file history so, here I can use the `git reset <commit_id>` command, and the `<commit_id>` should be at the point where you want your current version to be. In my case, I wanted to go back to the `revert` commit so I will add the revert commit id to the `reset` command.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690910442386/d602fa99-3b3d-4b43-b655-c3bc21a00c7d.png align="center")

You can see the history of the commit after the `revert` commit has been erased and the commit changes are now back to the untracked stage.

---

# 📍Git Ignore

To avoid the above scenario where you want to keep your credentials in your Git repository but do not want Git to track that `keys.txt` file then you can put it in the `.gitignore` file.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690911254176/ee22ea66-d37b-4940-b8a3-3ddb08ceb8f9.png align="center")

You can see in the above image the git is not tracking the `keys.txt` file because the `.gitignore` file contains the `keys.txt` file.

The `.gitignore` is a special file where all the files mentioned in it are not tracked by the git and cannot be committed. Make sure to commit the changes by adding a `.gitignore` file in your repository.

---

# 📍Merge Branches

We know that the changes committed on one branch do not affect the main branch. So when the changes are finalized and I want to add these changes to the main branch I will use the git merge command to add the commits after the latest commit in the main branch. Let's understand this by continuing the above scenario.

All the commits we made before were in the dev branch so when I switch to the master branch and do git status:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690911896307/c9f631a2-200d-4f00-8dd8-e304809eeb6c.png align="center")

Now instead of creating another .gitignore file and doing the same in the master branch, I will bring the changes made in the dev branch inside the master branch. For this, I will use git merge:

To merge branches first I have to be on the branch where the changes will be added, I want the changes from the dev branch to be in the master branch therefore, I will be on the master branch and execute the merge command:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690912196083/02584274-cb37-44ee-8a57-71e0db7f0b10.png align="center")

You can see all the changes in the dev branch were added to the master branch. Now, when you do git log:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690912288032/7d24c117-7cae-4b4e-a60e-d93eb22ff7af.png align="center")

HEAD is pointing to both the dev and master branch.

## ✔Squash & Merge

I will now switch to the dev branch and make 2 more commits. Now you can see that the master branch already has a long list of commits if this continues then the history will be very long:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690912946032/05682e57-5756-4f23-b737-e8453ac72228.png align="center")

So now, when I will merge the commits from the dev branch to the master branch I will squash and merge it. Squash will make multiple commits into a single commit and will be merged. Using the command:

`git merge dev --squash`

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690913078120/a56f0dc4-7f6d-4bf1-92d2-22d041784b80.png align="center")

You can see the 2 commits of adding feature3 and feature4 was not added to the master branch but the changes were added:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690913268852/fd535493-6316-4f41-97f5-d7d30430ce14.png align="center")

When I do git status these changes are not yet committed therefore, I need to commit these changes:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690942356438/4ac2d191-6de1-487e-a945-db89114ac46b.png align="center")

## ✔Merging branches in GitHub

I added 2 commits creating a feature3.txt and feature4.txt file inside the dev branch in my local repository. I will push these local changes to the remote dev branch on GitHub:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690917632187/51eac9e1-cac2-41f3-b2ae-db84cb4f0116.png align="center")

You can see the changes have been pushed to the GitHub repository:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690917713526/6fca45a7-fc0d-4d0f-8b29-40dfe8f06829.png align="center")

To merge these changes made in the dev branch GitHub is telling me to create a Pull request. And we can compare and merge the changes to the master branch on GitHub which we have seen in my [Python: Empowering DevOps with Automation and Efficiency (Part 2](https://varunmargam.hashnode.dev/git-github-a-comprehensive-series-on-version-control-and-collaborative-development-part-2)) blog.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690942480066/9bcafd70-ef66-40b6-9466-6120cc663eed.png align="center")

You can see there is a merge commit in my GitHub repository.

---

# 📍Rebase Branches

Rebase is similar to merging but it linearly creates the history branch whereas the merge does not.

### Q)In which scenario the rebase command is used?

Let's continue the above example:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690918391997/0d7d190d-7823-4b8b-ac2f-1ffb909e07ea.png align="center")

You can see that the origin master branch in my local repository is not in sync with the remote master branch as the changes we have merged from the dev branch were done on GitHub. The merge commit on the GitHub repository and the squash commit in the local repository are not known to either of them. This is the case where you need the `git rebase` command.

When you have made a certain commit but do not have the commits before that which is in another branch in this case the `git rebase` command can be used as it will merge the commit history in one line.

Therefore, first, the remote changes needed to be pulled to the local repository. And then use the command `git merge <remote_repo> <branch> --rebase`:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690943166090/452abee6-2065-4ead-abfb-18774443ef07.png align="center")

---

# 📍Rebase vs Merge

## ✔Merge

Merging a command means that there will be a new commit created i.e. a merge commit where the commits of the other branch will merge with the main branch. For example:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690480502163/59d2b1db-cf25-40d7-ab29-311363765e7f.png align="center")

**It will merge the latest commit from the dev branch to the master branch with a new commit.**

Here, the commits made in the feature branch will merge into the main branch as a new merge commit - in this case, C6. But the commits in `#git log` will be shown as C1-&gt;C2-&gt;C3-&gt;C4-&gt;C5-&gt;C6. This is how the commits will be merged when `#git merge` is used.

## ✔Rebase

Rebasing is similar to merging but it will be more in a straight line i.e. it will move the entire feature branch at the tip of the main branch.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690481161815/ecfd2c7d-8268-456a-a2fb-f19fc85f87e2.png align="center")

**Here, unlike merge it will merge all the commits made in the dev branch to the master branch.**

C3 and C4 were the commands in the feature branch which is now rebased at the tip of the main branch. The flow of the commit in the git log will still be C1-&gt;C2-&gt;C3-&gt;C4-&gt;C5-&gt;C6. But the history of the commits that were made in the `feature` branch will be gone whereas the `merge` command preserves the history.

---

# 📍Cherrypick

Whenever you integrate commits you do it on a branch level using commands like merge or rebase to integrate changes from one branch into your current branch. But in some situations, you might only want to commit some changes rather than all the changes from a branch.

### Q) When to use cherrypick?

Ans - I made 2 commits where I added a feature5.txt file and a feature6.txt file in the dev branch:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690943887097/a0637216-dd0b-4206-b1ac-5cc76912d676.png align="center")

Now, I want only the 6th feature commit from the dev branch to my master branch. If I use git `rebase` or `merge` but the commits will be added which I do not want. In this case, I will use the command:

`#git cherry-pick <commit_id>`: The `<commit_id>` will be the commit that I want to be merged in the master branch.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690944125801/48a85648-9798-4281-a3ee-42275bb68d13.png align="center")

You can see using the cherry-pick command I merged only the feature6 commit from the dev branch to my master branch.

---

# 📍Merge Conflict

A merge conflict can occur when the same changes were made in the same file by two separate branches so while merging it will throw a merge conflict since it does not know which one to pick.

You have to manually resolve this merge conflict by making some changes.

Let's understand this by creating a conflict first.

I am in my dev branch which is synced with the remote dev branch

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690947829223/dff5df45-a689-4c4f-a923-0e1eecaa4e7a.png align="center")

Now, I modified the feature6.txt file and committed these changes to my local repository but for some reason, I did not push these changes to the remote repository.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690949401307/976f9f29-9b77-4c36-9218-c1b959a90bf3.png align="center")

Now, an individual edited the same file on GitHub and committed those changes on GitHub:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690949671602/e48dd5ff-f3b9-47ad-8179-b58e9173bc5f.png align="center")

Now, when I try to execute the `git pull` command in my local repository Git will get confused about whose changes it should save and will throw an error creating a Merge Conflict:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690949900213/b6aee072-ee28-4d27-aabe-e98ba6a6a26a.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690950082476/22683f80-00bc-4df2-9190-1ca681f3f636.png align="center")

When I do git status it is saying both are modified i.e. from your local and remote both have modified the same file. Open the file in the Vim editor you will see these changes:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690950243771/f31759e5-fcd4-4c62-9c2f-6ede95cba238.png align="center")

It is saying that the HEAD is the feature added in the local by you and the other section is by the other individual on GitHub. To resolve this conflict we need to choose manually which changes I need to keep. Let's say I want to keep my changes then I will delete all the other content except my changes and save & quit the file.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690950490345/23ed9e0a-9214-449f-b9c7-db29a4633e83.png align="center")

I have resolved the commit when I do git status I have two options either `abort` the `merge` or go ahead with the merge:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690950623879/de44b125-0cd7-4bb2-8588-6f213a145b27.png align="center")

Since I have resolved the conflict I will go ahead with the merge with git add:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690950850666/98dc681f-2a4d-42fe-ad80-4e941e73ee81.png align="center")

`git status` now gives the prompt `All conflicts fixed but you are still merging` confirming if you are merging use git commit:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690951102204/57ad8b29-bcc9-4a48-a940-ff7d4cfc8399.png align="center")

And I can pull the changes from the remote dev branch without any conflict.

## ✔Merge Conflict when trying to push changes

This can also occur when you try to push the changes to the remote repository for this you will have to follow the same process by `git pull` on your local -&gt; manually resolving the changes by `vim <file>` -&gt; `commit` it on your local -&gt; `git push` you will get no error or conflict.

## ✔Best Practice to Avoid Merge Conflicts

Always make sure to pull the changes from the remote repository to your local repository before making or committing any changes in the local repository.

---

# 📍Conclusion

Thank you for reading this blog! 📖 Hope you have gained some value. You now know some advanced Git & GitHub concepts. Keep practicing these concepts, learn Git & GitHub best practices, and get familiar with Git & GitHub explore. 💻Stay tuned for more valuable content coming your way!

If you enjoyed this blog and found it helpful, please give it a like 👍, share it with your friends, do share your thoughts, and give me some valuable feedback.😇 Don't forget to follow me for more such blogs! 🌟

---

# 📍Reference

* [Git Branches Tutorial by freecodecamp](https://www.youtube.com/watch?v=e2IbNHi4uCI&list=PLLJ1hZKyeCH1I8dP0UNTpWoIhsl6KpVbu&index=3)
    
* [GFG- Git Tutorial](https://www.geeksforgeeks.org/git-tutorial/?ref=lbp)
    

---