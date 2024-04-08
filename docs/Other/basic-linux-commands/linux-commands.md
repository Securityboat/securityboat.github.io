# **Linux Commands**

## **The Shell - Bash**

The shell, or the terminal is a really useful tool. Bash is the standard shell on most Linux distros.

### **Navigating**

- `pwd` - Print working directory
- `cd` - Change directory
- `cd ~` - Change directory to your home directory

### **Looking at files**

- `ls` - List files in directory
- `ls -ltr` - Sort list by last modified. -time -reverse
- `file` - Show info about file. What type of file it is. If it is a binary or text file for example.
- `cat` - Output content of file.
- `less` - Output file but just little bit at a time. Use this one. Not `more`.
- `/searchterm` Use it to search. It is the same command as in vim. `n` to scroll to next search result. Press `q` to quit.
- `more` - Output file but just little bit at a time. `less` is better.

### **A little bit of everything**

- `history` - Show commands history
- `sudo`
List what rights the sudo user has. Sudo config file is usually **/etc/sudoers**

### **Working with files**

- `touch` - Create a new file.
- `cp` - Copy
- `mkdir` - Make directory.
- `mkdir -p new/thisonetoo/and/this/one` - Make entire directory structure
- `rm` - Remove file
- `rm -rf ./directory​` - Remove recursively and its content. Very dangerous command!

**Find**

Find is slower than locate but a lot more thorough. You can search for files recursively and with regex and a lot of other features.

- `find / -name file 2>/dev/null` - This will send all permissions denied outputs to dev/null.

**Locate**

Locate is really fast because it relies on an internal database.

- `sudo updatedb` - Update the internal locate database
- `locate example.txt` - Search for a file named example.txt

**Which**

Outputs the path of the binary that you are looking for. It searches through the directories that are defined in your $PATH variable.
- `which bash` - Prints the path of bash. /bin/bash​

### **Filters**

There are certain programs that are especially useful to use together with pipes. They can also be used as stand-alone programs but you will often see them together with pipes.

- `sort`
- `uniq`
- `sort -u test.txtsort test.txt | uniqcat filename | sort -u > newFileName`
- `grep`
- `head`
- `tail`
- `tr`

### **Editing text**

**sed**

Can perform basic editing on streams, that is to say, text.
- `sed -i '1d' example.txt` - Remove first line of example.txt

**cut**

Cut by column. This is a useful command to cut in text. Let's say that we have the following text, and we want to cut out the ip-address.
> 64 bytes from ip: icmp_req=1 ttl=255 time=4.86 ms

- `echo "64 bytes from ip: icmp_req=1 ttl=255 time=4.86 ms" | grep -oP '(\d+\.){3}\d+' | cut -d ' ' -f 4` - Cut out IP address.

**tr - Translate**

- `tr "[:lower:]" "[:upper:]" < file1 > file2​` - Transform all letter into capital letters

Example Remove character
- Remove characters

- `cat file.txt | tr -d "."`

- `cat file.txt | tr "." "_"**` - Remove all dots and replace them with underscore.

**awk**

awk is an advanced tool for editing text-files. It is its own programming language to it can become quite complex. Awk iterates over the whole file line by line. Below is the basic structure of an awk command

- `awk '/search_pattern/ { action_to_take_on_matches; another_action; }' file_to_parse` - The search pattern takes regex. You can exclude the search portion or the action portion.

- `awk '/172.16.40.10.81/' error.log` - Filtering out specific ip-address

- `awk '/172.16.40.10.81/ {print $4}' error.log# Another exampleawk '{print $2,$5;}' error.txt` - This prints columns 2 and 5.

- `awk -F ':' '{print $1}' test.txt` - Use the -F flag to add a custom delimiter

## **User Management**

User management involves various commands for creating, modifying, and deleting user accounts, as well as managing user permissions and groups.

- **useradd**: This command is used to add a new user account to the system.

    ```
    useradd username
    ```

- **passwd**: This command is used to set or change the password for a user account.

    ```
    passwd username
    ```

- **userdel**: This command is used to delete a user account from the system.

    ```
    userdel username
    ```

- **usermod**: This command is used to modify user account properties such as username, home directory, shell, etc.

    ```
    usermod -l newusername oldusername  # Change username
    usermod -d /new/home/directory username  # Change home directory
    usermod -s /bin/bash username  # Change default shell
    ```

- **groupadd**: This command is used to add a new group to the system.

    ```
    groupadd groupname
    ```

- **groupdel**: This command is used to delete a group from the system.

    ```
    groupdel groupname
    ```

- **groups**: This command displays the groups to which a user belongs.

    ```
    groups username
    ```

- **usermod -aG**: This command is used to add a user to a supplementary group.

    ```
    usermod -aG groupname username
    ```

- **chown**: This command is used to change the owner of a file or directory.

    ```
    chown username:groupname filename
    ```

- **chgrp**: This command is used to change the group ownership of a file or directory.

    ```
    chgrp groupname filename
    ```

## **Permissions**

In Linux, file permissions control access to files and directories. There are three types of permissions: read \(r), write (w), and execute (x). These permissions are assigned to three different entities: the file/directory owner, the group associated with the file/directory, and others (everyone else).

- **chmod**: This command is used to change the permissions of a file or directory.

    ```
    chmod permissions filename/directory
    ```

    - `permissions` can be specified using symbolic notation (e.g., u+x for adding execute permission for the owner) or octal notation (e.g., - for rwxr-xr-x permissions).
  
- **chown**: This command is used to change the owner and/or group of a file or directory.

    ```
    chown owner:group filename/directory
    ```

- **chgrp**: This command is used to change the group ownership of a file or directory.

    ```
    chgrp groupname filename/directory
    ```

- **ls**: This command is used to list files and directories, and it also shows their permissions.

    ```
    ls -l
    ```

- **umask**: This command sets the default permissions for newly created files and directories.

    ```
    umask permissions
    ```

- **setfacl**: This command is used to set Access Control Lists (ACLs) for files and directories, allowing more fine-grained control over permissions.

    ```
    setfacl -m u:user:permissions filename/directory
    ```

- **getfacl**: This command is used to view the ACLs of files and directories.

    ```
    getfacl filename/directory
    ```

​[https://linuxjourney.com/lesson/file-permissions](https://linuxjourney.com/lesson/file-permissions)​

## **Processes**

In Linux, process commands are used to manage and interact with processes running on the system.

- **ps**: This command is used to display information about active processes.

    ```
    ps
    ```

    - To display more detailed information, you can use options like `-aux`, `-ef`, or `-e`.
    ```
    ps aux
    ```

- **top**: This command provides dynamic real-time information about running processes, CPU usage, memory usage, etc.

    ```
    top
    ```

- **htop**: Similar to top but with a more user-friendly interface and additional features.

    ```
    htop
    ```

- **kill**: This command is used to terminate processes by sending signals.

    ```
    kill PID
    ```

    - The default signal is SIGTERM (terminate), but you can also send other signals like SIGKILL (force termination) using `-- option.
    ```
    kill -9 PID
    ```

- **killall**: This command is used to kill processes by name rather than by PID.

    ```
    killall process_name
    ```

- **pgrep**: This command is used to search for processes based on name or other attributes and print their PIDs.

    ```
    pgrep process_name
    ```

- **pkill**: This command is used to send signals to processes based on their names or other attributes.

    ```
    pkill process_name
    ```

- **nice**: This command is used to launch a process with a specified priority (niceness).

    ```
    nice -n value command
    ```

- **renice**: This command is used to change the priority (niceness) of an already running process.

    ```
    renice priority PID
    ```

- **jobs**: This command is used to display currently running jobs in the shell.

    ```
    jobs
    ```

## **Package management**

Package management is typically done using the Advanced Packaging Tool (APT) and its various frontends. (in Ubuntu, other linux distributions uses other package managers)

- **apt-get**: This is a command-line tool used to handle package management tasks, such as installing, updating, upgrading, and removing packages.

    - Install a package:
    ```
    sudo apt-get install package_name
    ```

    - Remove a package:
    ```
    sudo apt-get remove package_name
    ```

    - Update the package list (repository information):
    ```
    sudo apt-get update
    ```

    - Upgrade installed packages to their latest versions:
    ```
    sudo apt-get upgrade
    ```

- **apt**: A more user-friendly frontend to apt-get. It provides colorful output and progress bars.

    - Install a package:
    ```
    sudo apt install package_name
    ```

- **apt-cache**: This command is used to search and query information about packages available in APT's package cache.

    - Search for a package:
    ```
    apt-cache search search_term
    ```

    - Show information about a specific package:
    ```
    apt-cache show package_name
    ```

- **dpkg**: This is a low-level package management tool. It can be used to install, remove, and query information about individual packages.

    - Install a package (with its full path):
    ```
    sudo dpkg -i /path/to/package.deb
    ```

    - Remove a package (keeping its configuration files):
    ```
    sudo dpkg -r package_name
    ```

    - Remove a package (including its configuration files):
    ```
    sudo dpkg -P package_name
    ```

- **aptitude**: Another frontend for APT. It provides a text-based interface for package management tasks and dependency resolution.

    - Install a package:
    ```
    sudo aptitude install package_name
    ```

- **snap**: Ubuntu also supports snap packages, which are self-contained applications bundled with their dependencies.

    - Install a snap package:
    ```
    sudo snap install package_name
    ```

    - Remove a snap package:
    ```
    sudo snap remove package_name
    ```

- **Adding a Path**: This is a non-persistent way to add binaries to your path. Might be useful if you have entered a system that has limited binaries in the path.
```
export PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
```

## **Cronjobs**

Cronjobs are scheduled tasks in Unix-like operating systems, including Linux, that run at predefined times or intervals. They are managed using the cron daemon.

- **crontab**: This command is used to create, edit, and list cronjobs for a user.

    ```
    crontab -e   # Edit the cronjobs for the current user
    crontab -l   # List the cronjobs for the current user
    crontab -r   # Remove all cronjobs for the current user
    ```

- **cron.allow** and **cron.deny**: These files are used to control access to the cron daemon. If `cron.allow` exists, only users listed in it are allowed to use cron. If `cron.allow` does not exist but `cron.deny` does, users listed in `cron.deny` are not allowed to use cron. If neither file exists, only the superuser can use cron.

- **/etc/cron.d/**: This directory contains system-specific cronjobs. Instead of using the crontab command, system administrators can place cronjob files directly in this directory. The format of these files is the same as the user crontab files.

- **/etc/cron.{hourly,daily,weekly,monthly}/**: These directories contain system-wide scripts that are executed hourly, daily, weekly, or monthly. Scripts placed in these directories will be run automatically at the specified intervals.

- **systemctl**: On modern Linux distributions using systemd, you can control the cron service using systemctl.

    ```
    systemctl start cron.service    # Start the cron service
    systemctl stop cron.service     # Stop the cron service
    systemctl restart cron.service  # Restart the cron service
    systemctl status cron.service   # Check the status of the cron service
    ```

## **Devices**

In Linux, devices commands are used to manage and interact with hardware devices connected to the system. These commands help in viewing device information, configuring devices, and diagnosing issues.

- **lsblk**: This command lists information about block devices (e.g., hard drives, solid-state drives) connected to the system.

    ```
    lsblk
    ```

- **lspci**: This command lists all PCI buses and devices connected to them.

    ```
    lspci
    ```

- **lsusb**: This command lists USB buses and devices connected to them.

    ```
    lsusb
    ```

- **lshw**: This command provides detailed information about hardware configuration, including devices and their drivers.

    ```
    lshw
    ```

- **dmesg**: This command displays the kernel ring buffer, which contains information about device detection and driver initialization messages.

    ```
    dmesg
    ```

- **hwinfo**: This command provides detailed hardware information, including devices and their configuration.

    ```
    hwinfo
    ```

- **udevadm**: This command is used to manage device nodes in the udev (device manager) system.

    ```
    udevadm info /dev/sda
    ```

- **hdparm**: This command is used to get/set ATA/SATA device parameters like reading/writing speed, power management, etc.

    ```
    hdparm -I /dev/sda  # Get detailed information about a SATA drive
    ```

- **fdisk** and **parted**: These commands are used for disk partitioning and management.

    ```
    fdisk -l  # List partitions on all disks
    parted /dev/sda print  # Print partition table for a specific disk
    ```

- **lsdev**: This command lists all available devices on the system.

    ```
    lsdev
    ```

## **Mount**

In Linux, the `mount` command is used to mount file systems onto directories within the Linux filesystem.

- **Mounting a File System:**

    ```
    mount /dev/sdXY /mnt/mydisk
    ```

    - This command mounts the file system located on device `/dev/sdXY` to the directory `/mnt/mydisk`. Replace `/dev/sdXY` with the appropriate device identifier (e.g., `/dev/sda- for the first partition on the first SCSI/SATA/USB drive).

- **Mounting All File Systems Listed in `/etc/fstab`:**

    ```
    mount -a
    ```

    - This command mounts all file systems listed in the `/etc/fstab` file that are not already mounted.

- **Unmounting a File System:**

    ```
    umount /mnt/mydisk
    ```

    - This command unmounts the file system mounted on `/mnt/mydisk`. Replace `/mnt/mydisk` with the appropriate mount point.

- **Mounting a Network File System (NFS):**

    ```
    mount -t nfs server:/remote/directory /mnt/mountpoint
    ```

    - This command mounts a remote NFS share located at `server:/remote/directory` to the local directory `/mnt/mountpoint`.

- **Mounting a CD-ROM or DVD:**

    ```
    mount /dev/cdrom /mnt/cdrom
    ```

    - This command mounts the CD-ROM or DVD drive to the directory `/mnt/cdrom`.

- **Viewing Mounted File Systems:**

    ```
    mount
    ```

    - This command displays a list of all currently mounted file systems.

- **Bind Mounting:**

    ```
    mount --bind /source/directory /destination/directory
    ```

    - This command mounts a directory at another location, making the content of both directories accessible at both mount points.

- **Remounting a File System with Different Options:**

    ```
    mount -o remount,rw /mnt/mydisk
    ```

    - This command remounts the file system mounted on `/mnt/mydisk`, changing its options. In this example, it remounts it with read-write permissions.

## **Controlling services**

In Linux, services are background processes that run continuously to provide specific functionalities. Controlling services involves starting, stopping, restarting, enabling at boot time, and disabling services as needed.

- **systemctl**: This command is used to control systemd services in modern Linux distributions such as Ubuntu, CentOS, and Fedora.

    - Start a service:
    ```
    sudo systemctl start service_name
    ```

    - Stop a service:
    ```
    sudo systemctl stop service_name
    ```

    - Restart a service:
    ```
    sudo systemctl restart service_name
    ```

    - Enable a service to start automatically at boot time:
    ```
    sudo systemctl enable service_name
    ```

    - Disable a service from starting automatically at boot time:
    ```
    sudo systemctl disable service_name
    ```

    - Check the status of a service:
    ```
    sudo systemctl status service_name
    ```

- **service**: This command is used to control SysVinit services, commonly found in older Linux distributions.

    - Start a service:
    ```
    sudo service service_name start
    ```

    - Stop a service:
    ```
    sudo service service_name stop
    ```

    - Restart a service:
    ```
    sudo service service_name restart
    ```

    - Check the status of a service:
    ```
    sudo service service_name status
    ```

- **chkconfig**: This command is used to enable or disable services to start at boot time on SysVinit-based systems.

    - Enable a service at boot time:
    ```
    sudo chkconfig service_name on
    ```

    - Disable a service from starting at boot time:
    ```
    sudo chkconfig service_name off
    ```

- **update-rc.d**: This command is used to manage System V (SysV) init scripts on Debian-based systems.

    - Enable a service at boot time:
    ```
    sudo update-rc.d service_name defaults
    ```

    - Disable a service from starting at boot time:
    ```
    sudo update-rc.d -f service_name remove
    ```

These commands allow administrators to control the operation of services on Linux systems effectively. They are crucial for managing server processes, ensuring that essential services start automatically after system reboots, and troubleshooting service-related issues. The specific commands to use may vary depending on the Linux distribution and the init system being used (SysVinit or systemd).

## **Network basics**

In Linux, there are several commands available to manage and troubleshoot network-related tasks.

- **ifconfig**: This command displays the configuration of network interfaces, including IP addresses, MAC addresses, and network-related statistics.

    ```
    ifconfig
    ```

    - Note: `ifconfig` has been deprecated on many modern Linux distributions in favor of `ip` command.

- **ip**: This command is a more modern replacement for `ifconfig` and provides extensive functionality for configuring network interfaces, routing tables, and more.

    - Show information about network interfaces:
    ```
    ip addr show
    ```

    - Show routing table:
    ```
    ip route show
    ```

- **ping**: This command is used to send ICMP echo requests to a specified host to check network connectivity.

    ```
    ping hostname_or_IP
    ```

- **traceroute**: This command is used to trace the route that packets take from your computer to a specified destination host.

    ```
    traceroute hostname_or_IP
    ```

- **netstat**: This command displays network connections, routing tables, interface statistics, masquerade connections, and multicast memberships.

    - Show network connections:
    ```
    netstat -tuln
    ```

- **ss**: This command is a modern replacement for `netstat` and provides similar functionality.

    - Show socket statistics:
    ```
    ss -tuln
    ```

- **dig**: This command is used to perform DNS (Domain Name System) queries such as looking up IP addresses associated with domain names.

    ```
    dig domain_name
    ```

- **nslookup**: This command is used to query DNS servers to obtain domain name or IP address mapping.

    ```
    nslookup domain_name
    ```

- **hostname**: This command displays the hostname of the system.

    ```
    hostname
    ```

- **ifup/ifdown**: These commands are used to bring network interfaces up or down manually.

    ```
    sudo ifup interface_name
    sudo ifdown interface_name
    ```

## **Firewall**

In Linux, a firewall is a network security system that monitors and controls incoming and outgoing network traffic based on predetermined security rules. The firewall can be implemented using various tools such as iptables, nftables, and firewalld. These tools allow administrators to define rules that specify which network packets are allowed or denied based on criteria such as source and destination IP addresses, ports, and protocols.

Here are some key concepts related to firewalls in Linux:

- **Packet Filtering**: A firewall examines each network packet passing through it and decides whether to allow or block it based on predefined rules. Packet filtering is the fundamental functionality of a firewall.

- **Chains**: In Linux firewall configurations, rules are organized into chains. Each chain is a list of rules that are applied sequentially to incoming or outgoing packets. Commonly used chains in Linux firewalls include:

   - **INPUT chain**: Used for packets destined for the local system.
   - **OUTPUT chain**: Used for packets originating from the local system.
   - **FORWARD chain**: Used for packets that are being routed through the system.

- **Default Policies**: Each chain has a default policy that specifies what action should be taken if a packet does not match any of the rules in the chain. Common default policies are ACCEPT, DROP, and REJECT.

- **Rules**: Rules are the individual instructions that determine whether a packet is allowed or denied. Each rule consists of criteria (such as source and destination addresses, ports, and protocols) and an action (such as ACCEPT, DROP, or REJECT). Rules are evaluated in order, and the action of the first matching rule is applied.

- **Stateful Inspection**: Some firewall configurations support stateful inspection, which tracks the state of active network connections. This allows the firewall to make more informed decisions based on the state of the connection, such as allowing return traffic for established connections.

- **Logging**: Firewalls can be configured to log information about packets that are blocked or allowed. Logging helps administrators monitor network traffic and troubleshoot firewall issues.

- **Network Address Translation (NAT)**: In addition to packet filtering, firewalls can also perform Network Address Translation (NAT) to modify the source or destination IP addresses of packets as they pass through the firewall. NAT is often used to hide internal IP addresses or to map multiple internal IP addresses to a single external IP address.

### **iptables**

In Linux, `iptables` is a powerful firewall utility that allows administrators to configure rules for packet filtering and network address translation (NAT).

- **Listing Current Rules**:
   - List all current rules:
     ```
     sudo iptables -L
     ```

- **Creating Rules**:
   - Add a rule to allow traffic on a specific port (e.g., TCP port 80):
     ```
     sudo iptables -A INPUT -p tcp --dport - -j ACCEPT
     ```
   - Add a rule to allow traffic from a specific IP address:
     ```
     sudo iptables -A INPUT -s <IP_address> -j ACCEPT
     ```
   - Add a rule to block traffic from a specific IP address:
     ```
     sudo iptables -A INPUT -s <IP_address> -j DROP
     ```

- **Deleting Rules**:
   - Delete a specific rule (use `-D` followed by the rule number as listed in `iptables -L`):
     ```
     sudo iptables -D INPUT <rule_number>
     ```

- **Flushing Rules**:
   - Flush all rules (delete all rules from the specified chain):
     ```
     sudo iptables -F
     ```

- **Setting Policies**:
   - Set the default policy for a chain (e.g., INPUT, OUTPUT, FORWARD) to DROP:
     ```
     sudo iptables -P INPUT DROP
     ```

- **Saving and Restoring Rules**:
   - Save current rules to a file:
     ```
     sudo iptables-save > /path/to/save/iptables-rules
     ```
   - Restore rules from a file:
     ```
     sudo iptables-restore < /path/to/saved/iptables-rules
     ```

- **Miscellaneous Commands**:
   - Check detailed information about packet counters and byte counts:
     ```
     sudo iptables -L -v
     ```
