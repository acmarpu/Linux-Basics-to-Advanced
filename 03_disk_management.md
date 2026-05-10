#### Computer Storage
* Local storage: Hard disk drive (HDD), solid state drive (SSD), RAM disk, optical drive (CD/DVD), flash drive (USB)

* DAS (Direct Attached Storage): Storage directly attached to a computer, such as an internal hard drive or an external USB drive.

* SAN (Storage Area Network): A high-speed network that provides access to block-level storage, allowing multiple servers to access shared storage resources.

* NAS (Network Attached Storage): A file-level storage device connected to a network, allowing multiple users and devices to access and share files.


#### Disk Partition
* A disk partition is a logical division of a physical disk into separate sections, allowing for better organization and management of data.

* Commands for disk partition
    - df    = disk free, shows the amount of disk space used and available on the file system
    - df -h = human-readable format
    - fdisk = a command-line utility for managing disk partitions, allowing you to create, delete, and modify partitions on a disk

#### Adding Disk and Creating Partition
* Purpose? = Out of Space, Additional Apps etc.
* Commands for disk partition
    - df  
    - fdisk 
    - fdisk -l | more

    - fdisk /dev/sdb
        - n = new partition
        - p = primary partition
        - 1 = partition number
        - default = first sector
        - default = last sector (use entire disk)
        - w = write changes to disk
    
    - mkfs.ext4 /dev/sdb1 = format the new partition with the ext4 file system
    - mkdir /data = create a mount point for the new partition
    - mount /dev/sdb1 /data = mount the new partition to the /data directory
    - df -h = verify that the new partition is mounted and available for use

    - how can we makeit enable after reboot?
        - edit vi /etc/fstab and add the following line:
            /dev/sdb1   /data   ext4    defaults    0   2

#### Logocal Volume Management (LVM)
* LVM is a method of managing disk storage that allows for more flexible and efficient use of disk space. It provides features such as dynamic resizing, snapshots, and the ability to create logical volumes that can span multiple physical disks.

* Commands for LVM
    - pvcreate /dev/sdb = create a physical volume on the new disk
    - vgcreate myvg /dev/sdb = create a volume group named "myvg" using the physical volume
    - lvcreate -L 10G -n mylv myvg = create a logical volume named "mylv" with a size of 10GB in the "myvg" volume group
    - mkfs.ext4 /dev/myvg/mylv = format the logical volume with the ext4 file system
    - mkdir /data = create a mount point for the logical volume
    - mount /dev/myvg/mylv /data = mount the logical volume to the /data directory
    - df -h = verify that the logical volume is mounted and available for use


#### Add Disk and Create LVM Partition
* LVM Partition structure 
    - file system    = datafs
    - logical volume  = datalv
    - volume group    = datavg
    - Physical volume = /dev/sdb  /dev/sdb1
    - partition       = /dev/sdb  /dev/sdb1
    - Hard Disk       =  /dev/sdb  /dev/sdb

* Commands for LVM
    - df 
    - fdisk -l | more
    - fdisk /dev/sdb
        - n = new partition
        - p = primary partition
        - 1 = partition number
        - default = first sector
        - default = last sector (use entire disk)
        - w = write changes to disk
    
    - type to change the partition type to LVM (8e)
        - t = change partition type
        - 8e = Linux LVM
        - w = write changes to disk
    - pvcreate /dev/sdb1 = create a physical volume on the new partition
    - vgcreate datavg /dev/sdb1 = create a volume group named "datavg" using the physical volume
    - lvcreate -L 10G -n datalv datavg = create a logical volume named "datalv" with a size of 10GB in the "datavg" volume group
    - mkfs.ext4 /dev/datavg/datalv = format the logical volume with

#### ADD/Extend Swap Space
* Swap space in linux is used when the amount of physical memory(RAM) is full. if the system needs more memory resources and the RAM is full. inactive pages in memory are moved to the swap space. while swap space can help machines with a small amount of RAM, it should not be considered a replacement for more RAM. Swap space is located on hard drives, which have a slower access time than physical memory, so relying heavily on swap can lead to performance issues.

* MRecommended swap space size
    - M = Amount of RAM in GB and 
    - S = Amount of swap in GB, then
    - if M < 2GB, then S = 2 * M
    - if M >= 2GB and M < 8GB, then S = M

* df -h = check current swap space
* free -m = check current swap space in megabytes
* swapon -s = check current swap space in summary


#### File System Check (fsck and xfs_repair)
* Linux fsck utility is used to check and repair linux filesystems (ext2, ext3, ext4, etc)
* Linux xfs_repair utility is used to check and repair linux filesystem for xfs filesystem type
* Depending on when was the last time a files system was checked, the system runs the fsck during boot time to check whether the filesystem is in consistent state.
* System administrator could also run it manually when there is a problem with the filesystem.
* Make sure to execute the fsck on an unmount file system to avoid any data corruption issues.
* force a filesystem check even if its clean using option -f
* attempt to fix dected probleams automaticall using option -y
* The xfs_repair utility is highly scalable and is designed to repair even very large file systems with many inodes efficiently. Unlike other linux file system, xfs_repair does not run at boot time.
* The following are the possible exit codes for fsck command.
    - 0 = No errors
    - 1 = File system errors corrected
    - 2 = File system errors corrected, system should be rebooted
    - 4 = File system errors left uncorrected
    - 8 = Operational error
    - 16 = Usage or syntax error
    - 32 = Checking canceled by user request
    - 128 = Shared library error
* Commands for fsck
    - fsck /dev/sdb1 = check and repair the file system on the specified partition
    - fsck -f /dev/sdb1 = force a file system check even if it is marked as clean
    - fsck -y /dev/sdb1 = automatically answer "yes" to all prompts, allowing fsck to fix any detected problems without user intervention


#### Network file system (NFS)
* NFS stands for Network File System, a file system developed by Sun Microsystem, Inc.
* it is a client/server system that allows users to access files across a network and treat them as if they resided in a local file directory.
* NFS is commonly used in environments where multiple users need to access shared files, such as in enterprise settings, educational institutions, and data centers.
* NFS operates on a client-server model, where the server hosts the shared files and the


