---
title: "Mastering Basic Linux Commands for DevOps Excellence (Part 2)"
datePublished: Wed Jul 19 2023 09:46:33 GMT+0000 (Coordinated Universal Time)
cuid: clk9jgz82000p09ksc5dthz08
slug: mastering-basic-linux-commands-for-devops-excellence-part-2
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1689731016031/a1c5200a-28f8-4f02-8a6c-efb0907d79bd.png
tags: linux-for-beginners, devops-journey, 90daysofdevops, day3, trainwithshubham

---

---

# 📍Introduction

📚 In this 2-part blog series, we'll continue to explore basic Linux commands! Whether you're a beginner or want to refresh your Linux fundamentals, this guide has got you covered. By the end, you'll have a solid foundation in Linux commands 💪. Get ready to unlock the potential of Linux commands and join me on this exciting Linux journey! 🚀

📚**Let's continue to see the commands to perform operations on the directory and file.**

---

# 📍Perform operations on a file & directories

1. `#cat`: To read the file by displaying the file on the screen.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689749300588/1427dbbe-fbfa-48fd-bd78-2744a20e37b6.png align="center")
    
2. `#head <filename/filepath>`: To read the top 10 lines of the file by displaying it on the screen.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689749394888/2af07ea2-8caa-4416-8778-6d69dd9309e4.png align="center")
    
    (*You can also specify the number of lines you want to see from the top.*)
    
    `#head -n <filename>`: To read the top `n` lines of the file by displaying it on the screen.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689749557206/192b0c3a-2649-4624-b92e-db9e9ba39ab4.png align="center")
    
3. `#tail <filename>`: To read the last 10 lines of the file by displaying it on the screen.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689749414018/83d94946-f66c-428f-b887-365ce1e4ad38.png align="center")
    
    `#tail -n <filename>`: To read the last n lines of the file by displaying it on the screen.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689749571495/4afa7eef-4ec2-4edc-b662-b9b77f633f17.png align="center")
    

To edit files, many editors are available in Linux eg: gedit, vi, nano, vim, etc are some popular editors. We will be learning Vim editor.

---

📚**Let's dive into how to edit files using the Vim editor.**

# 📍Editing files with Vim

To open the file in the Vim editor use the command:

* `#vim <filename>`
    

The file will be opened in the **Vim editor** and will look something like this:

Here, the file 'devops.txt' is opened in the Vim editor.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689750846063/283ac2ef-aa84-4d56-9a36-f8d50ecf1e4f.png align="center")

If you cannot see this and get a prompt saying "**vim command does not exist**" or something like this. It means you do not have Vim editor on your Linux machine then install it by using the '`#apt-get`**'** command:

* `#sudo apt-get install vim` *(sudo for root privileges, more about this in the later section of this blog)*.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689750682997/fef0700e-2b30-4223-a6c7-9d08f4f55af0.png align="center")

Now you can open the file in the Vim editor.

## 📑Vim editor has 3 modes:🖊

1. Command Mode.
    
2. Insert Mode.
    
3. Extended command mode.
    

***Note: When the file opens in the Vim editor, it will by default be in the command mode. It looks something like this:***

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689751177019/36889b80-e053-4203-bccc-82dd3afb428b.png align="center")

### ✔Command Mode:

It has some basic commands (can be called shortcuts) which you have to click to navigate and operate throughout the text files like:

1. `gg`: To go to the beginning of the page.
    
2. `G`: To go to the end of the page.
    
3. `yy`: To copy a line.
    
    `nyy`: To copy n lines.
    
4. `P`: To paste the line below the cursor position.
    
    `p`: To paste the line above the cursor position.
    
5. `dd`: Deletes or cuts a line.
    
    `ndd`: Deletes or cuts the n lines.
    
6. `u`: To undo the last change (check for word or line).
    
7. `/word`: To search for a word in the file.
    

### ✔Insert Mode:

You can enter Insert mode in the Vim editor by pressing the '`i`' key in the command mode and pressing '`Esc`' to exit from Insert mode which will take you to the default mode i.e. command mode.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689751329183/f294730f-dc92-4829-b495-5ab3c2b24b5f.png align="center")

Insert mode is indicated at the bottom left corner as "-- INSERT --".

After entering command mode you can do whatever changes in the file content.

### ✔Extended Mode:

You can enter an extended mode in the Vim editor by typing the (:) key in the command mode.

Some commands in extended Mode are:

1. `:w` - To save changes made to the file.
    
2. `:q` or `x`\- To quit (without saving).
    
3. `:wq` - To save and quit.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689751523275/00691a77-8e43-44d8-8ae5-a83cffe20f54.png align="center")
    
4. `:wq!` - To save and quit forcefully.
    
5. `:se nu` (set numbers) - To set the line numbers to the file.
    
    `:se nonu` (set numbers) - To remove the set line numbers from the file.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689751612590/55f3f87a-79e6-48e9-9dd4-039187172ed6.png align="center")
    
6. `:n` - To go to the nth line number.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689751654523/8e40d872-4fda-406d-acfc-c74ea938a4d6.png align="center")
    
    The cursor points to line number 5.
    

---

### 📚Exercises on Vim editor:📚

1. Add content in devops.txt (One in each line) - Apple, Mango, Banana, Cherry, Kiwi, Orange, Guava.
    
2. To create another file Colors.txt and add content in Colors.txt (One in each line) - Red, Pink, White, Black, Blue, Orange, Purple, Grey.
    

---

# 📍User Management and Access Permissions

🔎In this section, we will explore the fundamentals of User management and User access permission files in Linux.🔎

In Linux, for every file and every process, there is an owner i.e. a user with a uid- user-id. There can be multiple users with various names every user has its directory and a file structure that only the corresponding user can access.

### ✔In Linux, there are 3 types of users:

1. **Super user or root user:**
    
    The system/root user is the most powerful user with all the administrative privileges given to it. The root user is the administrative user.
    
2. **System user**:
    
    System users are the user created by the software or applications.
    
    For eg: If we install Jenkins it will create a Jenkins user. Similarly, if we install any other service application it will create a user.
    
3. **Normal user**:
    
    Normal users are the users created by the root user. They are normal users like Lokesh, Aryan, etc. Only the root user has permission to create or remove a user.
    

To understand this concept easily, we can compare it to the Windows example. 🖥️ In Windows, there is an admin user and various user accounts for family members. Similarly, in Linux, the root user holds administrative privileges, similar to the Windows admin user, while normal Linux users are equivalent to non-admin users in Windows. 🐧

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689751856327/0e8fa2b2-6a3b-4db8-81a5-607da5e0e649.png align="center")

As shown, in the above image inside the home directory there is a directory name ubuntu for the user whose username is ubuntu. You can add as many users as you wish with the command:

* `#sudo adduser <username>`: Creates a user with the username as mentioned and creates a directory for the user in the home directory.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689752313082/e29a3598-0892-47b5-b190-f19ac70b3490.png align="center")
    
    You can skip the Full Name, Room Number, and other fields by just pressing the 'Enter' key but, it is necessary to give a password so that the user can be logged in using this password. *(Make sure to remember whatever password you set)*
    
* `#userdel`**:** To delete a user.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689752559515/43717967-f2a3-4068-82dd-dd3c3affa93b.png align="center")
    

Therefore, **to check the number of users** we can check the number of directories inside the **home directory** it can also be viewed in the '`/etc/passwd`' file where Users name along with UID and some additional information is displayed:

* `#cat /etc/passwd`: The 1st field/column shows all the users currently present in the system.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689753027386/3267e2e2-ec19-42a2-90a0-9996aafbcede.jpeg align="center")
    

*(In Advance Linux Blog, we will cover in detail what the rest of the fields represent.)*

*Note: Users name and UID (unique user id) are stored in the '*`/etc/passwd*`' *directory.*

### ✔Sudo Privilege

We know that only the root user can add or remove a user but a normal user can also perform this task by using the '`#sudo`' command:

* `#sudo`: It gives any normal user all the privileges of the root user temporarily.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689753180286/fc35b466-6849-4213-bb9b-271f33a2bb00.png align="center")

As you can see in the above image when '`#adduser <username>`' command is executed by the normal user it shows permission denied whereas when we use "`#sudo`" with the command '`#sudo adduser <username>`' it is successfully executed.

### ✔Switch User

Only the root user has the privilege to switch to any user without requiring a password and can also set passwords for specific users.

To enable user switching for normal users, it is necessary to set individual passwords for each user. These passwords are used to log in to their respective user accounts. If a normal user intends to set or change the password for another user, the command '`#sudo`' can be utilized.

As can be seen in the above image for '`#adduser`'.

1. **The command used to set the password:**
    
    * `#passwd <username>`: Sets a password for the file &lt;filename&gt;.
        
    * `#sudo passwd <username>` (For normal users).
        
2. **The command used to switch users:**
    
    * `#su <username>`: Switch to &lt;username&gt; user. (For root user)
        
    * `#sudo su <username>` (For normal users).
        
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689754063295/2912a11a-e358-468d-b606-5d9d085a63f7.png align="center")
    
    While switching from a normal user to a root user it requires a password but, for security reasons, we will not know the root user's password. To switch to the root user without it asking for the password I used '**#sudo**' to grant **root user privileges**.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689754288473/8ad1f566-6dec-4bff-a969-2696a243559d.png align="center")

As you can see in the above image, after switching to the root user it does not require any password to switch to a different user.

1. The command used to exit from the user:
    
    * `#exit`: Exits from the current user and goes to the original user from where users were switched.
        

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689753718444/9dc96967-8e46-4e9f-981b-6f5c817f2439.png align="center")

As we can see, when I switch from the 'varun' user to the 'aryan' user and exit, I return to the 'varun' user.

*(We will be learning about the sudo command in more detail in Advance Linux Blog.)*

## 📍User Access Permissions

Access Permissions for a file or a directory are of three types:

1. Read (r)
    
2. Write (w)
    
3. Execute (x) (perform operations like '#cd')
    
4. No permission (-)
    

To check the access permissions of a file use command:

* `#ls -l`: Displays all the files present in the current working directory with access permissions and some additional information.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689757541757/1079b317-d6eb-48ba-aafd-13a4a3debf9d.png align="center")

As shown in the above image the 1st (-) field is to tell file type, the 'devsecops' file type is a directory hence 'd' is mentioned.

The next 3 (-) fields are the 'rwx' i.e. read, write, and execute permission respectively for the user.

In the above image, for the 'devops.txt' file the user permission field is rw-, which means the user has read and write permission and does not have execute permission. We can add the execute permission for the user, shown in the next section.

### ✔Change Ownership:

#chmod: To change user permissions we use the command.

1. Add (+) permissions (r,w,x) to the user (u):
    
    * `#chmod u+r <filename>`: To provide read permission to the user.
        
    * `#chmod u+w <filename>`: To provide write permission to the user.
        
    * `#chmod u+x <filename>`: To provide execute permission to the user.
        
2. Remove (-) permissions (r,w,x) from the user (u):
    
    * `#chmod u-r <filename>`: To take read permission from the user.
        
    * `#chmod u-w <filename>`: To take write permission from the user.
        
    * `#chmod u-x <filename>`: To take execute permission from the user.
        

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689758142898/0710fa8b-e445-4ecd-84a2-611b0dc5d1b4.png align="center")

As we can see in the above image after adding execute permission using the '`chmod`' command the user permission fields show "rwx".

*(More about the file access permissions in the Advance Linux blog.)*

---

### ✔The last command to display all the commands the current user has executed is:

* `#history`: Displays all the commands executed by the currently logged-in user.
    

---

# 📍Conclusion

🎉 The 2-part blog series on Basic Linux commands have concluded, equipping you with nearly all the essential commands of Linux. By practicing these commands, you'll establish a solid foundation in Linux fundamentals.

💭 Share your thoughts in the comment section; I'm eager to hear your feedback. Don't forget to like & share the blog with your friends and peers if you found it helpful.😇

🙏 Thank you for reading my blog! Keep practicing, keep learning, and delve into these commands to embark on your Linux journey toward advanced concepts with confidence. Stay tuned for more exciting blogs!🔥

---

# 📍References

* [ChatGPT](https://openai.com/chatgpt)
    
* [Google](http://google.com)
    

---