This document is a beginner-friendly introduction to Linux fundamentals. It explains the basics of how Linux works, why it is important, and how users interact with it from the command line and other importent ps and systemctl and kill commends.

* *Main topics covered*
    - [What is Operationg Syatem](#01-what-is-operating-system)
    - [Root](#02-what-is-the-root)
    - [Filesystem](#03-introduction-to-filesystem)
    - [File-Wwnership](#04-file-ownership)
    - [Wildcards](#05-wildcards-)
    - [ACL](#06-access-control-list-acl)
    - [HELP](#07-help-commands)
    - [adding-text](#08-adding-text-to-filesredirection)
    - [PIPE |](#09-pipes--)
    - [File-maintenance-commands](#10-file-maintenance-commands)
    - [File-text-processors-commands](#11-file--text-processors-commands)
    - [grepegrep-text-processors-commands](#12-grepegrep---text-processors-commands)
    - [text-processors-commands](#13-sortunip---text-processors-commands)
    - [compare-files-diff-and-cmp](#14-compare-files-diff-and-cmp)
    - [vi-and-vim-editors](#15-diffrence-between-vi-and-vim-editors)
    - [user-account-managemen](#16-user-account-management)
    - [enable-password-aging](#17-enable-password-aging)
    - [linux-account-authentication](#18-linux-account-authentication)
    - [system-utility-commands](#19-system-utility-commands)
    - [processes-and-jobs](#20-processes-and-jobs)
    - [systemctl-command](#21-systemctl-command)
    - [ps-command](#22-ps-command)
    - [top-command](#23-top-command)
    - [kill-command](#24-kill-command)
    - [process-signals-in-linux](#25-process-signals-in-linux)
    - [crontab](#26-crontab-command)
    - [at-command](#27-at-command)
    - [log-monitoring](#28-log-monitoring)

------------------------------------------------------------------------------------
### 01. What is Operating system?
------------------------------------------------------------------------------------
- An operating system is system software that manages computer hardware and software resources and provides common services for computer programs. 
- The operating system is a vital component of the system software in a computer system. Application programs usually require an operating system to function.

* In simple words
- An operating system(OS) is software that acts as a middleman or a bridge between computer hardware and the computer user. it provides a user interface and controls the computer hardware so that software can function

* **Types of Operating Systems**
1. Desktop Oprating System e.g, Windows, Linux, MacOS 
2. Server Operating System e.g, Windows Server, Linux Server
3. mobile Operating System e.g, Android, iOS
4. Embedded Operating System e.g, routers, smart TVs, VxWorks, automobiles, home appliances, and other devices that are not traditional computers.
5. Real-Time Operating System (RTOS) e.g, used in critical systems like medical equipment, car ECUs, and industrial control systems, where timely and deterministic responses are crucial.  

* **What is Linux?**
- linux, in simple terms, is a free and open-source operating system.
- its similar to windows and macOS, but it is based on the Linux kernel, which was created by Linus Torvalds in 1991.
- Linux is very popluar for its stability, security, and flexibility. it can be modified and distributed by anyone. which has led to many diffrent versions, known as distribution is tailored for diffrent uses and preferences.
- its open-source nature means that a community of developers and users contribute to its development.

* **Why learn Linux or its importance**
- Widely used in servers and cloud computing 
- free software and open-source nature
- strong security and stability
- command-line interface and scripting capabilities
- community support
- Understanding of other operating systems

* **Linux flavors or distributions**
- Ubuntu
- Fedora
- Debian
- Red Hat Enterprise Linux (RHEL)
- CentOS
- Arch
- openSUSE
- linux mint
- Kali Linux
- gentoo
- alpine linux

* **Important Things to Remember in Linux**
* Linux is super-user account called root
    - root is the most powerful account that can create, modify, and delete accounts and make changes to system configuration 
* Linux is case-sensitive system
    - ABC is NOT dame as abc
* Avoid using spaces when creating files and directories 
* linux kernel is not an operating system. it is a small software within Linux operating system that takes commands from useers and pass them to system hardware or peripherals. it is responsible for managing system resources and providing an interface between software and hardware.
* Linux is mostly CLI not GUI
* Linux is very flexible as compared to other operating systems.

* **Access Linux via Putty or SSh**
- ssh -l username 192.168.1.5

* **Command Prompts and Getting Prompts Back**
* What are command prompts?
  - A coommand prompt, also referred to somply as a prompt, is a short text at the start of the command line followed by prompt symbol on a command line interface. It indicates that the system is ready to accept commands from the user. The prompt typically includes information such as the username, hostname, and current working directory.

* **Linux Users**
- Linux is used by a wide range of users and organizations due to its versatility, stability and open-source nature.
- Developers
- Educations Institutions
- Governmet agencies
- Businesses and Enterprises
- Tech companies
- CLoud and web servers

------------------------------------------------------------------------------------
### 02. What is the ROOT?
------------------------------------------------------------------------------------
* There are 3 types of root on linux system
1. root account: root is an account or a username on linux machine and it is the most powerful account which has access to all commands and files 
2. Root as /: the very firat directory in the linux file system is called root and it is represented by a forward slash (/). all other directories and files are organized under this root directory.
3. Root home directyory: the root user account also has a directory located in /root which is called root home directory.

------------------------------------------------------------------------------------
### 03. Introduction to Filesystem
------------------------------------------------------------------------------------
* it is a system used by an operating system to manage files. the system controls how data is saved or retrieved from storage devices. without a file system, data would be stored in a large block with no way to tell where one piece of data ends and the next begins. by organizing data into files and directories, file systems make it easy to find and access the data you need.
* Operating system stores files and directories in an oraganized and structured way
  - systemconfirguration file = Folder A
  - User files = Folder B
  - Log files = Folder C
  - Commands or Scripts = Folder D and so on
* There are many diffrent types of filesystemms, i general, improvements have been made to filesystem with new releases of operating system and each new filesystem has been given a diffrent name 
  - ext4, xfs, btrfs, zfs, ntfs, fat32 and so on


* **File System Structure and its Description** 
  - /boot               Contains file that is used by the boot loader(grub.cfg) to boot the system
  - /root               root user home directory. it is not same as /
  - /dev                System devices (e.g. disk, cdrom, speakers, flashdrive, keyboard etc.)
  - /etc                Configuration files
  - /bin  -> /usr/bin   Everday user commands (e.g. ls, cp, mv, rm, cat etc.)
  - /sbin -> /usr/sbin  Syatem/filesystem commands
  - /opt                Optional add-on applications (not part of OS apps)
  - /proc               running process (only exit in memory)
  - /lib  -> /usr/lib   System libraries (e.g. libc.so, libm.so etc.)
  - /tmp                Directory for temporary files needed by commands and apps
                      strace -e open pwd
  - /home               Directory for users
  - /var                Syatem logs
  - /run                Statem daemons that start very early (e g systemd, udev etc.) to store temproray runtime files like PID files.
  - /mnt                To mount extrnal filesystem (e. g NFS, SMB etc.)
  - /media              For cdrom mounts

* NAVIGATING FILE SYSTEM
* when navigating a UNIX filesystem. there are a few important commands.
  - "cd"
  - "pwd"
  - "ls"
  - "ls -l"

* CD stand for change directory, it is the primary command for moving you around the filesystem.
* pwd stand for print working directory, it tells yoy where you current location is .
* ls stand for list it list all the directiries/files with a current working directory  2


* **Linux file or Directory Properties**
  - Each file or directory in linux has detail information or properties


| type        | of links | owner  | size    | month   |  Day  | time  | name  |
|-------------|----------|--------|---------|---------|-------|-------|-------|
| drwxr-xr-x  |  21      | root   | 4096    |  feb    | 27    | 13:33 | var   |
| lrwxrwxrwx. |  1       | root   | 7       |  feb    | 27    | 13:33 | lib   |
|-rw-r--r--. v|  1       | root   | 0       |  feb    | 27    | 13:33 | file1 |


* anything starting with d is a directory, - is a file and l is a symbolic link
* anything starting with l is link, its link with the file or directory it is pointing to, and it is not a real file or directory. it is just a pointer to the file or directory it is linked to. if you delete the link, the original file or directory will still be there. but if you delete the original file or directory, the link will be broken and will not work anymore.
* LS -L


* **FILE SYSTEM PATHS**
* There are two paths to navigate to a filesystem.
  - absolute Path
  - relative Path

* An absolute path always begans with a "/" this indicates that the path starts at the root directory and example of an absolute path is 
  - /home/user1/Documents/file1.txt
  - cd /var/log/samba

* A relative path does not start with a "/" and it is relative to the current working directory. example of a relative path is
  - Documents/file1.txt
  - cd /var
  - cd log

* **Creating Files and Directories**
* Creating files
  - Touch
  - cp
  - vi

* **Creating directories**
  - mkdir

* **Copying Directories**
* Command to copy directory
  - cp
* To copy a directory on Linux, you have to execute the "cp" command with the "-R" option for recursive and specify the source destination directories to be copied
  - cp -R <source_folder> <destination_folder>

* **Find Files and Directories** 
- Two main commands are used to fine files and directories on linux system

* 1. find
  - find . -name "file1.txt"
  - find /home/user1/Documents -name "file1.txt"
  - find / -name "ipcfg.enp0s3"

* 2. locate
  - locate file1.txt

* Locate uses a prebuilt database, which should be reqularly updated using the "updatedb" command. while find iterates over a filesystem to locate files. Thus, locate is much faster than find, but can be inaccurate if the database (can be seen as a cache) is not updated.

* **Linux File Types**


| File Symbol    |       Meaning               |                                        |
|----------------|-----------------------------|----------------------------------------|
|      -         | Regular file                | Text, Executable, images, videos, etc. |
|      d         | Directory                   |                                        |
|      l         | Symbolic link               |                                        |
|      c         | Special file or device file | device file hardware device keyboard                                        |
|      p         | Named pipe (FIFO)           |                                        |
|      b         | Block device file           |                                        |
|      s         | Socket file                 |     network shocket                                   |

 

* **File Permissions**
* UNIX is a multi-user system. every file and directory in your account can be protected from or made accessible to other users by changing its access permissions.
Every user has responcebility for controlling access to their files.

* Permissions for a file or directory may be restricted to by types.
* There are 3 type of permissions
  - r -read
  - w -write
  - x -execute = running a program or script

* Each permission (rwx) can be controlled at three levels.
  - u - user= yourself
  - g - group = can be people in the same project or department
  - o - other = everyone else

* File or Directory permission can be displayed by running ls -l command.
  - rwxrwxrwx

* Command to change permission.
  - chmod
  - man chmod = to check how to use chmod command
    - chmod g-w file1.txt = to remove write permission for group
  - chmod o+x file1.txt = to add execute permission for other
  - chmod a-r file1.txt = to remove read permission for all users
  - chmod u+x file1.txt = to add execute permission for user


* **Permission using Numeric mode**
* Permission to a file and directory can also be assigned numerically using chmod command. in numeric mode, each permission is represented by a number.
  - chmod ugo+r FILE
or
  - chmod 444 FILE

* The table below assigan numbers to permission type


| Number          | Permission type                    | Symbol      |
|-----------------|------------------------------------|-------------|
| 0               | No permission                      | ---         |
| 1               | Execute permission                 | --x         |
| 2               | Write permission                   | -w-         |
| 3               | Write and execute permission       | -wx         |
| 4               | Read permission                    | r--         |
| 5               | Read and execute permission        | r-x         |
| 6               | Read and write permission          | rw-         |
| 7               | Read, write and execute permission | rwx         |

------------------------------------------------------------------------------------
### 04. File Ownership
------------------------------------------------------------------------------------
* There are 2 owners of a file or directory
  - user and group

* Command to change file ownership
  - chown and chgrp
  - chown changes the ownership of a file or directory to a user and group
  - chgrp changes the group ownership of a file or directory to a group

* Recursive ownership change option (Cascade)
  - -R

### 05. WildCards (*,?,^,[])
* A wildcard is a character that can be used as a substitute for any of a class of characters in a search 
  - *  -represents zero or more characters
  - ?  -represents a single character
  - ^  -represents a range of characters
  - [] -represents a set of characters

  - rm abc*
  - touch abcd{1..9}-xyz
  - ls -l abc*

  - ls -l ?bcd*
  - ls -l *[cd]*
------------------------------------------------------------------------------------
### 06. Access Control List (ACL)
------------------------------------------------------------------------------------
* **what is ACL?**
  - Access control list (ACL) provides an additional, more flexble permission mechanism for file system. it is designed to assist with UNIX file permissions. ACL allows you to give permissions for any user or group to any disc resource.

* **Use of ACL**
  - Think of a scenario in which a particular user is not a member of group created by you but still you want to give some read or write access, how can you do it without making user a member of group, here comes in picture access control list, ACL helps us to do this trick
  - Basically, ACL are used to make a flexible permission mechansim in linux.
  - From linux man pages, ACL are used to define more fine-grained discretionary access rights for files and directories than the standard UNIX permissions.
  - Commands to assigan and remove ACL permissions
  - setfacl and getfacl
  - setfacl is used to set ACL permissions for a file or directory
  - getfacl is used to display ACL permissions for a file or directory

* **List of commands for setting up ACL:**
  - setfacl -m u:user1:rwx file1.txt = to give user1 read, write and execute permission for file1.txt
  - setfacl -m g:group1:rx file1.txt = to give group1 read and execute permission for file1.txt
  - setfacl -m o::r file1.txt = to give other read permission for file1.txt
  - setfacl -m u:user1:rw file1.txt = to give user1 read and write permission for file1.txt
  - setfacl -x u:user1 file1.txt = to remove ACL permissions for user1 on file1.txt
  - getfacl file1.txt = to display ACL permissions for file1.txt

------------------------------------------------------------------------------------
### 07. Help Commands
------------------------------------------------------------------------------------
* There are 3 types of help commands
  - whatis command
  - command --help
  - man command


* **TAB Completion and UP arrow**
* Hitting TAB key completes the available commands, files or directories.
  - chm TAB
  - ls j<TAB>
  - cd Des<TAB>

* Hitting UP arrow key allows you to scroll through the command history and execute previous commands without retyping them.

------------------------------------------------------------------------------------
### 08. Adding Text to Files(Redirection)
------------------------------------------------------------------------------------
* 3 Simple ways to add text to a file
  - vi 
  - redirect command output > or >>

  - echo > or >>
  - echo "this line first line" > file1.txt = to add text to a file, if the file already exists, it will overwrite the existing content of the file
  - echo "this line second line" >> file1.txt = to add text to a file

------------------------------------------------------------------------------------
### 09. PIPEs |
------------------------------------------------------------------------------------
* A pipe is used by the shell to connect the output of one command directly to the input of another command.
* the symbol for a pipe is the vertical bar (|) the command syntax is as follows
  - command1 | command2

  - ls -ltr | more = to display the output of ls -ltr command one page at a time 

------------------------------------------------------------------------------------
### 10. FILE MAINTENANCE COMMANDS
------------------------------------------------------------------------------------
  - cp
  - rm
  - mv
  - mkdir
  - rmdir or rm -r
  - chgrp
  - chown

* **File Display Commands**
  - cat
  - more
  - less
  - head
  - tail 

  - more file.txt
  - less file.txt 
  - head -2 file.txt = to display the first 2 lines of a file
  - tail -2 file.txt = to display the last 2 lines of a file

------------------------------------------------------------------------------------
### 11. File / Text processors Commands
------------------------------------------------------------------------------------
  - cut
  - awk
  - grep and egrep
  - sort
  - uniq
  - wd

------------------------------------------------------------------------------------
### 12. grep/egrep - Text Processors Commands
------------------------------------------------------------------------------------
* What is grep ?
  - The grep command which stands for "global regular expression print", process text line by line and prints any lines which match a specified pattern. it is used to search for specific patterns in files or output of other commands.

  - grep --version or grep --help = Check version or Help

  - grep file.txt             = to search for a pattern in a file
  - grep file.txt /etc/passwd = to search for a pattern in a file
  - grep -i file.txt          = to search for a pattern in a file, ignoring case
  - grep -c file.txt          = to count the number of lines that match a pattern in a file
  - grep -n file.txt          = to display the line number of each line that matches a pattern
  - grep -v file.txt          = to display lines that do not match a pattern in a file
  - grep -r file.txt          = to search for a pattern recursively in a directory and its subdirectories
  - grep -E file.txt          = to use extended regular expressions in the search pattern
  - ls -l | grep file.txt     = to search for a pattern in the output of another command
  - ls -l | grep -i file.txt  = to search for a pattern in the output of another command, ignoring case
  - egrep -i "file.txt"|"file2.txt name = to search for multiple patterns in a file, ignoring case

------------------------------------------------------------------------------------
### 13. sort/unip - Text Processors Commands
------------------------------------------------------------------------------------
* What are sort and unip commands?

  - Sort command sorts in alphabetical order
  - The sort command is used to sort lines of text files in a specified order. it can sort in ascending or descending order, and it can also sort based on specific fields or columns in the text file.

  - Uniq command filters out the repeated or duplicate lines
  - The uniq command is used to filter out duplicate lines from a sorted text file. it can be used in conjunction with the sort command to remove duplicate lines from a file or to count the number of occurrences of each unique line.

  - sort --version OR sort --help = Check version or Help
  - sort file.txt = to sort the lines of a text file in ascending order
  - sort -r file.txt = to sort the lines of a text file in descending order
  - sort -k2 file.txt = to sort the lines of a text file based on the second field or column
  - sort -u file.txt = to sort the lines of a text file and remove duplicate lines

  - uniq file.txt = to filter out duplicate lines from a sorted text file

------------------------------------------------------------------------------------
### 14. Compare Files (diff and cmp)
------------------------------------------------------------------------------------

- diff command compares two files line by line and displays the differences between them. it is used to identify changes or differences between two versions of a file.

- diff file.txt file2.txt = to compare two files and display the differences between them
- diff -u file.txt file2.txt = to compare two files and display the differences in a unified format
- diff -c file.txt file2.txt = to compare two files and display the differences in a context format
- diff -i file.txt file2.txt = to compare two files and ignore case differences


* **Compress and un-Compress Files**
- tar 
- gzip
- gunzip

- tar cvf iafzal.tar file1.txt file2.txt = to create a tar archive of multiple files
- tar cvf iafzal.tar . = to create a tar archive of a directory and its contents

------------------------------------------------------------------------------------
### 15. DIffrence Between vi and vim Editors
------------------------------------------------------------------------------------
As far as funcctionality is concerned, there is no difference between vi and vim editors. vim is an improved version of vi editor, it has more features and capabilities than vi editor. vim stands for "Vi IMproved" and it is a more powerful and feature-rich version of the original vi editor. vim includes additional features such as syntax highlighting, multiple undo levels, and support for plugins and extensions.

------------------------------------------------------------------------------------
### 16. User Account Management
------------------------------------------------------------------------------------
* Commands for user account management
  - useradd
  - groupadd
  - usermod
  - userdel
  - groupdel


* Files
  - /etc/passwd
  - /etc/shadow
  - /etc/group

* Example:
  - useradd -g superheros -s /bin/bash -c "user description" -m -d /home/spiderman spiderman

  - useradd username     = to create a user account with default settings
  - id username          = to check the user account details
  - groupadd groupname   = to create a group called superheros
  - cat /etc/group       = to check the group file and see the group you created
  - userdel -r username  = to delete a user account and its home directory
  - groupdel groupname   = to delete a group
  - usermod -G groupname username = to add a user to a group
  - grep username /etc/group      = to check if a user is a member of a group
  - chgrp -R groupname username   = to change the group ownership of a user's home directory and its contents to a group

------------------------------------------------------------------------------------
### 17. Enable password aging
------------------------------------------------------------------------------------
* chage -M 30 username = to set the maximum number of days a password is valid to 30 days for a user account
* chage -l username = to check the password aging information for a user account

------------------------------------------------------------------------------------
### 18. Linux Account Authentication
------------------------------------------------------------------------------------
* Linux account authentication is the process of verifying the identity of a user who is trying to access

* types of authentication
  - local authentication
  - Domain/ Directory account authentication

* Active Directory = Microsoft 
* IDM = Identity Management = Linux
* WinBIND = Used in Linux to communicate with windows active directory(same as samba)
* OpenLDAP = (Open Source Lightweight Directory Access Protocol)
* IBM Directory Server = (IBM's implementation of LDAP)
* LDAP = Lightweight Directory Access Protocol

------------------------------------------------------------------------------------
### 19. System Utility Commands
------------------------------------------------------------------------------------
* date     = to display or set the system date and time
* uptime   = to display how long the system has been running and the current load average
* hostname = to display or set the system's hostname
* uname    = to display system information such as the kernel version, architecture, and operating system
* which    = to locate the executable file for a command
* cal      = to display a calendar for a specific month or year
* bc       = to perform basic arithmetic calculations from the command line

------------------------------------------------------------------------------------
### 20. Processes and Jobs
------------------------------------------------------------------------------------
* A process is an instance of a running program. it is an executing instance of a program that can be managed and controlled by the operating system. each process has its own unique process ID (PID) and can be in different states such as running, sleeping, or stopped.

* Application = a program that is designed to perform a specific task or set of tasks for the user. 
* Script = a file that contains a series of commands that can be executed by the shell. 
* Process = an instance of a running program or script that is being executed by the operating system.
Daemon = a background process that runs continuously and performs specific tasks or services for the system or other applications.
* Threads = a thread is a lightweight process that can run concurrently with other threads within the same process. 
* job = a job is a process that is running in the background or foreground and can be managed using job control commands.

------------------------------------------------------------------------------------
### 21. systemctl command
------------------------------------------------------------------------------------
* systemctl is a command-line utility used to control and manage the systemd system and service manager in Linux. it is used to start, stop, restart, enable, disable, and check the status of services and daemons on a Linux system.
* Syatemctl command is a new tool to control system services.

* usage example:
  - systemctl start|stop|status
  - systemctl status firewalld.service
  - systemctl enable|disable service_name
  - systemctl restart| reload servicename.service
  - systemctl list-units --all

* To add a service under systemctl management:
  - Create a unit file in /etc/systemd/system/servicename.service
  - To control system with systemctl
  - systemctl poweroff
  - systemctl halt
  - systemctl reboot

------------------------------------------------------------------------------------
### 22. ps command
------------------------------------------------------------------------------------
* ps command stands for process status and it display all the currently running processes in the Linux system

* Usage Examples
- ps = shows the processes of the current shell

  - PID  = the unique process ID
  - TTY  = terminal type that the user logged-in to
  - TIME = amount of CPU in minutes nad seconds that the process has been running
  - CMD  = name of the command

  - ps -e          = shows all running processes in the system
  - ps aux         = shows all running processes in BSD format
  - ps -ef         = shows all running processes in standard format
  - ps -u username = shows all running processes for a specific user

------------------------------------------------------------------------------------
### 23. top command
------------------------------------------------------------------------------------
* top command is used to show the linux processes and it provides a real-time view of the running system.
* This command shows the summary information of the system and the list of processes or threads which are currently managed by the Linux Kernel.
* When the top command is executed then it goes into interactive mode and you can exit out by hitting **"q"** key.

* **Usage : top**

- PID:     Shows the task's unique process id
- USER:    Shows the user name of the task's owner
- PR:      Shows the priority of the task
- NI:      Shows the nice value of the task
- VIRT:    Shows the virtual memory used by the task
- RES:     Shows the resident memory used by the task
- SHR:     Shows the shared memory used by the task
- S:       Shows the status of the task (e.g. R for running, S for sleeping, Z for zombie)
- %CPU:    Shows the percentage of CPU used by the task
- %MEM:    Shows the percentage of memory used by the task
- TIME+:   Shows the total CPU time used by the task
- COMMAND: Shows the command that started the task


- top -u username   = to display processes for a specific user
- top then press c  = to display the full command line of each process
- top then press k  = to kill a process by entering its PID
- top then press r  = to renice a process by entering its PID and new priority
- top then M and P  = to sort processes by memory or CPU usage

------------------------------------------------------------------------------------
### 24. Kill command
------------------------------------------------------------------------------------
* kill command is used to terminate process manually
* it sends a signal which ultimately terminates or kills a particular process or group of processes.

- Usage:
- kill [options] <pid> = to send a signal to a process with a specific PID
- kill -l              = to list all available signals
- kill PID             = to send the default signal (SIGTERM) to a process with a specific PID
- kill -1              = restart
- kill -2              = interrupt just like keyboard Ctrl C
- kill -9              = to forcefully kill a process with a specific PID
- kill -15             = to gracefully terminate a process with a specific PID

------------------------------------------------------------------------------------
### 25. Process Signals in Linux
------------------------------------------------------------------------------------
* Process: Running Program in Computer.
- it is an instance of a program that is being executed by the operating system. each process has its own unique process ID (PID) and can be in different states such as running, sleeping, or stopped.

* Signals: Short Message Sends To Process 
  - Interrupt
  - Control
  - Communicate

* Process Signal: Send Signals to Running Processes
  - Control Behavior of Process

------------------------------------------------------------------------------------
### 26. Crontab Command
------------------------------------------------------------------------------------
* Crontab command is used to schedule tasks to run automatically at specified intervals. it is commonly used for automating system maintenance or administration tasks, such as backups, updates, and monitoring.

* Usage:
  - crontab -e = to edit the crontab file for the current user
  - crontab -l = to list the current user's crontab entries
  - crontab -r = to remove the current user's crontab entries
  - crond      = to start the cron daemon, which is responsible for executing scheduled tasks
  - systemctl status crond = to manage the crond service using systemctl


  - * * * * * <command to execute> = to schedule a task to run every minute
  - 0 0 * * * <command to execute> = to schedule a task to run every day at midnight
  - 0 0 * * 0 <command to execute> = to schedule a task to run every Sunday at midnight
  - 0 0 1 * * <command to execute> = to schedule a task to run on the first day of every month at midnight
  - 0 0 1 1 * <command to execute> = to schedule a task to run on the first day of every year at midnight

  - 1st *  = minute (0-59)
  - 2nd *  = hour (0-23)
  - 3rd *  = day of month (1-31)
  - 4th *  = month (1-12)
  - 5th *  = day of week (0-7) (Sunday is both 0 and 7)

* Create crontab entry by scheduling a task:
  - crontab -e
  - schedule, echo "this is my first crontab entry" > crontab-entry

```
Creating another crontab entry:
crontab -e
enter: 21 16 * 10 * echo "this is my second crontab entry" > crontab-entry2
:wq! = to save and exit the crontab file

```
* By default there are 4 types of cronjobs
  - Hourly
  - Daily
  - Weekly
  - Monthly

* All the above crons are setup in 
  - ./etc/cron.___ (directory)

* The timing for each are set in
  - ./etc/anacrontab --

* for hourly
  - ./etc/cron.d/0hourly

  - ls -l cron.*
  - ls -l | grep cron

  - if you want add your script to run hourly
  - cd cron.hourly
  - cp /path/to/your/script.sh . = to copy your script to the cron.hour

------------------------------------------------------------------------------------
### 27. at Command
------------------------------------------------------------------------------------
* at command is used to schedule a one-time task to run at a specific time in the future. it is commonly used for scheduling tasks that need to be executed only once, such as sending an email or running a script at a specific time.
* When the command is run it will enter interactive mode and you can get out by pressing Ctrl D

* Usage:
  - at HH:MM PM  = to schedule a task to run at a specific time in the future
  - atq          = to list the pending at jobs
  - atrm #       = to remove a pending at job with a specific job number
  - atd          = to start the at daemon, which is responsible for executing scheduled at jobs
  - systemctl status atd = to manage the atd service using systemctl

* Create at entery by scheduling a task:
  - at 4:30 PM
  - enter: echo "this is my first at entry" > at-entry
  - Ctrl D = to save and exit the at command

------------------------------------------------------------------------------------
### 28. Log Monitoring
------------------------------------------------------------------------------------
* Linux system logs are stored in the /var/log directory. these logs contain information about system events, errors, and other important information that can be used for troubleshooting and monitoring the system.

  - Log Directory: /var/log
  - boot
  - chronyd = NTP
  - cron
  - maillog
  - messages
  - secure
  - syslog
  - httpd = web server logs
  - samba = samba server logs