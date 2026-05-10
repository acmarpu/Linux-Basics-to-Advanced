#### Basic Linux Commands
* ls = list files and directories
* cd = change directory
* whoami = display the current user
* pwd = print working directory, shows the current directory you are in
* ifconfig = display network configuration (Linux)
* To check = rpm -qa | grep module_name  = check if a specific module is installed (Linux)
* less = view the contents of a file one page at a time
* more = view the contents of a file one page at a time (similar to less)
* grep "search_term" file.txt = search for a specific term in a file and display the matching lines
* ping network.com = check network connectivity to a specific host
* top = display real-time system information, including CPU and memory usage
* cal = display a calendar
* date = display the current date and time
* free = display memory usage
* df = display disk space usage
* df -h = display disk space usage in a human-readable format
* history = display a list of previously executed commands

#### SSH Connect 
* ssh user1@192.168.1.10 

#### LS Commands
* ls = list files and directories
* ls -l = long listing format, shows detailed information about files and directories
* ls -a = show all files, including hidden files (those starting with a dot)
* ls -h = human-readable format, shows file sizes in a more readable format (e.g., KB, MB, GB)
* ls -al = combination of -a and -l, shows all files in long listing format

#### CD Commands
* cd = change directory
* cd .. = move up one directory level
* cd ~ = move to the home directory
* cd /path/to/directory = move to a specific directory
* pwd = print working directory, shows the current directory you are in

#### Touch Command
* touch filename = create an empty file with the specified name or update the timestamp of an existing
* touch line{1..3}.txt = create multiple files named line1.txt, line2.txt, line3.txt
* touch -d  "2024-01-01 12:00:00" filename = create a file with a specific timestamp

#### echo Command
* echo "Hello, World!" > file.txt = print the specified text to the terminal

#### cat Command
* cat file.txt = display the contents of a file
* cat file1.txt file2.txt > combined.txt = concatenate the contents of multiple files into

#### mkdir Command
* mkdir directory_name = create a new directory with the specified name
* mkdir -p parent_directory/child_directory = create a nested directory structure, creating parent directories as needed

#### copy and move Command
* cp source_file destination_file = copy a file from the source location to the destination location
* cp file.txt ./mynewdirectory/ = copy a file to a specific directory
* cp -r source_directory destination_directory = copy a directory and its contents recursively to the destination location

* mv file.txt ./mynewdirectory/ = move a file to a specific directory
* mv file.txt newfile.txt = rename a file
* mv file.txt ./mynewdirectory/ = move a file to a specific directory

* **Copy the file from loacal to another linux vm** 
* Data copy from vm1 to vm2, need to do run command from vm1 
* scp user1@192.168.122.52:~/anaconda.cfg  ~/Downloads

#### rm Command
* rm file.txt = remove a file
* rmdir directory_name = remove an empty directory
* rm -r directory_name = remove a directory and its contents recursively

#### how to find perameters in script 
- use / to search for the perameter in the script
- use n to find the next occurrence of the perameter in the script

#### User Creation
* useradd username = create a new user with the specified username
* passwd username = set a password for the specified user
* sudo adduser username = create a new user with the specified username and set a password (Ubuntu/Debian)

#### Installation and updates
* yum install package_name = install a package using the YUM package manager (Red Hat/CentOS)
* yum update package_name = update a package using the YUM package manager (Red Hat/CentOS)
* apt-get install package_name = install a package using the APT package manager (Ubuntu/Debian)
* apt-get update = update the package list using the APT package manager (Ubuntu/Debian)

#### man command
* man finger = display the manual page for the "finger" command, providing information about its usage and options
* man cat = display the manual page for the "cat" command, providing information about its usage and options
* man man = display the manual page for the "man" command itself, providing information about how to use the manual system in Linux

#### wget and curl Command
* curl http://example.com = fetch the content of the specified URL and display it in the
terminal
* curl -o file.txt http://example.com/file.txt = fetch the content of the specifiedURL and save it to a file named "file.txt"

* wget http://example.com/file.txt = download a file from the specified URL
* wget -O newfile.txt http://example.com/file.txt = download a file and save it with a specific name
* wget -r http://example.com/directory/ = download a directory and its contents recursively

#### zip
* zip archive.zip file1.txt file2.txt = create a zip archive named "archive.zip" containing the specified files
* unzip archive.zip = extract the contents of a zip archive

#### head and tail Command
* head -n 10 file.txt = display the first 10 lines of a file
* tail -n 10 file.txt = display the last 10 lines of a file
* tail -f file.txt = continuously monitor a file for new lines being added (useful for log files)

#### compare two files
* diff file1.txt file2.txt = compare the contents of two files and display the differences
* cmp file1.txt file2.txt = compare two files byte by byte and report if they are identical or not

#### sort
* sort file.txt = sort the lines of a file in alphabetical order
* sort -n file.txt = sort the lines of a file in numerical order

#### find
* find / -name "file.txt" = search for a file named "file.txt" starting from the root directory
* find /home/user -type f -name "*.txt" = search for all text files in the user's home directory

#### chmod and chown Command
* chmod 755 file.txt = set the permissions of a file to rwxr-xr-x (read, write, execute for owner; read and execute for group and others)
* chmod 644 file.txt = set the permissions of a file to rw-r--r-- (read and write for owner; read-only for group and others)
* chmod +x script.sh = add execute permission to a script file

* chown user1 file.txt = change the ownership of a file to a specific user
* chown user1:group1 file.txt = change the ownership of a file to a specific user and group

#### ifconfig Command
* ifconfig = display network configuration (Linux)
* ifconfig eth0 = display the configuration of a specific network interface (e.g., eth0)
* ifconfig eth0 up = bring a network interface up (activate it)
* ip address show = display detailed information about all network interfaces and their IP addresses (Linux)


#### grep Command
* ip address | grep eth0 = search for the term "eth0" in the output of the "ip address" command, which displays network interface information
* grep "search_term" file.txt = search for a specific term in a file and display
* ip address | grep eth0 | grep inet 

#### awk Command
* ip address | grep eth0 | grep inet | awk '{print $2}' = extract the IP address associated with the "eth0" network interface from the output of the "ip address" command
* awk '{print $1}' file.txt = print the first column of a file

#### ping and traceroute Command
* ping network.com = check network connectivity to a specific host
* ping -c 4 network.com = send a specific number of ping requests (e.g  4) to a host and then stop
* ping -i 5 network.com = send ping requests to a host at a specific interval
* ping -c 4 -i 5 network.com = send a specific number of ping requests at a specific interval

* traceroute network.com = trace the route packets take to reach a specific host, showing each hop along the way
* traceroute -n network.com = perform a traceroute without resolving hostnames, showing only IP addresses

#### netstat Command
* netstat = display network connections, routing tables, and interface statistics
* netstat -tuln = display active TCP and UDP connections without resolving hostnames
* ss -tuln = display active TCP and UDP connections without resolving hostnames (similar to netstat -tuln, but faster and more modern)

#### ufw allow Command
* ufw allow 80/tcp = allow incoming traffic on port 80 for TCP protocol
* ufw status = check the status of the firewall and see which rules are currently active
* ufw enable = enable the firewall

#### free command
* free -m = display memory usage in megabytes

#### Disk Management Commands
* df = display disk space usage
* df -h = display disk space usage in a human-readable format

#### process management ps
* ps = display information about active processes
* ps aux = display detailed information about all running processes
* ps -ef = display detailed information about all running processes (similar to ps aux, but with a different format)

#### top and htop Command
* top = display real-time system information, including CPU and memory usage
* top -u username = display processes for a specific user
* htop = an interactive process viewer that provides a more user-friendly interface than top, allowing for easier navigation and management of processes

#### kill Command
* ps -aux | grep process_name = find the process ID (PID) of a specific process
* kill PID = terminate a process using its PID
* kill -9 PID = forcefully terminate a process using its PID

* pkill process_name = terminate processes by name
* killall process_name = terminate all processes with the specified name

#### systemctl Command
* systemctl status service_name = check the status of a specific service
* systemctl start service_name = start a specific service


