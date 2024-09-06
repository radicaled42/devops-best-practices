# Useful Linux Commands

## Hardware Information

- dmesg: show bootup messages
- cat /proc/cpuinfo: show CPU information
- free -h: show free and used memory (-m flag indicates memory in MB)
- lshw: list information about hardware configuration
- lsblk: list information about block devices
- lspci -tv: show PCI devices in a tree-like diagram
- lsusb -tv: show USB devices in a tree-like diagram
- dmidecode: show hardware information from the BIOS
- hdparm -i /dev/[disk]: show information about disk data
- hdparm -tT /dev/[disk]: conduct a read speed test on disk
- badblocks -s /dev/[disk]: test for unreadable blocks on disk

## Searching

- grep [pattern] [file_name]: search for a specific pattern in a file
- grep -r [pattern] [directory_name]: search recursively for a specific pattern in a directory
- locate [name]: find all files and directories by a specific name
- find [/folder/location] -name [a]: list names that begin with [a] in [/folder/location]
- find [/folder/location] -size [+100M]: list files larger than 100M in a particular folder

## File Commands

- ls: list files in directory
- ls -a: list all files, including hidden
- pwd: show the directory currently working in
- mkdir [directory]: create a new directory
- rm [file_name]: remove a file
- rm -r [directory_name]: remove a directory recursively
- rm -rf [directory_name]: remove a directory recursively without requiring confirmation
- cp [file_name1] [file_name2]: copy the contents of the first file to the second file
- cp -r [directory_name1] [directory_name2]: recursively copy the contents of the first directory into the second directory
- mv [file_name1] [file_name2]: rename file_name1 to file_name2
- ln -s /path/to/[file_name] [link_name]: create a symbolic link to a file
- touch [file_name]: create a new file
- more [file_name]: show the contents of a file
- head [file_name]: show the first 10 lines of a file
- tail [file_name]: show the last 10 lines of a file
- gpg -c [file_name]: encrypt a file
- gpg [file_name.gpg]: decrypt a file
- wc: print the number of words, lines, and bytes in a file

## Directory Navigation

- cd ..: move up one level in the directory tree structure
- cd: change directory to $HOME
- cd /chosen/directory: change to specified directory

## File Transfer

- scp [file_name.txt] [server/tmp]: securely copy a specific file to a server directory
- rsync -a [/your/directory] [/backup/]: synchronize the contents of a specific directory with a backup directory

## Users

- id: show details of the active user
- last: show the last logins onto the system
- who: show who is logged into the system
- w: show who is logged in and their activity
- groupadd [group_name]: add a new group
- adduser [user_name]: add new user
- usermod -aG [group_name] [user_name]: add a user to a group
- userdel [user_name]: delete a user
- usermod: use for changing / modifying user information

## SSH Login

- ssh user@host: 
- ssh host: 
- ssh -p [port] user@host: 
- telnet host: 

Disk Usage
Keyboard Shortcuts
System Information
Network
Process Related
File Permission
Package Installation
File Compression






show free and used space on
mounted systems
show free inodes on mounted
filesystems
show disk partitions, sizes, and
types
show disk usage for all files and
directory
show disk usage of current
directory
show target mount point for all
filesystems
mount a device
df -h
df -i
fdisk -l
du -ah
du -sh
findmnt
mount [device_path]
[mount_point]
tar cf [compressed_file.
tar] [file_name]
tar xf [compressed_file.
tar]
tar czf
[compressed_file.tar.gz]
gzip [file_name]
uname -r
uname -a
uptime
hostname
hostname -i
last reboot
date
timedatectl
cal
w
whoami
finger
[username]
show system information
show kernel release information
show how long the system has been
running, including load average
show system hostname
show the IP address of the system
show system reboot history
show current time and date
query and change the system clock
show current calender month and
day
show logged in users in the system
show user you are using
show information about a user
Ctrl + C
Ctrl + Z
Ctrl + W
Ctrl + U
Ctrl + K
Ctrl + Y
Ctrl + R
Ctrl + O
Ctrl + G
!!
exit
kill current process running in the
terminal
stop current process (can be
resumed in the foreground with fg
or in the background with bg)
cut one word before the cursor and
add it to clipboard
cut part of the line before the
cursor and add it to clipboard
cut part of the line after the cursor
and add it to clipboard
paste from clipboard
recall last command that matches
the provided characters
run the previously recalled
command
exit command history without
running a command
repeat the last command
log out of current session
ps
pstree
pmap
top
kill [process_id]
pkill [proc_name]
killall [proc_name]
bg
fg
fg [job]
lsof
show a snapshot of active
processes
show processes as a tree
shows a memory usage map of
processes
show all running processes
kill a process under a given ID
kill a process under the specified
name
kill all processes labelled proc
list and resume stopped jobs in
the background
bring the most recent suspended
job to the foreground
bring a particular job to the
foreground
list files opened by processes
create an archived file from a file
extract archived file
create a gzip compressed tar file
compress a file with the .gz
extension
find a package by a related
keyword
show package information and
summary
install a package using the YUM
package manager
install a package using the DNF
package manager
install an rpm package from a local
file
remove an rpm package
install software from source code
yum search
[keyword]
yum info
[package_name]
yum install
[package_name.
rpm]
dnf install
[package_name.
rpm]
rpm -i
[package_name.
rpm]
rpm -e
[package_name.
rpm]
tar zxvf
[source_code.tar.gz]
cd [source_code]
./configure
make
make install
ip addr show
ip address add
[IP_address]
ifconfig
netstat -pnltu
netstat -nutlp
whois [domain]
dig [domain]
dig -x host
dig -x
[ip_address]
host [domain]
hostname -I
wget [file_name]
show IP addresses and network
interfaces
assign an IP address to interface
eth0
show IP addresses of all network
interfaces
show active (listening) ports
show tcp and udp ports and their
programs
show more information about a
domain
show DNS information about a
domain
reverse lookup on domain
reverse lookup of an IP address
do an IP lookup for a domain
show the local IP address
download a file from a domain
chmod 777 [file_name]
chmod 755 [file_name]
chmod 766 [file_name]
chown [user]
[file_name]
chown [user]: [group]
[file_name]
give read, write, and execute
permission to everyone
give full permission to owner, and
read and execute permission to
group and others
give full permission to owner, and
read and write permission to
group and others
change the file ownership
change the owner and group
ownership of a fileconnect to host as user
securely connect to host via SSH
default port 22
connect to host using a particular
port
connect to host via telnet default
port 23