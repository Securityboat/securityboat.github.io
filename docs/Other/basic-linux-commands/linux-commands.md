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

​- Remove and replace

# Remove all dots and replace them with underscore.

`cat file.txt | tr "." "_"**`

**awk**

So awk is an advanced tool for editing text-files. It is its own programming language to it can become quite complex. Awk iterates over the whole file line by line.

This is the basic structure of an awk command
awk '/search_pattern/ { action_to_take_on_matches; another_action; }' file_to_parse
The search pattern takes regex. You can exclude the search portion or the action portion.

This just prints every line of the file.

Filtering out specific ip-address:
awk '/172.16.40.10.81/' error.log
Now we want to print out the fourth column of that file, we can just pipe this to cut, but we can also use awk for it, like this:
awk '/172.16.40.10.81/ {print $4}' error.log# Another exampleawk '{print $2,$5;}' error.txtThis prints columns 2 and 5.
We can use the -F flag to add a custom delimiter.
awk -F ':' '{print $1}' test.txt
## **User Management**

To add a user we do:
adduser NameOfUser​# On some machines it isuseradd nameOfUser
To add user to sudo-group:

On some machines we might not be able to edit the sudoers file because we don't have an interactive shell, in this case can you can just redirect the text into the file, like this:
echo "username ALL=(ALL) ALL" >> /etc/sudoers
Check which users are in the sudo group:
cat /etc/group | grep sudo
Switch user in terminal:

Remove/delete user:

## **Permissions**

Shows all the files and directories and their permission settings.
drwxrwxrwt 2 root root 4,0K ago  3 17:33 myfile
Here we have 10 letters in the beginning. The first one `d` shows that it is a directory. The next three letters are for read, `w` for write and `x` for execute. The first three belong to the owner, the second three to the group, and the last three to all users.

​[https://linuxjourney.com/lesson/file-permissions](https://linuxjourney.com/lesson/file-permissions)​

## **Processes**

To display information regarding the systems processes you can use the `ps` command.

- `-a` stands for all `-u` stands for all processes by all users `-x` stands for all processes that don't run a `tty`+

### **Install Package**

Example of how to install something with apt:
sudo apt-get install nmap​
### **Remove Packages**

This can be tricky. First find the package

Then you find it in your list.
sudo apt-get --purge remove nameOfProgram
### **Organizing your $path variable**

I am talking about debian/ubuntu here. On other systems I don't know.

You can define your path in `/etc/environment`. If you don't have it you can create it and add the path like this:
source /etc/environment && export PATH
If you are using zsh (which you should) you have to add it here

And add this line somewhere:

### **Adding a Path**

This is a non-persistent way to add binaries to your path. Might be useful if you have entered a system that has limited binaries in the path.
export PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
## **Cronjobs**

There are two ways to configure cronjobs. The first one is by putting scripts in the following folders.
/etc/cron.daily/etc/cron.hourly/etc/cron.weekly/etc/cron.monthly
The second way is to write the command in the crontab
# **list cronjobscrontab -l​# Edit or create new cronjobscrontab -e**
## **Devices**

List all devices

## **The Filesystem**

**Difference between sbin and bin**

sbin is system binaries. A normal user do not have access to these binaries. It is only root and users with sudo privileges that do.

### **Mount**

So everything on the linux-filesystem belongs to some part of the filesystem-tree. So if we plug in some device we need to mount it to the filesystem. That pretty much means that we need to connect it to the filesystem. Mount is like another word for connect.

So if you want to connect a CD-rom or USB to your machine. You need to mount it to a specific path on the filesystem.

So if you plug in the usb it might be accessible at **/dev/usb**. But that it not enough for you to be able to browse the usb content. You need to mount it. You do this by writing
mount /dev/usb /media/usb
Or whereever you want to mount it.

So when you click on Eject or Safetly remove you are just unmounting.

Knowing how to mount and unmount might be useful if you want to get access to a remote NFS-directory. You will need to mount it to your filesystem to be able to browse it.
## **10. Controlling services**

### **Systemctl**

Systemctl can be used to enable and disable various services on your linux machine. Start ssh
systemctl start sshsystemctl status sshsystemctl stop ssh

You can verify that the service is listening for connection by running network status.

Make ssh start upon boot
systemctl enable sshsystemctl enable apache2
### **Init.d**

Init.d is just a wrapper around Systemctl. I prefer it.
/etc/init.d/cron status/etc/init.d/cron start/etc/init.d/cron stop

## **16. Network basics**

### **Netstat - Find outgoing and incoming connections**

Netstat is a multiplatform tool. So it works on both mac, windows and linux.
Find out what services are listening for connection on your machine Flags
-a # All-n # show numeric addresses-p # show port-t # tcp
To easily check out what process is using lots of bandwidth you can use nethogs.
sudo apt-get install nethogsnethogs

### **Firewall - Iptables**

Iptables is a firewall tool in linux. A firewall is basically a tool that scans incoming and/or outgoing traffic. You can add rules to the iptables to filter for certain traffic.

**Types of chains**

So you can filter traffic in three different ways **input**, **forward**, and **output**. These are called three different chains.

**INPUT** This is for incoming connections. If someone wants to ssh into your machine. Or a web-server responds to your request.

**FORWARD** This chain is used for traffic that is not aimed at your machine. A router for example usually just passes information on. Most connections are just passing through. As you can see this will probably not be used so much on your machine, as a normal desktop or a server doesn't router that much traffic.

**OUTPUT**

This chain is used for outgoing traffic.

**Active rules**

To view your active rules you do
iptables -L# It will output something like this​Chain INPUT (policy ACCEPT)target     prot opt source               destination         ​Chain FORWARD (policy ACCEPT)target     prot opt source               destination         ​Chain OUTPUT (policy ACCEPT)target     prot opt source               destination
So as we can see the current policy is to accept all traffic in all directions.

If you for some reason has been tampering with the iptables and maybe fucked up. This is how you return it to the default setting, accepting all connections
iptables --policy INPUT ACCEPTiptables --policy OUTPUT ACCEPTiptables --policy FORWARD ACCEPT
If you instead want to forbid all traffic you do
iptables --policy INPUT DROPiptables --policy OUTPUT DROPiptables --policy FORWARD DROP
Okay, so let's block out some connections. To do that we want to add/append a new rule. We want to block all connections from our enemy 192.168.1.30.
# **A for append, and S for source. iptables -A INPUT -s 192.168.1.30 -j DROP# Block an entire rangeiptables -A INPUT -s 192.168.1.0/24 -j DROP**
Now if we want to see our current rules we just do
**Measuring bandwidth usage**

There are a few different tools in hour arsenal that we can use to measure bandwidth usage. We will start with iptables.

To view the input and output traffic we just list the rules with some verbosity.
iptables -L -v# StdoutChain INPUT (policy ACCEPT 6382 packets, 1900K bytes) pkts bytes target     prot opt in     out     source               destination         ​Chain FORWARD (policy ACCEPT 0 packets, 0 bytes) pkts bytes target     prot opt in     out     source               destination         ​Chain OUTPUT (policy ACCEPT 4266 packets, 578K bytes) pkts bytes target     prot opt in     out     source               destination
So clean this up and reset the count we can do the following
# **Restar the countiptables -Z# Remove all the rules, FLUSH themiptables -F**

**Examples**

**Block outgoing connections to a specific ip**
iptables -A OUTPUT -d ip -j DROP

