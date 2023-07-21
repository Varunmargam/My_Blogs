---
title: "Mastering Basic Linux Commands for DevOps Excellence (Part 1)🐧"
datePublished: Tue Jul 18 2023 18:29:04 GMT+0000 (Coordinated Universal Time)
cuid: clk8mp3ff000009lb7v86hjjy
slug: mastering-basic-linux-commands-for-devops-excellence-part-1
canonical: https://varunmargam.hashnode.dev/mastering-basic-linux-commands-for-devops-excellence-part-1
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1689770842344/3fa427c6-3dcb-4dec-846c-2c69776c7c52.png
tags: linux-for-beginners, devops-journey, 90daysofdevops, day2, trainwithshubham

---

# 📍Introduction

📚 In this 2-part blog series, we'll explore basic Linux commands! Whether you're a beginner or want to refresh your Linux fundamentals, this guide has got you covered. By the end, you'll have a solid foundation in Linux commands 💪. Get ready to unlock the potential of Linux commands and join me on this exciting Linux journey! 🚀

📚Before diving into the commands, let's **familiarize** ourselves with key **Linux terminologies** frequently used to enhance our understanding.🧐

## Linux terminologies used often :

1. ### 📂Directory: 📂
    
    * In Linux, directories are used to organize and store files and other directories. They provide a hierarchical structure for efficient data organization, similar to folders in other operating systems.
        
        📁 Common Directories in Linux:
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689695499780/b64b4109-426e-45a2-ae8e-634eb6642c58.png align="center")
        
        * 🏠 /home: Stores user-specific files and personal directories.
            
        * 💻 /bin: Contains essential executable binaries.
            
        * ⚙️ /etc: Stores system configuration files.
            
        * 🖥️ /media: Mount point for external devices like USB drives.
            
        * 🚀 /root: Home directory for the root user.
            
    
    🔍Understanding Linux directories is essential for efficient file management and system administration. 🚀💻
    
2. ### 🌱Root:🌱
    
    On Linux, "root" refers to two key concepts: the root directory and the root user.
    
    📂 **Root Directory:** The root directory ("/") is the parent directory that contains all files and folders on your system *(can be seen in all the directories in the root directory in the above image)*. It serves as the starting point of the directory structure and is denoted by the "/" (forward slash) wildcard in commands.
    
    **👑 Root User:** The root user, also known as the superuser or simply root, possesses ultimate administrative privileges. This user has unrestricted access to view, modify, and delete any file or directory. They hold the highest level of control over the system, allowing them to make critical changes and configurations.
    
    (photo)
    
3. ### 📦Package manager📦:
    
    Q) What's your go-to approach for downloading applications or games on your smartphone📱💡?
    
    Ans - Just like downloading applications from PlayStore 📲, Linux uses package managers to distribute and manage software.
    
    ✨ How Package Managers Work: In Linux, applications are packaged and distributed as software packages. To install a package, specific commands are executed through the package manager. It fetches the required packages from the Linux distribution's official repository.
    
    🔧 **Popular Package Managers**: Linux distributions have different package managers. Here are three widely used ones:
    
    * **APT**: Used by Debian and Ubuntu-based distributions.
        
    * **RPM**: Commonly found in Fedora, CentOS, and RHEL.
        
    * **Pacman**: Associated with Arch Linux and its derivatives.
        
    
    📦Package managers simplify the process of installing, updating, and removing software. They handle dependencies, ensuring all required components are properly installed.
    
    (can add an article where Linux distros are mentioned)
    
    (photo)
    
4. ### 🔖Repository🔖
    
    Software repositories🔖 are remote servers that house a collection of packages📦 and metadata. They serve as the primary source for obtaining software in Linux distributions.
    
    🌐 **Repository Types**: Linux distros maintain their (own) repositories or use those of their parent distro, providing centralized software distribution to users.
    
    📦 **Package** **Collection**: Repositories store a wide range of packages, including applications and libraries, readily accessible for installation and updates.
    
    (photo)
    
5. ### ⚙️Process⚙️
    
    A process is nothing but multiple lines of code executing. Linux excels at running numerous processes simultaneously to accomplish complex tasks. 🚀💻
    
    🚀 From the moment you boot the OS, processes start and initiate various child processes, forming a dynamic system.
    
    🔍 To explore processes in Linux, you can utilize the command "#ps -ef"
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689695973159/2d3d6872-eb6f-4c86-aecd-142ea01f44ec.png align="center")
    
    This command displays process-related information, including:
    
    * PID - Process ID
        
    * PPID - Parent process ID
        
    
    You can see that the root process has process id as 1. PID 0 is for the process executed at the booting time.
    
    Processes play a crucial role in the functionality of Linux, orchestrating the execution of code and facilitating multitasking capabilities. 🔄💻
    

***💥Note: Practice all these Linux commands in*** `/home/username` ***directory.💥***

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689696336076/d40cd205-7f62-4246-b967-08eecf7229ad.png align="center")

# 📍 Ready to Dive into Basic Linux Commands🐧? Let's Go! 🚀💻

Now that we have covered the fundamental Linux terminologies, it's time to explore some essential Linux commands. Get ready to unleash the power of the command line and take your Linux skills to the next level! 💪🔥

**In Linux, every command follows a standard syntax:**

`command <options> <source> <destination>`

When working with commands in Linux, you'll come across various scenarios where options, source, and destination parameters **may or may not be required** for successful execution.

## Here are some basic commands:

1. `#whoami`: displays the currently logged-in user name.
    
2. `#pwd` (present working directory): displays the present working directory.
    
3. `#clear`: clears the screen.
    
4. `#date`: displays time and date, in the format of :
    
    Day-Month-Date-Hours-Minutes-Seconds
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689697035770/cc47f30c-fd44-451a-b71a-e1dfb3db31e7.png align="center")
    
5. `#echo "text"`: used to print the text mentioned in (" ") on the screen.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689699416904/f47c4d0a-c11b-4918-85c9-e0aae19f722b.png align="center")
    
6. `#ls` command contains 2 parameters:
    
    `ls <option> <destination>`
    
    * ls &lt;destination&gt;
        
        1. `#ls`: when no destination is mentioned, it displays available files and directory list in the present working directory
            
        2. `#ls <path>`: displays available files and directory list inside the directory path which is mentioned.
            
    * ls &lt;option&gt;
        
        1. `#ls -a`: displays hidden files in the current working directory. Hidden file denoted as "." & "..".
            
        2. `#ls - l`: displays a long list of all the files and directories along with some additional information.
            
        
        Like these, there are many more options that you can explore.
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689697300521/fb31cb8e-6f8f-46df-8774-409aba49cac7.png align="center")
        
7. `#uname`: displays the name of the kernel.
    
    `#uname -r`: displays the version of the kernel.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689699548726/015d2e38-219b-4083-a4d9-c07d0bf4198c.png align="center")

# 📍Path - absolute and relative.

### Q) What is a path?

Ans - A path is a unique location of a file or a folder in a file system. There are 2 types of paths -

1. Absolute path
    
2. Relative path
    
3. ### Absolute path
    
    An absolute path is a path of the directory or file from the root directory ("/").
    
4. ### Relative path
    
    A relative path is a path of the directory or file from the present working directory
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689699985845/1901eafb-7572-44dd-8e75-1fccb1851ddc.png align="center")

After `#pwd` command when we were in `/home/ubuntu` directory to go to `devopsdir` we can put **relative path** `linux-practice/devopsdir` since `linux-practice` is available in the current directory but if it was not present then I would have to mention the absolute path i.e. `#/home/ubuntu/linux-practice/devopsdir.`

This path can be specified while writing commands which require &lt;source&gt;,&lt;destination&gt; as a parameter.

# 📍Create a directory and file.

`#mkdir <directoryname>`: Creates a directory named &lt;directoryname&gt; as mentioned in the present working directory.

1. `#mkdir <directoryname1> <directoryname2>...`: Creates multiple directories at once.
    
2. `#mkdir <directorypath>`: Creates a directory at the specified path if the path exists.
    
3. `#mkdir -p <directorypath>`: Creates a directory at the specified path if the path does not then it creates the mentioned directory path.
    
4. `#mkdir /directoryname{1..10}`: Creates 10 files as specified in '`{}`'.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689700837245/36d119f2-d66d-4b20-8516-dfadb18eb9eb.png align="center")
    

1. `#touch <filename>`: Creates a file named &lt;filename&gt; in the present working directory.
    
    1. `#touch filename{1..10}`: Creates 10 files as specified in '`{}`'.
        
    2. `#touch <filename1> <filename2>...`: Creates multiple files as mentioned at once.
        
        Try to run touch commands on your own.
        

# 📍Perform operations on a file & directories

1. `#cd <directorypath>`: Used to change directory(cd). `<directorypath>` can be absolute or relative.
    
    Some cd command shortcuts:
    
    * `#cd ..` - To go a directory back from the present working directory.
        
    * `#cd ~` - Goes back to the /home/username directory.
        
        ***Note: Here, (~) represent /home/username.***
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689701192289/2abcfee5-195a-42a1-a16f-9bc33c928b15.png align="center")
        
2. `#rm <filename> or <filepath>`: Deletes the file. Use &lt;filename&gt; if the file is available in the present working directory if not then use &lt;filepath&gt;.
    
3. `#rm -rf <directoryname> or <directorypath>`: Deletes the directory if the directory is empty (check if it does give the prompt or not). Use &lt;directoryname&gt; if the directory is available in the present working directory, Ii not then use &lt;directorypath&gt;.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689702558268/25889484-ab5e-4978-8b0a-da225a6551b3.png align="center")
    
    Since my present working directory was test directory and test11.txt was present outside the test directory I used rm &lt;filepath&gt; and used rm&lt;filename&gt; to delete the file available inside the test directory.
    
4. `#mv <source> <destination>`: Moves the file or directory from the source path to the destination path.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689702959830/f53ab637-42e8-4cc3-8257-1e2449a37bba.png align="center")
    
5. `#mv <filename> <newfilename>`: Renames the file from &lt;filename&gt; to &lt;newfilename&gt;.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689703096568/c78f0056-28b4-468f-8c75-dbdf921cfc5f.png align="center")
    
6. `#cp <source> <destination>`: Used to copy files from the source path to the destination path.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689703812153/a8f83f84-495b-40fc-91ca-1645dcc1e8b4.png align="center")
    
    `#cp -r <source> <destination>`: Used to copy directories from the source path to the destination path.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689703492946/dbbdf7c3-8ecf-4618-bfd7-c14546071d28.png align="center")
    
7. To Edit files we have to use Vim editor. Stay tuned for an upcoming blog where we dive deep into this topic. 🚀💻
    

💡Tip: It is not feasible to know all options for every command for that we have a manual for every command on how to use it provided by Linux which can be seen using the command:

`#man command_name` and press 'Q key' to quit the manual.

Try this "man" command yourself example "`#man ls`".

# 📍Conclusion

Stay tuned for the next part of this 2-part blog series, where we'll dive deeper into more essential Linux commands! In the meantime, keep practicing the commands we've covered so far, play around with them, and enhance your comfort level with Linux. Stay tuned! 🚀💻

# 📍References

* [Linux Terminologies referred from this article](https://www.makeuseof.com/tag/linux-confusing-key-terms-definitions/)
    
* [ChatGPT](https://openai.com/chatgpt)
    
* [Google](http://google.com)