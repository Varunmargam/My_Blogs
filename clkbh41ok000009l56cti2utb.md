---
title: "Learning Bash Scripting Basics: Gateway to Automation"
datePublished: Thu Jul 20 2023 18:16:02 GMT+0000 (Coordinated Universal Time)
cuid: clkbh41ok000009l56cti2utb
slug: learning-bash-scripting-basics-gateway-to-automation
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1689942838335/cd8979a7-4488-4255-9f6c-fa656556ed8c.png
tags: 90daysofdevops, day4, linux-for-devops, trainwithshubham, shellscripting-devops

---

---

# 📍Introduction

👋Hello guys! Welcome aboard on an exciting journey into the world of Shell scripting! 🔥This blog is the perfect starting point for anyone interested in learning basic shell scripting as part of my comprehensive Shell scripting for DevOps series.

*(Note: )* Before diving in, make sure you are **familiar** with **basic Linux commands**; if you need a refresher, don't miss my two-part blog series on ["Mastering Basic Linux Commands."](https://varunmargam.hashnode.dev/mastering-basic-linux-commands-for-devops-excellence-part-1)

Throughout this blog series, we will progress from the fundamentals of Shell scripting to crafting some advanced scripts that are essential for DevOps tasks. So, let's get ready to unlock the power of Shell scripting and take your skills to the next level!💪🚀

---

# 📍Bash & Shell

The script is a single file that contains a series of commands, we do this to execute a series of commands using a single command.

### ❓Q)What is a terminal❓

The terminal (aka command line interface) is a GUI (graphical user interface) application window that allows the user to connect to or access the shell. It is a special program called Terminal in Linux & MacOS or Command Prompt in Windows.

### ❓Q)What is a shell❓

A window in Linux where you write all your Linux commands is a shell. After connecting to the shell from the terminal, we enter the shell where we perform various tasks by entering Linux commands on the shell.

Shell takes human-readable commands as input, processes them, interprets them for the kernel, and gives it to the kernel to execute the corresponding code as per the command and then the shell takes the processed output and displays it on the screen.

Therefore, a **shell** is also called a **command line interpreter**. It acts as an **interface** **between** the **user** and the **kernel**. Linux shell looks like this:

(Photo)

*(An interface is nothing but a medium. For eg: While booking a ticket you speak into the mic to communicate with the person on the other side. Here mic is acting as an interface between you and the person inside the ticket counter.)*

**Shell** stands for Bourne **sh**ell.

### ❓Q)What is bash❓

**Bash** stands for **B**ourne **a**gain **sh**ell. As the name, it stands for, bash is a better version of the shell. Therefore, many Linux distros use bash as their default shell.

You can check which shell your Linux is using with the command:

`#echo $0`: It tells us which shell is being used by your Linux machine.

***(Note: $0 can be the name of the shell or the name of the shell script. When it is used inside a shell script, it denotes the name of the script.)***

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689869370652/79330f56-5f55-4bb5-a27d-063e1edcad0f.png align="center")

As you can see, my Linux instance has a bash shell.

### ❓Q)What is the difference between a bash script and a shell script❓

A script written in a bash programming language is a bash script. This 'bash script' can only be executed by the 'bash shell'. Whereas the 'shell script' is a more generic term for a script that can be executed by 'any shell.' Bash scripting is a subset of shell scripting.

Bash is more programmer-friendly as compared to Shell. Therefore, bash is widely used for scripting.

### ❓Q)What is Shell Scripting for DevOps❓

* As DevOps engineers, we often find ourselves repeatedly executing the same set of commands in our daily tasks. To streamline and automate this process, we create scripts that store these commands in a file. This way, instead of running each command individually, we can simply execute the script to perform all the tasks at once.
    
* Therefore, a script is essentially a file containing a series of commands that are executed in sequence, making our workflow more efficient and time-saving.
    

---

# 📍First Script

Let's make our first script.

`Step 1:`

Create a file with an extension of '`.sh`' This indicates that the file is a **shell script**. Just like a **Python** file has an extension of '`.py`'.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689872858817/ad90f639-40ac-42f3-8746-24c70bbc3e1f.png align="center")

`Step 2:`

Now, open the file in the Vim editor and go into the 'Insert mode'. The first line of any script is with the "**shebang**" character i.e. "**#!**" along with the shell i.e. which shell your Linux is using. This tells what type of script are we writing in this case we are writing a bash script. We can see the type of shell Linux is using with `#which shell` command.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689873101404/68218e15-858f-40ea-8cfb-3de95b5edfd0.png align="center")

Since my Linux uses the bash shell, therefore, I wrote `#!/bin/bash`.

`Step 3:`

Write any simple command. For eg: echo "This is my first bash script." then save and quit the file.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689873429183/36fd8cd2-9ecc-45c9-9533-de3e13ac74cd.png align="center")

`Step 4:`

Execute this script file with the command `#bash <filename>`:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689873532470/13bd99c9-4b15-491e-8904-939b973a2da1.png align="center")

Congratulations!!🥳 You just executed your first bash script!!🔥

---

### ❓Q) Can we write `#!/bin/sh` instead of `#!/bin/bash` as the first line of your script❓

🧠💭 Brainstorm about this before checking the answer. 💡🤔

<details data-node-type="hn-details-summary"><summary>Ans</summary><div data-type="detailsContent">When we write '<code>#!/bin/sh</code>' instead of '<code>#!/bin/bash</code>' we are indicating that our file is a shell script rather than a bash script specifically. It's essential to understand that a bash script is just one form, a subset, of a shell script. The '<code>#!/bin/sh</code>' declaration doesn't directly invoke the shell; rather, it designates the file as a shell script. However, when you run the script, the shell installed in your Linux system will be utilized. Fortunately, Linux commonly has a bash shell, so if the script is written in a bash programming language, it will be executed successfully. On the other hand, if the script is not in a bash programming language, it might not execute as intended.</div></details>

---

The script file can also be executed using the command `./<filename>`, but, the permission is denied for that we can change the permissions. This `./<filename>` command makes the script executable.

---

# 📍Permissions

Now, when we try to execute the script file using the command `./<filename>` it says permission denied.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689873703123/a467226a-f623-4c9a-9e69-182ed1a92ed0.png align="center")

Let's see what permissions are given to us for the file. For that, we have a command `#ls -l`.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689873766820/13c15d4a-5d5c-45bc-94fb-fe73f7773d7a.png align="center")

Before moving forward make sure to check out my ["Mastering Basic Linux Commands."](https://varunmargam.hashnode.dev/mastering-basic-linux-commands-for-devops-excellence-part-1) blog's "User Access permissions" section if you are unaware of this concept.

After the 4 fields(-) the next 3 fields are the permissions for the group and the next 3 fields are the permissions for others.

As we can see in the image:

* The user/owner has read (r) and write (w) permission.
    
* Group has read (r) and write (w) permission.
    
* Others have only read permission.
    

There are 2 ways to give permissions in Linux:

* Numeric.
    
* Non-numeric *(Already discussed in my basic Linux blog (Part 2)).*
    

## ✔Changing permissions using a numeric way.

We will be giving the script file permission using the numeric method for that we will use the command:

`#chmod 777 <filename>`: To give the user/owner, group, and others all (read, write, and execute) permission.

Permissions are calculated by adding:

* 4 ( to read)
    
* 2 ( to write)
    
* 1 ( to execute)
    

Therefore:

* 3 means - write and execute permission (2 + 1).
    
* 5 means - read and execute permission (4 + 1).
    
* 6 means - read and write permission (4 + 2).
    
* 7 means - read, write, and execute permission (4 + 2 + 1).
    

In the command `#chmod 777 <filename>`:

* 1st digit specifies the owner's permissions.
    
* 1st digit specifies group permissions.
    
* 1st digit specifies others' permissions.
    

Now when you do `#ls -l` It will show all the permissions given:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689873893466/56afdab1-1979-4a52-a116-ebcb2872ea17.png align="center")

Now we can execute the script file using the command `./<filename>`.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689873938091/5f350d54-d9af-4b16-b7f2-5cf15ae2e136.png align="center")

---

# 📍Variables & Comments

## ✔Variables

In bash creating a variable is very easy we just have to write:

`variable_name="variable_value"`: A variable `variable_name` has been created with a value `variable_value`.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689874258259/296b7e7a-c9e5-4d05-bb19-70784b0385d6.png align="center")

To print ("echo") this variable we use '$' `echo $variable_name`.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689874323520/1f94e6b2-c99b-457f-b463-a8e9e97cd1a0.png align="center")

But, what if I want to print the variable with some other text?

For this, we need something to differentiate the variable from the printable text. Therefore we use a placeholder '`{}`' Now we can print variables with some other text like this:

`echo "hello ${variable_name}"`: This will print - hello `variable_value`.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689874485245/2f5218e4-320b-4d59-bf88-189e295be6b9.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689874537988/409c2260-15c8-442a-b6b7-1cb7eaeb0285.png align="center")

### ❓Q) Why do we need variables❓

In scripting, when a file/directory path or a lengthy value appears repeatedly, it becomes cumbersome to rewrite it multiple times. 😩 However, we have an elegant solution - using variables. 🎉 Variables allow us to store these values with short and meaningful names, making the script more concise and manageable.

Moreover, when debugging, variables prove invaluable. If there's an issue with the file/directory path or the variable value, we can simply modify the variable, and all instances of its usage will be automatically updated.🛠️

Incorporating variables in our scripts significantly enhances convenience and streamlines the debugging process, making scripting a breeze.😎

## ✔Comments

Comments can be used to tell the user or the reader some additional information about the command or the task the commands will be performing. In bash, comments can be written using '#'.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689874631345/fbda3811-e58e-4ce6-bbe1-57a638359cdc.png align="center")

These comments will not be read and executed while the script is implemented.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689874691792/74c9a04b-4bb1-41bb-9cfb-68b3dfc2105d.png align="center")

---

# 📍User Input & Arguments

## ✔User Input

To take user input in the bash script we use the `read` command:

Syntax: `read <variable_name>`

Then we can print the variable\_value the user has input.

`echo "Your input was ${<variable_name>}"`

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689874899899/fbbced11-b412-4411-b0d3-8022df0e83e4.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689874951105/c4ba7947-a55b-4153-b375-ffade699367d.png align="center")

## ✔Arguments

### ❓Q) What is an argument and why do we need it❓

When we write an executable script `./<filename>` command if we add a space then we can enter out arguments. For eg: `./<filename> argument1 argument2...and so on`. These arguments act as `variable_value` of the variable inside the script.

Suppose, I don't want to define variable\_value in the script, for that we have user input. But, I also don't want the script to be interactive, I want to define it with the executable file command. In such cases, arguments can be used.

### ❓Q)How to use these arguments inside the script❓

Inside the script `$1` is the variable that will contain the value `argument1` similarly, `$2` will contain the value `argument2`, and so on.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689875336547/dacd34bd-ab90-4c3f-879e-0393f64ef5da.png align="center")

For $1 there is no need to specify a placeholder `{}` in the echo command.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689875401106/bc91e4b1-af32-4e2b-9824-2f4a547ce141.png align="center")

---

# 📍If Else

### Syntax:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689875933176/4473da0e-a873-4e61-8aeb-71a61e221005.png align="center")

In the above image, all the spaces are one single space.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689876043028/5b712f1f-3988-4041-945a-164588667fe4.png align="center")

---

# 📍Conversation

Just a fun command:

`sleep n`: While the script is being executed, the execution will pause for `n` seconds and then resume its execution.

So, using this command we can create a script in which a conversation can be printed one-by-one

---

# 📍Conclusion

Thank you for reading this blog! 📖 We've reached the end of the Basic Bash Scripting. In my next blog, get ready to delve into some exciting advanced bash scripting concepts. 🚀 Until then, keep practicing these scripts, unleash your creativity, and try to craft more scripts. 💻🔧 Stay tuned for more valuable content coming your way!

If you enjoyed this blog and found it helpful, please give it a like 👍, share it with your friends, do share your thoughts, and give me some valuable feedback.😇 Don't forget to follow me for more such blogs! 🌟

---

# 📍Reference

* [Shell Scripting Tutorial by Shubham Londhe sir.](https://www.youtube.com/watch?v=_-D6gkRj7xc&list=TLPQMTkwNzIwMjPMT8_PfTURFA&index=3)
    
* [Article on Bash and Shell scripting.](https://askubuntu.com/questions/172481/is-bash-scripting-the-same-as-shell-scripting)
    
* [ChatGPT](https://openai.com/chatgpt)
    
* [GFG](https://www.geeksforgeeks.org/)
    
* [Stackoverflow](https://stackoverflow.com/)
    

---