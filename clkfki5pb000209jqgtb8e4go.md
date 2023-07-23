---
title: "Mastering Advance Linux Commands for DevOps Excellence (Part 2)"
datePublished: Sun Jul 23 2023 15:02:04 GMT+0000 (Coordinated Universal Time)
cuid: clkfki5pb000209jqgtb8e4go
slug: mastering-advance-linux-commands-for-devops-excellence-part-2
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1690124423675/7f3aff6b-ddb3-498e-9a0b-405b8a76c677.png
tags: devops-journey, 90daysofdevops, day7, trainwithshubham, linuxsystemadministration

---

---

# 📍Introduction

📚 In this 2-part blog series, we'll explore some more Advance Linux commands! After learning and mastering basic Linux commands and getting introduced to advance Linux in the previous blog we are now ready to learn some advance Linux commands. By the end, you'll be familiar with piping, redirection, sudoers file, some administrative commands, etc 💪. Get ready to unlock the potential of Linux commands and join me on this exciting Linux journey! 🚀

---

# 📍Piping

Piping is used to run multiple commands at a time. Using the operand `|`, it is the key located above the Enter key on your keyboard. `|` is called a pipe.

Syntax: `command1 | command2`

In the above syntax, the `command1`'s output will act as an input to the command on the right-hand side i.e. `command2`.

Example:

`#ls -l | grep script`:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690119619659/750f4670-437a-481e-9b43-49283f9f8870.png align="center")

The list of files inside the current directory from `ls -l` has gone as input to the command `grep script`. For this, we can use a pipe `|` to concatenate two or more commands.

---

# 📍Redirection

## Input/Output redirection:

There are many times when you don't want to see the output of any process running or after executing a command. Since DevOps engineers like to automate tasks and run the process in the background with as minimal manual interactions as possible this redirection process can help you to achieve that.

These redirections will be very helpful while writing Shell scripts.

### ✔Redirection symbols:

1. `>`: It is used to redirect the output of a command.
    
    `#command > file path`: The `command`'s output will be redirected to the file to which the `file path` is provided.
    
    Example:
    
    `#echo "I am studying redirection" > /tmp/test.txt`: If test.txt is not present it will create the file and if the file already exists it will overwrite the content of the file with the command's output.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690120018512/1150cd1d-dc51-4ed5-a047-0a8f77d4d7de.png align="center")
    
    `/tmp` directory is where we can store files or directories temporarily.
    
    `#apt-get install tree > /temp/tree_install.txt`:
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690120414558/978fe012-7cb6-4f70-a3ba-bfe281f9abf6.png align="center")
    
    But, if the other output is redirected to the same file then it will overwrite its content. Like this:
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690120698019/ed3e0035-36ca-40f5-a8d2-8bfc29041949.png align="center")
    
2. `>> or 1>>`: It is also used to redirect the output of a command but instead of overwriting the content of the file provided, it will append the command's output to the existing content of the file.
    
    Example:
    
    `#echo "This sentence is appended to the existing content" >> /tmp/test.txt`:
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690120806216/3ddcd3de-07e9-48b3-bbb3-9099e2bf79dc.png align="center")
    
    But if any error occurred while executing the command it will show it on the screen to redirect such an error we use `2>>`.
    
3. `2>>`: It is used to redirect errors while executing the command to a file.
    
    Example:
    
    `#echooo 2>> /tmp/error.log`:
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690120908337/94503531-8dcc-4853-bcf7-1b5cff9835ac.png align="center")
    
    Therefore, &gt;&gt; or 1&gt;&gt; is used to redirect the standard output of a command, and 2&gt;&gt; is used to redirect errors while executing a command.
    
4. `&>>`: It will redirect any kind of output to the standard output as well as errors.
    
    Example:
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690121089595/f980658a-d81d-4921-a475-c0e88c7c37a7.png align="center")
    
    Try trying to redirect the error using `>> or 1>>` and to redirect standard output using `2>>` It will not be redirected.
    

The open part of the redirection symbol is for input and the tapering/pointed part is for the output.

---

# 📍Sudo

As we know, only the root user has all the privileges to perform any kind of operation or administration. If a normal user wants to execute commands which only the root user is allowed to execute then the normal user will have to use `sudo` to temporarily grant root user privileges or switch to the root user.

It is harmful if normal users can execute root user commands. Therefore, not all users are given the privilege to use this sudo command and switch to the root user. To give normal users the privilege to use the `sudo` command, and switch to the root user, we have to add the users in the `sudoers` file.

Let's take an example:

I have 3 users `ubuntu`, `aryan`, and `lokesh` as you can see in the image below and I have also set the password for each one of them.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690121442388/d7f1d15a-b775-4710-bcaa-722b83f8db7a.png align="center")

Now, I can switch to the `root` user from `ubuntu` user and I can also execute `root` user commands using `sudo`.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690121610227/4250ee88-b735-458b-b931-f1f93ed9d22f.png align="center")

But, when I switch to `aryan` user, I am not able to execute the `sudo` command nor I can switch to the root user. It throws me an error called `aryan is not the sudoers file`:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690121781157/e980d418-14b6-4045-bc91-e8effc9508f6.png align="center")

This `sudoers` file is located inside the `etc` directory `/etc/sudoers`:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690121867858/bc3c0309-9664-4019-b935-3e61bccc23ec.png align="center")

It is a read-only file for the root user, and for the root group, no permission is given to others. Therefore, to edit this file we use the command `#visudo` from root user.

Traditionally, `visudo` opens the `/etc/sudoers` file with the `vi` text editor. Ubuntu, however, has configured `visudo` to use the `nano` text editor instead.

If you would like to change it back to `vi`, issue the following command:

`#sudo update-alternatives --config editor` and then select option 3 for vim editor.

`#visudo`: This command will open the sudoers file in write mode.

Then do, `:se nu` to set line numbers and go to line number 44th. Copy this line and write the user you want to give the privileges to.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690122484604/ba0f5ef0-0810-4b71-a4a2-b0efa51c4fa1.png align="center")

`NOPASSWD`: This is to ask for no password while switching to the root user and executing the sudo command.

If while editing this sudoers file there is any syntax error then it will give the prompt to edit it again for that type `e (to edit)` :

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690122608407/4544f7cf-c46f-4c4c-8d28-c58818529de2.png align="center")

Important: Be careful while editing the sudoers file if you save the file with the syntax error then you will not be able to execute the sudo command and you will also not have the root password (for security reasons) and you will be stuck.

Now the `aryan` user can execute sudo commands and switch to the root user.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690123190855/c9ea262e-8caf-4429-8b1f-deab4e63bdc5.png align="center")

---

# 📍Software Management/package manager

The most popularly used Linux distros in the IT industry are:

These distros are different based on how they are packaged.

* RPM (Red Hat Package Manager) based: Centos, Oracle Linux, RHEL (Red Hat Enterprise Linux)
    
* Debian-based: Ubuntu, Kali Linux
    

We will be looking into software management in Ubuntu:

## ✔APT- Advanced Packaging Tool

In Ubuntu, `apt` command is used to download any software or upgrade existing software, or update the package list index or service. This apt command makes software installation easy by downloading the necessary dependencies if they are not present in the system for the software.

Only the root user and user who can execute the `sudo` command can install or remove the packages. Let's see some apt commands:

1. `#sudo apt install package_name -y`: To install a package -y is to not ask any questions during the installation.
    
2. `#sudo apt remove package_name`: To remove the package installed.
    
    * `--purge`: This `--purge` option to `apt remove` will remove the package configuration files as well.
        
3. `#sudo apt update`: To update the local package index with the latest changes made in the repositories.
    
    The package index is essentially a database of available packages from the repositories defined in the `/etc/apt/sources.list` file and in the `/etc/apt/sources.list.d` directory.
    
4. `#sudo apt upgrade`: To upgrade installed packages from the package repository which was updated using `#sudo apt update`. This is done so that the packages in our system are up-to-date. You should always do `#sudo apt update` and then `#sudo apt upgrade`.
    

---

# 📍Systemctl - Services

There are many services that we will use as DevOps engineers, to administer that services is very important and every DevOps engineer should know.

`#systemctl`: This command helps us to manage or control or administer a service.

Syntax: `#systemctl subcommand service`

`#systemctl` is a utility that can be used to know about the services using `subcommand`.

List of subcommands:

1. `#systemctl status service`: Used to check the status of the service- active or inactive.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690123395079/2a871036-15c6-43d1-b459-e169253eb914.png align="center")
    
    As you can see, after the output is displayed it does not go to the command line so to exit from this output press the `q` key.
    
    `sshd` is a service for ssh login, we can connect to the shell using ssh because this `sshd` service is active, if it was inactive we could not have been able to connect to the shell.
    
2. `#systemctl start service`: To start the service. Give sudo for normal users.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690123724784/cd9f3ea3-109f-45be-9fab-e49b6613e1fb.png align="center")
    
3. `#systemctl stop service`: To stop the service gracefully i.e. it will stop the process as well as its child processes.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690123865402/26fc709b-55b6-476a-ac0b-72d0e30f8d5c.png align="center")
    
    Sometimes, services refuse to stop gracefully for that use:
    
4. `#systemctl kill service`: It will stop/kill the service but it will not stop the child processes running.
    
5. `#systemctl enable service`: To enable the service. It means when the system will be restarted or rebooted then this service will automatically start and run if the service is enabled.
    
6. `#systemctl disable service`: To disable the service.
    

But there are many subcommands to remember them is very difficult, for that use the trick `#systemctl` + `Tab` key 2 times. Type `#systemctl` with 'single' space and press the `Tab` key 2 times.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690124265880/36aae6d6-0bdc-438d-9612-9d58736d63dc.png align="center")

---

# 📍Conclusion

Thank you for reading this blog! 📖 We've reached the end of this Advance Linux Commands blog. You are now familiar with some Linux system administration commands as well. Keep practicing these commands, and get familiar with them. 💻 Master Linux system administration and keep learning. Stay tuned for more valuable content coming your way!

If you enjoyed this blog and found it helpful, please give it a like 👍, share it with your friends, do share your thoughts, and give me some valuable feedback.😇 Don't forget to follow me for more such blogs! 🌟

---

# 📍Reference

* [Udemy DevOps course by Imran Teli](https://www.udemy.com/course/decodingdevops/)
    
* [Ubuntu Software Management](https://ubuntu.com/server/docs/package-management)
    
* [RedHat systemctl command](https://www.redhat.com/sysadmin/getting-started-systemctl)
    

---