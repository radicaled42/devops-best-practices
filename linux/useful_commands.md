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

- ssh user@host: connect to host as user
- ssh host: securely connect to host via SSH default port 22
- ssh -p [port] user@host: connect to host using a particular port
- telnet host: connect to host via telnet default port 23

## Disk Usage

- df -h: show free and used space on mounted systems
- df -i: show free inodes on mounted filesystems
- fdisk -l: show disk partitions, sizes, and types
- du -ah: show disk usage for all files and directory
- du -sh: show disk usage of current directory
- findmnt: show target mount point for all filesystems
- mount [device_path] [mount_point]: mount a device

## Keyboard Shortcuts

- Ctrl + C: kill current process running in the terminal
- Ctrl + Z: stop current process (can be resumed in the foreground with fg or in the background with bg)
- Ctrl + W: cut one word before the cursor and add it to clipboard
- Ctrl + U: cut part of the line before the cursor and add it to clipboard
- Ctrl + K: cut part of the line after the cursor and add it to clipboard
- Ctrl + Y: paste from clipboard
- Ctrl + R: recall last command that matches the provided characters
- Ctrl + O: run the previously recalled command
- Ctrl + G: exit command history without running a command
- !!: repeat the last command
- exit: log out of current session

## System Information

- uname -r: show system information
- uname -a: show kernel release information
- uptime: show how long the system has been running, including load average
- hostname: show system hostname
- hostname -i: show the IP address of the system
- last reboot: show system reboot history
- date: show current time and date
- timedatectl: query and change the system clock
- cal: show current calender month and day
- w: show logged in users in the system
- whoami: show user you are using
- finger [username]: show information about a user

## Network

- ip addr show: show IP addresses and network interfaces
- ip address add [IP_address]: assign an IP address to interface eth0
- ifconfig: show IP addresses of all network interfaces
- netstat -pnltu: show active (listening) ports
- netstat -nutlp: show tcp and udp ports and their programs
- whois [domain]: show more information about a domain
- dig [domain]: show DNS information about a domain
- dig -x host: reverse lookup on domain
- dig -x [ip_address]: reverse lookup of an IP address
- host [domain]: do an IP lookup for a domain
- hostname -I: show the local IP address
- wget [file_name]: download a file from a domain

## Process Related

- ps: show a snapshot of active processes
- pstree: show processes as a tree
- pmap: shows a memory usage map of processes
- top: show all running processes
- kill [process_id]: kill a process under a given ID
- pkill [proc_name]: kill a process under the specified name
- killall [proc_name]: kill all processes labelled proc
- bg: list and resume stopped jobs in the background
- fg: bring the most recent suspended job to the foreground
- fg [job]: bring a particular job to the foreground
- lsof: list files opened by processes

## File Permission

- chmod 777 [file_name]: give read, write, and execute permission to everyone
- chmod 755 [file_name]: give full permission to owner, and read and execute permission to group and others 
- chmod 766 [file_name]: give full permission to owner, and read and write permission to group and others
- chown [user] [file_name]: change the file ownership
- chown [user]: [group] [file_name]: change the owner and group ownership of a file 

## Package Installation

- yum search [keyword]: find a package by a related keyword
- yum info [package_name]: show package information and summary
- yum install [package_name.rpm]: install a package using the YUM package manager
- dnf install [package_name.rpm]: install a package using the DNF package manager
- rpm -i [package_name.rpm]: install an rpm package from a local file
- rpm -e [package_name.rpm]: remove an rpm package
- tar zxvf [source_code.tar.gz] && cd [source_code] && ./configure && make && make && install: install software from source code

## File Compression

- tar cf [compressed_file.tar] [file_name]: create an archived file from a file
- tar xf [compressed_file. tar]: extract archived file
- tar czf [compressed_file.tar.gz]: create a gzip compressed tar file
- gzip [file_name]: compress a file with the .gz extension


### Bibliography

- https://ns2.elhacker.net/cheat-sheet/linux-commands-cheat-sheet-by-pnap.pdf