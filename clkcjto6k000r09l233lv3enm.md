---
title: "Exploring Advanced Bash Scripting Concepts"
datePublished: Fri Jul 21 2023 12:19:43 GMT+0000 (Coordinated Universal Time)
cuid: clkcjto6k000r09l233lv3enm
slug: exploring-advanced-bash-scripting-concepts
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1689941510646/bf9507ca-cd5c-4ca6-ab1d-823ffcf509ec.png
tags: bash-script, 90daysofdevops, day5, trainwithshubham, devopsjourney

---

---

# 📍Introduction

👋Hello guys! Welcome back to the exciting journey of Bash scripting! 🔥 This blog continues the comprehensive Bash scripting for DevOps series, exploring advanced concepts and taking your skills to the next level!💪🚀

Before we dive in, ensure you are familiar with basic Linux commands. If you need a refresher, check out my two-part blog series on [Mastering Basic Linux Commands](https://varunmargam.hashnode.dev/mastering-basic-linux-commands-for-devops-excellence-part-1). Also, make sure you understand the basics of bash scripting, covered in my previous blog [Bash Scripting Basics: Your Gateway to Automation](https://varunmargam.hashnode.dev/bash-scripting-basics-your-gateway-to-automation).

Throughout this series, we'll progress from the fundamentals of Shell scripting to crafting essential advanced scripts for DevOps tasks. Get ready to unlock the full power of Shell scripting! Let's begin the exciting journey!🚀

---

# 📍If-elif

In the [Bash Scripting Basics: Your Gateway to Automation](https://varunmargam.hashnode.dev/bash-scripting-basics-your-gateway-to-automation) blog we learned how to write if-else statements in the script. Which was helpful when we had a condition.

But, what if, we have multiple conditions? For that we use If-elif, the syntax is similar to an if-else statement.

Let's see the syntax of an if-elif statement using an example: Find the greatest number from 3 numbers.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689930759506/ead7cb99-17bb-43f8-b51d-c5c489453ba6.png align="center")

📝Few things to note here:📝

1. While dealing with multiple conditions we have to use some operators like `&&` (and), `==` (checks are equal or not)`-gt` (greater than), etc.
    
2. While using operators we can use syntax `[[ expression1 <operator> expression2]]` or `[expression1] <operator> [expression2]`.
    
3. I have used arguments as my variable instead of defining a variable inside so that I can compare any 3 numbers I wish by passing them as arguments.
    

Now, we execute the script using the command `#./<filename.sh>` after changing the file permissions. *(Already covered in my* [*Bash Scripting Basics*](https://varunmargam.hashnode.dev/bash-scripting-basics-your-gateway-to-automation) *blog)*

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689931105979/d0bd1834-f000-40f0-826b-b80402db33eb.png align="center")

---

# 📍Loops🔁🔄

If you want to do a single thing multiple times in a script then we can use loops. There are two ways in which you can write loops in bash:

1. For-loops
    
2. While-loops
    

## ✔For-loops

If you want to do a single thing multiple times in a script then we can use loops. Let's see the loop statement syntax with a simple loop script:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689931517114/b9c60d36-7ffa-4d6c-958d-cb45aae836ae.png align="center")

📝 A few things to note while writing loops in bh:📝

* For loops to run it needs 3 things ( initialization; condition; iteration )
    
* In the above image, we created a variable `i` and initialized it with `0`.
    
* Then we specify a condition `i<10` telling when to stop this loop.
    
* Then we specify by how much the `i` will be incremented, here, `i++` means after every iteration of the loop `i` will be incremented by `1`. Similarly, if we do `i+2` then it will be incremented by `2`, and so on.
    

Then we will execute the script.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689931596868/60bb5f64-f461-4cbc-bd72-bd8f362ba5d3.png align="center")

As you can see the `i` variable starts from `0` and gets printed and incremented after every interaction. After printing `9` i.e. `i=9` the value of `i` get incremented to `10` which fails the condition `i<10`. Therefore, the loop ends its execution.

Let's take a more advanced example:

* Iterating files using loops: Create 10 files and then iterate all 10 files.
    

`Step 1`: Create 10 files using the command `#touch {1..10}.txt`.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689932188652/7f0c3c2a-2011-410d-8683-c9c9b45c0483.png align="center")

`Step 2`: Write a script to iterate all the text files using for loops.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689932479336/33f23d12-0a49-4339-94f7-dba86e7a6acf.png align="center")

📝Few things to note here:📝

* Here we follow another type of for-loop syntax where `FILE in *.txt` means, all files in this folder with an extension '`.txt`' print that file. (\*) means all. We save and quit.
    

Now we execute the script:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689932905567/aa3d01ff-b129-42dc-8668-79cb998c686d.png align="center")

The loop ends after iterating all the files inside the folder (where this script resides).

## ✔While Loops

It executes the same way the for-loop does which was discussed in my [Bash Scripting Basics](https://varunmargam.hashnode.dev/bash-scripting-basics-your-gateway-to-automation) blog. The syntax is different, it is something like:

```bash
while [ condition ];
do
    # statements
    # commands
done
```

If the condition is true then the commands inside the while block are executed and are iterated again after checking the condition. Also if the condition is false the statements inside the while block are skipped and the statements after the while block are executed.

Let's convert the for-loop example from the [Bash Scripting Basics](https://varunmargam.hashnode.dev/bash-scripting-basics-your-gateway-to-automation) blog into a while-loop. In the while-loop the script will be something like this:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689934930838/6dd998fb-e3ca-4a4a-a19c-41604f3c37ba.png align="center")

In the above image, we created a variable `i` initialized it as `1`, then in the while loop we put a condition `i` (less than)`-lt` `10`, and then incremented `i` by doing `((i++))`. This is the syntax to increment the variable.

Then we execute the script.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689935242751/a2a18742-c3a3-4508-bf12-19e336d65e7d.png align="center")

---

# 📍Functions

Function syntax in bash is:

```bash
#!/bin/bash
#It is a function
myFunction () {
echo Hello World from GeeksforGeeks
}

#function call
myFunction
```

The syntax is somewhat similar to making functions in other programming languages.

Let's understand functions by making a function that adds users to the system.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689936222864/14a18464-f96c-4535-8d8f-4e715f701aa8.png align="center")

But, this won't work if we simply execute the file even after giving all the permissions. Because adding a user is something only the root user can do.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689936268135/6b08b7d4-2d21-4f73-8293-121e8964e562.png align="center")

Therefore, for normal users to execute the script we have to use `#sudo`.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689936314383/ea47407b-cf15-4447-9146-abc3c615f372.png align="center")

After, executing the script we can check if the user has been added or not, we can `ls` the `/home/` directory or do see the passwd file using `#cat /etc/passwd`.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689936405282/649ee1f7-709c-4d61-abdd-5c2f595bb8c5.png align="center")

As we can see in the above image, the last line where `varun` user was added after executing the script.

---

# 📍Actual Script work for DevOps

DevOps engineers craft highly complex scripts for various tasks like user management and more. We have seen a shell script for adding a user in the previous section. Let's take another example: Creating a function taking a backup of a directory.

*We will explore a detailed backup and archiving process for files and directories in the Advanced Linux blog.*

But for now, let's take an overview of it here.

To take a backup of files or a directory, we just need to compress it and store it in a backup directory/folder.

`Step 1`

Compress the folder which you need to backup using the command:

`#tar czf <backup_filename>.tar.gz <backup_file/directoryname>`: This will compress the `<backup_file/directoryname>` file with Gunzip compression with the filename as mentioned `<backup_filename>.tar.gz` This `.tgz` extension tells it is a Gunzip file.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689937961823/ee62c8e5-43cd-40d9-b656-f2a43453b4db.png align="center")

The tar command options are `czf` which means compress, zip, and file- points to the file I'd like to compress.

`Step 2`: Create a directory to store backup files.

`#mkdir backups`: Will create a directory named backups.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689938079488/fe00416b-6c4f-4adf-82ff-3afff4ca0f54.png align="center")

`Step 3`

Then move the compressed file to the backup directory using the command `#mv`.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689938265168/3159f1c6-b0a5-4365-a8f7-8b116a15fddd.png align="center")

And your backup is done.🥳🎉

Now, we will automate this backup process by writing these commands in a bash script.

Therefore, create a `backup.sh script`, open it in the Vim editor, write the commands, and then save & quit.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689938803408/9a81cb18-eba8-4f33-9301-ccccb08473e3.png align="center")

`src_dir` means source directory.

`tgt_dir` means target directory.

Here, to directly take the backup of the scripts directory I used the command in this format:

`#tar czf <targetfilepath.tgz> <sourcefilepath>`(which needed to back up).

Then execute the bash script:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689939276701/da2341f8-cb97-4b67-bc55-e33df1abdb4d.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689939364113/af45a674-ae01-469f-8616-9b292e540f97.png align="center")

*Note: More about the* `tar` *command will be explored in detail in my upcoming Advanced Linux commands blog, stay tuned for that!😉*

---

# 📍Cron Job

### ❓Q) What is Cron❓

🔧DevOps engineers use the Cron utility to automate and schedule repetitive tasks that they perform daily. Instead of manually executing these tasks every day, the engineer sets up Cron to run them automatically at specific times and intervals. This way, the tasks run in the background, ensuring efficiency and accuracy in their execution. 👨‍💻Cron serves as a crucial daily utility for automating and scheduling these tasks, enabling DevOps engineers to focus on more critical aspects of their work.🚀

### ❓Q) What is Crontab❓

📅 Crontab is a crucial file for scheduling and executing tasks in the background. ✨ To set up a scheduled task, you create a Crontab file containing a series of commands that dictate the timing and frequency of execution. 💻 This file allows you to specify a bunch of commands that determine when your tasks will run, how often they'll run, and at what specific times ⏰, among other things. 🕒🔧 It's a handy way to keep your tasks running smoothly! 💪🚀

Cron is a service, utility, or practice, the actual work is done using Crontab. This Crontab file is located in the `/etc/` directory, you can see this crontab by using the `#cat` command.

`#cat /etc/crontab`: This will display the crontab file on the screen and it contains the definition of crontab. It tells us the format to follow while creating a crontab file.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689939749768/f839de0f-cf10-4fa2-88d3-a1d4df1a1ce2.png align="center")

📝5 things needed to be considered while writing in crontab. The given format is:

`Minute` `Hour` `Day-of-Month` `Month` `Day-of-week` `#command`

Let's understand with a cronjob example how to write a cronjob in a crontab following the above format:

`*` `*` `1,5` `*` `sun` `echo "Hello"`: Here, (\*) means all (every day, every week, and so on). There is only a single space after every word.

So, the above cronjob means it will print "Hello" at:

`every minute` `every hour` `on the 1st and 5th day` `of every month` `Sunday`.

💡There are 3 commands related to crontab which you always have to remember.📝

* `#crontab -l`: Displays a list of currently active crontabs for this user.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689939823766/2e2edb02-6929-4e15-b207-0f4862a72955.png align="center")

* `#crontab -e`: This `-e` means to edit, this command will create and open a crontab in an editor to let you write your cronjobs.
    
    *Note: While creating your first crontab it will ask you which editor to use. It is up to you to use Vim, vi, or Nano in whichever editor you are most comfortable with.*
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689940001711/351bbe7f-6be5-4502-881e-56638c7589e5.png align="center")

After that, your crontab will be opened and it will look something like this:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689939918986/a3fe327b-297d-4c19-b7df-26ab9bfd69ba.png align="center")

* `#cat /etc/crontab`: This will display the crontab file on the screen and it contains the definition of crontab. It tells us the format to follow while creating a crontab file. Same as we have seen previously.
    

Now, you can write your first cron job.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689940512986/5d7f7f74-eafe-4d5e-934f-e1c15348d102.png align="center")

In the above image, I am redirecting the output of the command to a file by specifying the absolute(complete) path of that file. If the file doesn't exist, the cron job will automatically create a new file and redirect the output into it. 🔄📂🔗

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689940593250/09179644-72d6-4c7f-bd0b-91c2c3923987.png align="center")

As you can see the crontab was empty therefore, it was creating a new crontab, we can also see the time is 11:51 (hrs: minutes) and our cronjob will be executed at 11:54 since we scheduled it for that time.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689940743543/d2802857-8d8c-4289-97ec-1bffdf29f2db.png align="center")

Congratulations!!🥳 🎉You just created your first cron job.

*"Stay tuned for a more advanced cronjob, with the utilization of advanced Linux commands which will soon be uploaded in this blog section. 🚀I will cover these commands in detail in my upcoming blogs, and they will be uploaded shortly.📝 Don't worry; you won't want to miss it!"😉*

---

# 📍Conclusion

Thank you for reading this blog! 📖 We've reached the end of the Bash Scripting series, but there's much more to come as I gain more experience and learn more in my DevOps journey. 🤩Stay tuned for exciting advanced Linux commands in my next blog. 🚀 Meanwhile, keep practicing and unleashing your creativity with these scripts. 💻🔧 More valuable content is on its way!

If you enjoyed this blog and found it helpful, please give it a like 👍, share it with your friends, do share your thoughts, and give me some valuable feedback.😇 Don't forget to follow me for more such blogs! 🌟

---

# 📍References

This blog's Topics and scripts are referred from the following 2 videos:

* [Advanced Shell Scripting Tutorial from the TrainWithShubham channel (Part 1)](https://www.youtube.com/watch?v=UYstAfqkLtg)
    
* [Cron job vs Cron tab Tutorial from the TrainWithSuhbham channel](https://www.youtube.com/watch?v=aolKiws4Joc&t=180s)
    
* [Stackoverflow](https://stackoverflow.com/questions/2359270/using-if-elif-fi-in-shell-scripts)
    
* [Functions in bash scripting](https://www.geeksforgeeks.org/bash-scripting-functions/)
    
* [GFG-While Loops](https://www.geeksforgeeks.org/bash-scripting-while-loop/)