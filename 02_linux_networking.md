This document is an introduction to Linux networking and remote connectivity. It focuses on how Linux machines communicate with each other over a network and how to manage network services securely.

* *Main topics covered*
    - []()

#### Client & Server Relationship
- **Client:** A client is a computer or a program that, as part of its operation, relies on sending a request to another program or a computer hardware or software that accesses a service made available by a server.

- **Server:** Server is a piece of computer hardware or software that provides functionality for other program or devices, called clients.


#### Network Components
- **IP Address:** An IP address is a unique string of numbers separated by periods that identifies each computer using the Internet Protocol to communicate over a network.
- **Subnet Mask:** A subnet mask is a 32-bit number that divides an IP address into network and host parts. It is used to determine which portion of the IP address identifies the network and which portion identifies the host.
- **Default Gateway:** A default gateway is a node in a computer network that serves as an access point to another network, often the Internet. It is used to route traffic from a local network to other networks or the Internet.
- **DNS Server:** A DNS server is a server that translates domain names (like www.example.com) into IP addresses
- **Static vs DHCP IP Addressing:** Static IP addressing is when a device is manually assigned a specific IP address, 
- while DHCP (Dynamic Host Configuration Protocol) automatically assigns IP addresses to devices on a network.
- interface: An interface is a point of interaction between two systems, such as a network interface that connects a computer to a network.

#### Network Files and Commands
* Interface Detection
* Assigning an IP address to an interface

* **Interface configuration files**
    - /etc/nsswitch.conf     = where it should reslove hostname to IP address
    - /etc/hostname          = hostname of the system
    - /etc/hosts             = static hostname to IP address mapping
    - /etc/sysconfig/network = network configuration file
    - /etc/sysconfig/network-scripts/ifcfg-eth0 = network interface configuration file
    - /etc/resolv.conf       = DNS configuration file


#### Network Commands
* ping              = test connectivity to another host
* ifconfig or ip a  = show network interfaces and their IP addresses
* ifup or ifdown    = bring a network interface up or down
* netstat   -rnv    = show routing table
* tcpdump           = capture network traffic
* traceroute        = show the path packets take to reach a destination
* nslookup          = query DNS servers for information about domain names


#### NIC information 
* Network interface card (NIC)
* ethtool enp0s3 

* other NICs
    - lo    = The loopback device is a special interface that your computer uses to communicate with itself. It is used mainly for diagnostics and troubleshooting, and to connect to servers running on the local machine.
    - virb0 = The virbr0, or "Virtual Bridge 0" interface is used for NAT (Network Address Translation). Virtual environments sometimes use it to connect to the outsice network.



#### NIC Bonding
* NIC = Network Interface Card
    - NIC (Network Interface Card) bonding is also known ad Network bonding. it can be defined ad the aggregation or combination of multiple NIC into a single bond interface.
    - The main purpose of NIC bonding is to provide increased bandwidth and redundancy for network connections. By bonding multiple NICs together, you can achieve higher data transfer rates and ensure that if one NIC fails, the others can continue to provide network connectivity.
    - it's main purpose is to provide high availability and redundancy.

    - modprobe bonding
    - modinfo bonding

    - create vi /etc/sysconfig/network-scripts/ifcfg-bond0
    - Edit   /etc/sysconfig/network-scripts/ethernet1
    - Edit   /etc/sysconfig/network-scripts/ethernet2

- nic1 -----
             ----- bond0
- nic2 -----


    - restart network: systemctl restart network

#### NIC Teaming
* Combining two or more network interfaces into a single logical interface to provide increased bandwidth and redundancy. It is similar to NIC bonding but offers more flexibility and features.
* NIC teaming is a newer and more flexible way of aggregating network interfaces in Linux. It was introduced as a replacement/alternative to bonding.

    - Broadcast = data transmitted over all ports
    - round-robin = data transmitted sequentially over all ports
    - active-backup = only one port is active at a time, if the active port fails, another port takes over
    - load-balance = data transmitted based on the current load of each port
    - lacp = Link Aggregation Control Protocol, a standardized protocol for dynamic link aggregation

    - rpm -qa| grep teamd
    - dnf install teamd
    - nmcli = network manager command line interface
    - addr show = to check network interfaces and their IP addresses

* **teaming Process**
    - nmcli connection show            = to check network connections and fidn the UUID of the connection you want to delete
    - nmcli connection delete UUID     = to delete a network connection
    - nmcli device status              = to check the status of network devices
    
* **teaming Creation**    
    - nmcli connection add type team con-name team0 ifname team0 config '{"runner": {"name": "activebackup"}}' = to create a team connection with active-backup runner
    - nmcli connection show team0      = to check the team connection
    - nmcli connection modify team0 ipv4.addresses 192.168.0.111/24 = to assign an IP address to the team connection
    - nmcli connection modify team0 ipv4.gateway 192.168.0.1 = to assign a gateway to the team connection
    - nmcli connection modify team0 ipv4.dns 192.168.0.1 = to assign a DNS server to the team connection
    - nmcli connection modify team0 ipv4.method manual = to set the IP method to manual
    - nmcli connection modify team0 ipv4.autoconnect yes    = to set the team connection to autoconnect
    - nmcli connection add type team-slave con-name team0-port0 ifname enp0s3 master team0 = to add a slave connection to the team connection
    - nmcli connection add type team-slave con-name team0-port1 ifname enp0s8 master team0 = to add another slave connection to the team connection
    - nmcli connection down team0  = to bring the team connection down
    - nmcli connection up team0 =  to bring the team connection up
    - teamdctl team0 state = to check the state of the team connection


#### SSH and Telnet
* Telnet: Un-secured Connection between computers, it sends data in plain text, which can be intercepted by attackers. It is not recommended for use over the internet or in secure environments.

* SSH (Secure Shell): A secure protocol for remote access to computers. It encrypts data transmitted between the client and server, making it more secure than Telnet. It is widely used for remote administration and secure file transfers.

* SSH stands for secure shell:
    - Provides you with an interface to the linux system. it takes in your commands and translate them to kernel to manage hardware and software resources of the system.

* runs on port # 22


* Two type of packages for most of the services:
    - Server package: This package contains the software that runs on the server and provides the service to

    - Client package: This package contains the software that runs on the client and allows it to connect to the server and use the service provided by the server.


* To check ssh 
    - systemctl status sshd
    - ps -ef | grep sshd
    - systemctl stop sshd
    - systemctl start sshd
    - systemctl restart sshd


* Following are the most common configuration an administrator should take to secure SSH:
    - Configure idle Timeout Interval
    - Become root user to perform administrative tasks
    - Edit your /etc/ssh/sshd_config
    - **ClientAliveInterval** 600
    - **ClientAliveCountMax** 0
    - **# systemctl restart sshd**

* Disble root login
    - Disabling root login should be one of the measures you should take when setting up the system for the first time.
    - it disable any user to login to the system with root account.
    - Edit /etc/ssh/sshd_config
    - **PermitRootLogin no**
    - **# systemctl restart sshd**

* Disble Empty passwords
    - Disabling empty passwords is another important measure to secure your system.
    - it prevent any user from logging in to the system with an empty password.
    - Edit /etc/ssh/sshd_config
    - **PermitEmptyPasswords no**
    - **# systemctl restart sshd**

* Limit Users' SSH Access
    - Limiting users' SSH access is another important measure to secure your system.
    - it allows you to specify which users are allowed to login to the system via SSH.
    - Edit /etc/ssh/sshd_config
    - **AllowUsers user1 user2**
    - **# systemctl restart sshd**


#### Access Remote Server without Password (SSH-Keys)
* Two reasons to access a remote machine without password:
    - Repetitive logins
    - Automation through scripts

* Keys are generated at user level
    - user1
    - root

* if you want connect client linux vm to server linux vm without password, you need to generate the keys on the **client linux** vm and copy the public key to the **server linux** vm.
    - ssh-keygen -t rsa -b 2048 = to generate a pair of keys (private and public) on the client linux vm
    - ssh-copy-id user1@192.168.1.1 = to copy the public key to the server linux vm


#### curl and ping Commands

* Linux = curl -I www.google.com
* Windows = curl -I www.google.com

* curl http://www.google.com = to check the response from the server
* curl -O www.google.com     = to download the file from the server 
* ping www.google.com = to check the connectivity to the server




#### FTP (File Transfer Protocol)
* The FIle Transport Protocol is a standard network protocol used for the transfer of computer files between a client and server on a computer network. FTP is built on a client-server model architecture using separate control and data connections between the client and the server.

* Protocol = Set of rules used by computers to communicate with each other over a network.
* Default FTP Port - 21
* For this lecture we need 2 linux machines

* For this lecture we need 2 linux machines.
    - Linux VM1 = FTP Server
    - Linux VM2 = FTP Client

* Install and configure FTP on the remote server
    - become root
    - rpm -qa | grep ftp = to check if the FTP server package is installed
    - yum install vsftpd = to install the FTP server package
    - vi /etc/vsftpd/vsftpd.conf = to edit the FTP server configuration file

* Find the follwoing lines and make the changes ad shown below:
    - anonymous_enable=NO
    - local_enable=YES
    - write_enable=YES

* Uncomment
    - ascii_upload_enable=YES
    - ascii_download_enable=YES

* Uncomment Enter your welocme message - This is optional
    - ftpd_banner=Welcome to the FTP server

    - systemctl start vsftpd = to start the FTP server
    - systemctl enable vsftpd = to enable the FTP server to start on boot
    - systemctl status vsftpd = to check the status of the FTP server
    - systemctl disable vsftpd = to disable the FTP server from starting on boot
    - systemctl stop vsftpd = to stop the FTP server


#### SCP -Secure copy Protocol 
* SCP (Secure Copy Protocol) is a network protocol that supports file transfers between hosts on a network. It is based on the SSH protocol and provides a secure way to transfer files between a local host and a remote host or between two remote hosts.

* Protocol - set of rules used by computers to communicate with each other over a network
* Default SCP Prot - 22 (Same as SSH)

#### Download Files or Apps
* To download files or apps from the internet, you can use the following commands:
    - curl -O http://example.com/file.tar.gz = to download a file from the internet
    - wget http://example.com/file.tar.gz = to download a file from the internet
    - dnf install package-name = to install a package from the internet


#### System Updates and Repos
* dnf  = Dandified YUM, is a package manager for RPM-based Linux distributions. It is used to install, update, and remove packages on the system.
    - repositories location = /etc/yum.repos.d/

* apt-get = is a package manager for Debian-based Linux distributions. It is used to install, update, and remove packages on the system.

* rpm = Red Hat Package Manager, is a package manager for RPM-based Linux distributions. It is used to install, update, and remove packages on the system. It is also used to query the package database and to verify the integrity of packages.

* dnf and rpm diffrences: 
    - dnf is a higher-level package manager that uses rpm as its backend. It provides a more user-friendly interface and additional features such as automatic dependency resolution and support for multiple repositories. 
    - On the other hand, rpm is a lower-level package manager that is used to manage individual packages and does not provide the same level of functionality as dnf.



#### System Upgrade / Patch Management 

* Types of upgrades
    - Major Upgrade: A major upgrade is a significant update to the operating system that includes new features, improvements, and bug fixes. It may also include changes to the user interface and may require a complete reinstallation of the operating system.

    - Minor Upgrade: A minor upgrade is a smaller update that includes bug fixes and security patches. It may also include minor improvements and new features, but it does not require a complete reinstallation of the operating system.

    - Security Patch: A security patch is an update that addresses vulnerabilities in the operating system. It is designed to protect the system from potential security threats and should be applied as soon as possible to ensure the security of the system.

* Major Version = can not done with dnf command
* Minor Version = can be done with dnf command
    - dnf update = to update the system with the latest packages and security patches
    - dnf update -y 
    - dnf upgrade = to upgrade the system with the latest packages and security patches

* Update vs. Upgrade
    - Upgrade = delete packages and install new ones
    - Update = only update the existing packages without deleting them 



#### Roolback Updates and Patches
* Rollback updates and patches is the process of reverting to a previous version of the operating system or software after an update or patch has been applied. This can be necessary if the update or patch causes issues or if it is not compatible with the system.

* Roleback a package or path
    - yum install <package-name>
    - yum history undo <id>

* Rollback an update
    - Downgrading a system to minor versions (ex. RHEL7.1 to RHEL7.0) is not recommended as this might leave thr system in undisired or unstable state.




