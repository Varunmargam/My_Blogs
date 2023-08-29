---
title: "Exploring Advanced Linux Commands (Part 1)"
datePublished: Sat Jul 22 2023 18:16:18 GMT+0000 (Coordinated Universal Time)
cuid: clkec035o00050al57cmkgdq9
slug: exploring-advanced-linux-commands-part-1
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1690049656663/5439e6c8-4f2f-4d03-adcf-20fdae84a3ce.png
tags: devops-journey, 90daysofdevops, day6, trainwithshubham, linux-advance-commands

---

---

# 📍Introduction

📚 In this 2-part blog series, we'll explore advanced Linux commands! After learning basic Linux commands and mastering them we are now ready to learn some advance Linux commands. By the end, you'll be familiar with file permissions, users and groups, some administrative commands, filtering, etc 💪. Get ready to unlock the potential of Linux commands and join me on this exciting Linux journey! 🚀

---

# 📍Users & Groups

📝Note: Any operations on users and groups can only be done by the root user, normal users will have to use #sudo before every command to perform operations on users and groups.🖊

## ✔Users

In Linux, a user is similar to a user account in Windows. Each user has a unique identity to which they can log in and perform various operations on the system. Both Linux and Windows support multiple user accounts users and allows each user to give a separate work environment. In Linux, each user gets a separate file structure and a work environment to perform their operations. By file structure, I mean this:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690028708950/ef5b6cde-2384-4edc-8f01-9a4d5ca0e1ab.png align="center")

As shown above every user will have a file structure like this. All the existing users in the system are stored in `/etc/passwd` file with their `<username>`. You can see it by doing `#cat /etc/passwd`. And all the user's account passwords are stored in `/etc/shadow` file in an encrypted format.

### 📍Let's explore some user management commands:

1. `#useradd <username>`: Used to add a new user to the system. For a normal user use `sudo`.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690029325286/6b433fb1-5342-4ca6-b23c-530f9f905763.png align="center")
    
    In the above image, you can see that the user has been added successfully to the system. It can also be seen in the `/etc/passwd` file. But as you can see there is no directory of the user created inside the home directory. For that, we use the option `-m`:
    
    * `#useradd -m <username>`: This will add a user as well as create a directory for the user inside the home directory.
        
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690030329553/a01ae170-b49a-4ebc-977b-681e4da8df1a.png align="center")
    
2. `#passwd <username>`: It is used to change a user's password so that, it can be used to log in to that user's account.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690030702191/628088fb-fc69-4563-a824-47522ddf644c.png align="center")
    
    Normal users can only change their password, while the super-user can change the password of any user.
    
3. `#su <username>`: It is used to switch to the user whose `<username>` is specified.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690031352935/85f0a869-3c8e-4837-9b04-7aec8f1ab605.png align="center")
    
    As I am a normal user it is asking for the password. After typing the password we set previously, we logged in to a `varun` user account. If I had tried to switch user as a root user it would have not asked for a password.
    
4. `#exit` or Press the "Ctrl + d" key: It is used to exit from a user's account.
    
5. `#userdel <username>`: Used to delete a user account. Use '`sudo`' for a normal user.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690031943813/4f9da0da-e46f-4403-8c62-73302c20dfd8.png align="center")
    
    As you can see, the user has been removed and it is also deleted from the `/etc/passwd` file. But the user `varun` directory inside the `/home` directory still exists. To remove that we use the option `-r`:
    
    * `#userdel -r <username>`: Used to delete a user account as well as its home directory.
        
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690032232315/dd1689b2-3d37-4158-834e-3fd8f5e4e909.png align="center")
    
6. `#usermod`: It is used to modify the user account.
    
    * `-l (--login)`
        
        `#usermod -l <new_username> <username>`: It will change the user's name from `<username>` to `<new_username>`.
        
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690032843243/c804e4b2-f354-48e6-9d1f-0c513fd4806c.png align="center")
    
    As you can see, the username `varun` changed to `lokesh`. The second `varun` highlighted in red in the same line is the group name.
    

## ✔Group

In Linux, a group is a collection of user accounts. Whenever we create a new user in Linux it by default creates a group with the same name as the user.

All the existing groups in the system are stored in /etc/group file with &lt;groupname&gt;. You can see it by doing `#cat /etc/group`.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690035292016/97a38355-4efe-4871-b8ec-f93480eda2a7.png align="center")

I used the tail command to print the last 1 line because there were many groups. `varun` here is the group name, `x` is the password, and `1001` is the group id (GID).

### 📍Let's explore some Group management commands:

1. `#groupadd <group_name>`: Creates a new group with the name `<group_name>`.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690035632744/9abc9ee2-9e5b-4fd5-a754-41ee3f609d8b.png align="center")
    
    A group `devops` was created with the group id (GID) `1002`.
    
2. `groupmod`
    
    * `-n (name)`: The name of the group will change.
        
        `#groupmod -n <new_name> <old_name>`: The group name will change from `<old_name>` to `<new_name>`.
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690036513845/02f3dd89-56b2-44f2-a218-d1ded4f409ea.png align="center")
        
    * `--gid or --g/-g`: The group id (GID) will change.
        
        `#groupmod --gid <newGID> <group_name>`: It will change GID of the group `<group_name>` to `<newGID>`.
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690037183574/4a5a43ac-d196-4d95-bf5f-c7222a7a4c83.png align="center")
        
3. `#groupdel <group_name>`: It deleted the group specified.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690036089689/8038434f-e255-475d-ad9a-87c4dcdcf506.png align="center")
    
    A group named `devops` was deleted.
    
4. `#gpasswd`: This command is used to administer `/etc/group`, and `/etc/gshadow`
    
    * `-a`: It is used to add a user.
        
        `#gpasswd -a <username> <groupname>`: It will add user `<username>` in the group `<groupname>`.
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690038167061/52a20cd0-eacd-4d73-89b8-7a3b7c883210.png align="center")
        
    * `-M`: It is used to add multiple users at a time.
        
        `#gpasswd -M <username1>,<username2>,<username3> <group_name>`: It will add users `<username1>,<username2>,<username3>` in the group `<group_name>`.
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690038561110/ef8acc0a-cbc0-4a81-b796-3ab8b6a03b65.png align="center")
        
        As you can see, `aryan`, and `lokesh` users have also been added to the `devops` group.
        
    * `-d (delete)`: It will remove the user from the named group.
        
        `#gpasswd -d <username> <group_name>`: It will remove the user `<username>` from the group `<group_name>`.
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690038907262/6cf07137-83f2-4bae-ad67-0ef47f73f22e.png align="center")
        
5. `#groups <user_name>`: Shows all the groups the user `<user_name>` is a part of.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690039408197/924f14ca-7088-4a84-9e6d-ab0ae7056e65.png align="center")
    
6. `#usermod`: It is used to modify the user account.
    
    * `-aG (append group)`: It will append the user to the group.
        
        `#usermod -aG <group_name> <username>`: It will add the user `<username>` to the group `<group_name>`
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690039617246/b23c66cf-8583-425f-89fd-da59e55e51ae.png align="center")
        
        *Note: Make sure to use* `-a` *option because, if you only use the* `-G` *option will override the current group the user is a part of.*
        

---

# 📍File Permissions & ownership

One of the many features that set Linux apart from other OS is that multiple users in Linux can access the same system simultaneously. To achieve this there is a need for a method to protect the users from each other. This is the reason file permissions were needed.

## ✔Permission classes:

There are 3 permission classes:

1. User (the user who created the file)
    
2. Group
    
3. Others (other users)
    

To know which user created a file we use the command #ls -l &lt;filename&gt;

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690040141144/53877411-0b4b-4f0b-a125-d907a4f1e3f5.png align="center")

In the above image, the first block `drwxrwxr-x` tells us permissions given to the user, group, and others:

* r - Read, w - Write, x - Execute
    
* The first character `d` represents the file type. Here, the file type is a directory.
    
* The next 3 characters `rwx` represents the permissions assigned to the user who created the file.
    
* The next 3 characters `rwx` represents the permissions assigned to the group.
    
* The next 3 characters `r-x` represents the permissions assigned to other users.
    

The second block represents the number of hard links, in this case `2`.

The third block represents the user who owns the file (&lt;user\_name&gt;). Here, it is `ubuntu` user.

The fourth block represents the group that owns the file(&lt;group\_name&gt;). Here it is `ubuntu` group.

The fifth block represents the file size. Here it is `4096 (in bytes)`.

The sixth block represents the date of creation.

At last, the name of the file, in this case, is `devops`.

## ✔Changing permissions

`#chmod` command is used to change the permissions given to the users, group, and others.

There are 2 ways to change permissions:

1. Non-numeric way
    
2. Numeric way
    

### 📍Non-numeric way

Here, the users are denoted by u, a group is denoted by g, and others are denoted by o.

To give permissions we use + and to remove permission we use -

Let's take an example to understand it better:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690040736543/0fc7527a-6678-40f6-b986-e4bff37033fb.png align="center")

The above `test.txt` file has permissions `rw-rw-r--`.

The user has read(r), and write(w) permission, to add execute(x) permission we will do `u+x`:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690040945424/d5153298-7a1b-405a-9a71-bda608fc7aa3.png align="center")

As you can see the user's permission changed from `rw-` to `rwx`.

To remove the permission we will use (-):

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690041105941/e4f356b4-a2cb-4fe3-b7ed-6751c60495be.png align="center")

As you can see, the user permissions changed from `rwx` to `r-x`.

Similarly, you do change permissions to the group(g) and to others(o).

### 📍Numeric way

An example of giving permission using a numerical way:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690041273208/704121e2-1544-4441-a55e-e6cb9823a35d.png align="center")

In the above image, the 3-digit number each digit represents the permissions given to the user, group, and others respectively. In the above example, 7 is the permission for the user, 7 is for the group, and 7 is for other users.

Here, all the 3 permissions are assigned a number:

read (r) - 4, write (w) - 2, execute (x) - 1

If I want to give read(4), write(2), and execute(1) permission then we will add the numbers each is assigned to i.e. 4+2+1 = 7. Therefore, 7 represents all the permissions.

If I want to give read(4) and execute(1) permission then it will be 4+1 = 5.

If I want to give no permission it will be 0.

If I want to give only write(2) permission then it will be 2.

Example 1:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690041446602/b635a795-9def-4d40-886a-8003bc186b4c.png align="center")

In the above example, we know 7 means all the permissions. Therefore, 777 means all the permissions are given to the user, group, and others respectively.

Example 2:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690041616499/01ba0060-dd07-4ff7-948e-5b77be7cf400.png align="center")

Think for yourself what permissions are given and then check the answer.🤔

<details data-node-type="hn-details-summary"><summary>Ans</summary><div data-type="detailsContent">The user is given permission 7 which means <code>4+2+1</code> i.e. read(r), write(w), and execute(e). The group is given permission 6 which means <code>4+2</code> i.e. read(r), and write(w). The group is given permission <code>4</code> which means only read(r).</div></details>

## ✔Changing ownership of the file

📝Important: Only a root user can change the owner of the file. Only the root or the owner can change a file's group.

`#chown` command is used to change the ownership of a file.

`#chown <username> <file/directory>`: The user `<username>` ownership of the file `<file/directory>`.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690042441166/f423b5ee-c929-42f2-a54a-76c44d6f15a3.png align="center")

---

# 📍Filtering (grep, find, awk, & sed)

Suppose you are in a scenario where you have to find a single word, or a particular column from a large file and a DevOps engineer faces a lot of scenarios like these. For such scenarios, we use Filtering commands.

I copied some lines of a log file from here [IBM\_logs](https://www.ibm.com/docs/en/zos/2.2.0?topic=problems-example-log-file) and then pasted into a directory called `ibmlogs.logs` using the Vim editor.

## ✔grep - global regular expression print

`#grep word <filepath>`: It finds the word from the file when given its path.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690045843093/4e265580-3747-4cf0-938d-76e62ac10ea8.png align="center")

It gave me all the lines which had `TRACE` in it.

* `-r`: With this the grep command can also find the word inside a directory.
    
    `#grep -r word <file/directorypath>`.
    
* `-i (case insensitive)`: It will find a word irrespective of its case.
    
    `#grep word <filepath>`: It will display the word even if that word is in capital letters or small.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690046209170/47baf852-a6a1-4833-9560-c5383254492a.png align="center")
    
    I typed `initialized` in the command but it also printed Initialized, which would not have been the case if we were not using `-i`.
    

## ✔awk

Awk itself is a programming language. It is used to trim, filter a file based on our requirements and also find a word.

Let's take an example of the `ibmlogs.log` file:

1. I want to search for `TRACE` in that file, for this, the command will be:
    

`#awk '/TRACE/' ibmlogs.log`: This will display all the lines containing `TRACE` inside `ibmlogs.log`.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690047353331/52d85075-8812-41ce-aeb3-b20c8981e710.png align="center")

1. Now I want all the lines containing `TRACE` but only the 1st, 3rd, and the 6th column for this the command will be:
    
    `#awk '/TRACE/ {print $1,$3,$6}' ibmlogs.log`: This will display the 1st, 3rd, and the 6th column containing the word `TRACE`.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690047698538/39faf548-fcdb-4414-a25f-7177e1a014fb.png align="center")
    

## ✔sed - stream editor

It is used to search for a word in the file and replace it with the word required to be in the output.

📝Note: It will only modify the output, there will be no change in the original file.

Syntax: `#sed 's/word_being_replaced/word_replaced_by/g' <filename_or_filepath>`

`s` - search for

`g` - is for global i.e. if a word repeats twice in a line then it will consider it, if not mentioned then it will only consider the very first occurrence of the word inside a line and will move to the next line.

Let's display the first 10 lines of the `ibmlogs.logs` file and replace the word `INFO` with `VARUN`, the command for this is:

`#sed 's/TRACE/VARUN/g' ibmlogs.log`

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690048184340/a08371a0-ef29-43ed-b131-0b2c797b929b.png align="center")

All the lines containing `TRACE` is replaced by `VARUN`. I just piped `|` two commands to display only top 10 lines of a file.

*You can concatenate 2 commands using* `|` *key (above the enter button), the left command's output will be the input to the right command. More about this in my next blog.*

---

# 📍Conclusion

Thank you for reading this blog! 📖 We've reached the end of this Advanced Linux Commands blog. In my next blog, get ready to delve into some more exciting advanced Linux commands. 🚀 Until then, keep practicing these commands, and get familiar with them. 💻 Stay tuned for more valuable content coming your way!

If you enjoyed this blog and found it helpful, please give it a like 👍, share it with your friends, do share your thoughts, and give me some valuable feedback.😇 Don't forget to follow me for more such blogs! 🌟

---

# 📍Reference

* [Stackoverflow](https://stackoverflow.com/questions/2359270/using-if-elif-fi-in-shell-scripts)
    
* [GFG](https://www.geeksforgeeks.org/)
    
* [ChatGPT](https://openai.com/chatgpt)
    

---