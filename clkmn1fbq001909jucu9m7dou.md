---
title: "Linux Cheat Sheet: Compiling My Linux Knowledge"
datePublished: Fri Jul 28 2023 13:47:26 GMT+0000 (Coordinated Universal Time)
cuid: clkmn1fbq001909jucu9m7dou
slug: linux-cheat-sheet-compiling-my-linux-knowledge
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1690551547849/f613c749-a148-4a38-b59b-2669eae2207c.png
tags: devops-journey, 90daysofdevops, day12, trainwithshubham, linuxcheatsheet

---

---

# 📍Linux Terminologies

* `Boot Loader`: Program that loads the Linux OS. Eg: GRUB - Grand Unified Boot Loader. Initiates the `Kernel`. It resides in the `/` base directory `/boot`.
    
* `Kernel`: It is an interface that connects users to the hardware via shell. It runs the very first `init` process, which resides in `/sbin/init`.
    
* `Shell`: Shell is a command line interface that allows the user to communicate with the kernel. By default, Linux contains a bash shell. There are other kinds of shells like Korn shell, Z shell (zsh), Secured shell (ssh), etc.
    
* `Daemon (or services)`: In Linux Daemon is a program that runs on the background and takes care of executing all the subprocesses required for the OS to run properly. In Linux processes ending with `d` are daemon processes. Eg: the `systemd` process is executed by the init process.
    
* `Root or /`: In Linux root is the base directory where the OS resides. There is also a root directory for the root user which has all the permissions given to it.
    
* `Directory`: In Linux directory is a folder. It is a type of file.
    

---

# 📍Linux Distributions

Linux distributions are classified based on how they are packaged.

* **RPM(RedHat Package Manager) based**: RHEL (Red Hat Enterprise Linux), Centos, Oracle Linux.
    
* **Debian-based (.deb)**: Ubuntu, Linux Mint, etc., and many other distros.
    

---

# 📍Basic Commands

The commands are for Ubuntu Linux but most of the basic commands may work in other distros:

* `whoami`: Displays your current user name.
    
* `pwd`: Displays your current working directory.
    
* `ls <path>`: Lists all the files and directories from the given &lt;path&gt;.
    
    `ls -l`: Lists the files along with some metadata.
    
    `ls -a`: Lists all the files along with the hidden files.
    
* `clear`: Clears the working screen.
    
* `cd <directory_name or path>`: Changes to the directory of the path provided.
    
* `date`: Displays the date of the system.
    
* `uptime`: Tells how much time the system is running.
    
* `history`: Lists all the previously executed commands.
    
* `~`: Denotes /home/user.
    
* `echo "text"`: Prints the text on your screen.
    
* `$0`: Variable that stores the name of the shell system that is running. Execute the `echo $0` command.
    
* `man <command>`: Provides a manual for the &lt;command&gt;. Press the q key to exit from the manual.
    
* `sudo`: Gives the normal user to execute administrative commands by giving them root user privileges temporarily.
    
* `ps -ef`: Displays every process in the system along with their PID-process\_id and PPID-parent process\_id and more.
    

---

# 📍Files & Directories

## ✔Directories

* `mkdir dir`: Creates a directory with the name `<dir>`.
    
* `mkdir dir{1..n}`: Creates n directories.
    
* `mkdir -p dir1/dir2/..`: Creates a directory inside a directory.
    
* `cd`: Changes to the particular directory or the path if provided.
    

## ✔Files

* `touch <file>`: Creates a file and the type of the file is decided by the extension provided.
    
* `touch file{1..n}`: Creates n files.
    
* `touch file1 file2 file3..`: Creates multiple files.
    
* `cat file`: Displays the content of the file.
    

## ✔Operations on files and directories

* `cp <source> <destination>`: Copy files from the `source` path to the `destination`.
    
    `cp -r <source> <destination>`: Copy directories from its `source` to the `destination`.
    
* `rm <file or path>`: Removes/Deletes the file.
    
    `rm -r <dir or path>`: Removes/Deletes the directory.
    
* `mv <source> <destination>`: Moves the file or the directory from its `source` to the `destination`.
    
* `mv <old_name> <new_name>`: Renames the file or a directory.
    

---

# 📍Vim Editor

It is used to edit files. The `#vim <file>` command opens the file in the Vim editor.

It has 3 modes:

1. **Command mode** (Default mode)
    
2. **Insert mode** (edit mode) (Press Esc to go back to the Command mode)
    
3. **Extended mode**
    

### ✔Command Mode

* `i`: Goes to the insert mode to edit files.
    
* `ndd`: Deletes n number of lines.
    
* `nyy`: Copies n number of lines.
    
* `p`: Paste the copied line below the cursor.
    
* `u`: Undo the changes.
    
* `/<word>`: Searches the word.
    

### ✔Extended Mode

* `:` - Moves from the command mode to the extended mode, Therefore all the commands start from `:`.
    
* `:w` - Saves the changes made in the file.
    
* `:q` - Quits from the Vim editor.
    
* `:q!` - Forcefully quit or quit the file without saving.
    
* `:se nu` - Set the number to all the lines.
    
* `:se nonu` - To remove numbers from the lines.
    
* `:n` - Goes to that line number n.
    

---

*📝Note: These user and group management commands can only be executed by the root user, normal users who are present in the sudoers file can execute these commands by adding sudo at the beginning of the command.*

# 📍User Management

* `useradd <new_user>`: Adds a new user with the name `<new_user>` to the system.
    
* `passwd <user>`: Sets password to the `<user>` account for secure login.
    
* `su user`: Switch the user from the current user to the username `user` provided. Before switching to that user it asks the password we set for the user.
    
* `exit`: Exit from the user's account.
    
* `userdel user`: Deletes the user.
    
* `usermod -aG group user`: Adds the user to the group.
    
* `/etc/passwd`: Contains all the users currently in the system along with the metadata like UID.
    

---

# 📍Group Management

* `groupadd <group_name>`: Adds a group in the system.
    
* `groupdel <group_name>`: Deletes the group in the system.
    
* `gpasswd -a user group`: Adds a user to the group.
    
* `gpasswd -M user1,user2,user3.. group`: Adds the members (multiple users) to the `group`. (No spaces after the '`,`').
    
* `gpasswd -d user group`: Removes the user from the group.
    
* `groupmod -n <old_name> <new_name>`: Renames the group.
    
* `/etc/group`: Contains all the groups currently in the system along with the metadata like GID, users added to it, etc.
    

---

# 📍File permissions

`chmod <permissions> file`: Syntax of the `chmod` command used to change file permissions.

Permissions are Read - r, Write - w, Execute - x.

**There are two ways to give permissions to the file:**

1. Non-numeric
    
2. Numeric
    

### ✔Non-numeric way

Users/Owner - u, Groups - g, Other users - o.

* `u+`: To give permissions to the user it can be r, w, x, or rx any of the combinations you want to give.
    
* `u-`: To remove permissions from the user.
    
* Similar for the Group (g) and other users(o).
    

### ✔Numeric way

* Read - 4
    
* Write - 2
    
* Execute - 1
    
* To give read and write permission it is 4+2 i.e. 6.
    
* To give read and execute permission it is 4+1 i.e. 5.
    
* To give read, write, and execute permission it is 7 (4+2+1).
    
* The command `#chmod 777 file` denotes the permissions given to the owner group others.
    

## ✔Changing Ownership of the File

* `chown` command is used to change the owner of the file. Only the root user can change a file's owner.
    
* `chown -R new_user <file/directory>`: Changes the ownership of the file to the `new_user`. `-R` changes the ownership of the directory as well as all the files and directories inside it.
    
* `chgrp` is used to change group ownership. Only the root or the owner can change the file's group
    
* `chgrp -R new_group <file/directory>`: Changes the ownership of the file to the `new_group`.
    

---

# 📍Grep & awk

* `grep word <file path>`: Searches a `word` from the file whose `<file path>` is provided.
    
* `grep -n word <file path>`: Displays the `word` match with the line number.
    
* `grep -i word <file path>`: Searches a `word` insensitive to the word's case.
    
* `grep -v word <file path>`: Search and displays all the lines which do not contain the `word`.
    
* `grep -c word <file path>`: Displays the count of the `word` in the file.
    
* `awk '/word/' <file path>`: Searches and displays the word from the file.
    
* `awk '/word/ print{$1,$2,$3}' <file path>`: Displays only the 1st, 2nd, and 3rd field of the line containing the `word`.
    

---

# 📍Package Management (APT)

Downloading or removing packages can only be executed by the root user.

* `apt install <package>`: To install any package in the system.
    
    `apt-get install`
    
* `apt remove <package>`: To remove the installed package.
    
* `apt update`: Updates all the indexes of the installed packages in the system repository with the current versions.
    
* `apt upgrade`: Used to update the packages in the system. It installs the latest versions of the packages that were retrieved using `#apt update`.
    

---

# 📍Services

The `systemctl` commands are used to control the services in the system.

* `systemctl start service`: Starts the service.
    
* `systemctl enable service`: Enables the service i.e. when the system is booted the service will also get started.
    
* `systemctl disable service`: Disables the service if it was enabled.
    
* `systemctl status service`: Checks and displays the status of the service active or inactive.
    
* `systemctl stop service`: Gracefully stops the services along with their child processes.
    
* `systemctl kill service`: Kills the service forcefully not stopping the child processes.
    

---

# 📍Conclusion

Thank you for reading this blog! 📖 Hope you have gained some value.

If you enjoyed this blog and found it helpful, please give it a like 👍, share it with your friends, do share your thoughts, and give me some valuable feedback.😇 Don't forget to follow me for more such blogs! 🌟

---