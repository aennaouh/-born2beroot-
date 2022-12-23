# -born2beroot-
**globle information** 

- **i**n lunix   theres no administration there is root
- hardware its the mather bord , RAM ……
- software ; oeration syseteme(windows , linux, mac)
- **debian** its easy to install and configure then centos because debian you can find implement of information its also un open source  

**centos**  - replica of redhat and its take to muche time to updat 10 years debian about 2 years

**virtual machine**

- A virtual machine is a **software capable of installing an Operating System within itself,**
- This is possible because **the virtual machine is hosted on a physical device**
- here can be multiple virtual machines on the same host and each of these will be isolated from the rest of the system.

### How do Virtual Machines work?

Virtualization allow us share a system with multiple virtual environments. The hypervisor manages the hardware system and separate the physical resources from the virtual environments.

The software program that creates virtual machines is **the hypervisor**

definition:

A **hypervisor** is a type of computer software, firmware or hardware that creates and runs virtual machines. A computer on which a hypervisor runs one or more virtual machines is called a host machine, and each virtual machine is called a guest machine.

here can be multiple virtual machines on the same host and each of these will be isolated from the rest of the system.

                  **differences between CentOS and Debian?**

**debian** its easy to install and configure then centos because debian you can find implement of information its also un open source  

**centos**  - replica of redhat and its take to muche time to updat 10 years debian about 2 years 

                               **the difference between aptitude and apt?**

In Debian-based OS distributions, the default package manager we can use is dpkg This tool allows us to install, remove and manage programs on our operating system

**apt :** can be used to install all the necessary dependencies when installing a program we can install a useful program with a single command.

EXEMPLE  : apt-get, which allows us to install and remove packages.

**aptitude :** we use a graphical interface and commandline 

Apart from main difference being that **Aptitud**e is a high-level package manager while **APT** is lower-level package manager

                                             **What is AppArmor?**

apparmor  gere permission that app have 

For example, if an installed application can take photos by accessing the camera application, but the administrator denies this privilege, the application will not be able to access the camera application

• To check AppArmor status: `sudo aa-status`

**Package Managers** are essentially software applications that help users to: Search, Download, Install, Remove and Update software applications on their computer operating system

                                                            **SSH** 

rules that allows 2 machines to communicate securely over a network

host is server

ssh uses asymmetric cypher(algorithm or function for performing encryption or decryption)

There are three different techniques that SSH uses to encrypt:

- Symmetric encryption: a method that uses the same secret key
- Asymmetric encryption: These are known as the public key and the private key
- private key

                                                   **UFW**

Once we have UFW installed, we can choose which ports we want to allow connections, and which ports we want to close. This will also be very useful with SSH,

**password chosen condition subject  command check** 

- chage -l  user name

• `sudo vim /etc/login.defs`

check password strength

• `sudo vim /etc/pam.d/common-password`

### Check that the chosen OS is Debian or CentOS.

- `head -n 2 /etc/os-release`

### Check that a user with your login is present on the VM.

- `awk -F: '{ print $1}' /etc/passwd`

### port check

- vi etc/ssh/sshd_config
- netstat -W

### chack if apprmor work

- systemctl status apparmor

### check if the

- sudo service ufw status
- sudo service ssh status

### add user to group

- adduser aennaouh name of the group

### check if user add to group

- getent group name of the group
- sudo !!

## **Create group**

```
$ sudo groupadd user42sud0
$ sudo groupadd evaluating

```

```
Check if group created:

$ getent group

```

## **2.8. Create user and assign into group**

Check the all local users:

```
$ cut -d: -f1 /etc/passwd
```

Create the user

```
$ sudo adduser username
```

Assign an user into “evaluating” group (This is for when you defend)

```

$ sudo usermod -aG evaluating your_new_username
```

Check if the user is in group

```

$ getent group evaluating
```

Check which groups user account belongs:

```
$ groups
```

Check if password rules working in users:

```
$ chage -l your_new_username
```

## **Change hostname (!!!This is for when you defend!!!)**

Check current hostname

```
$ hostnamectl
```

Change the hostname

```
vi /etc/hostname
vi /etc/hosts
$ hostnamectl set-hostname new_hostname
```

Change /etc/hosts file

```
$ sudo nano /etc/hosts
```

Change old_hostname with new_hostname:

```
127.0.0.1       localhost
127.0.0.1       new_hostname
```

Reboot and check the change


**script** 

wall << .
#Architecture: `uname -a`
#CPU physical : `cat /proc/cpuinfo | grep "physical id" | wc -l`
#vCPU : `cat /proc/cpuinfo | grep "processor" | wc -l`
#Memory Usage : `free --mega | awk '{if ($1 == "Mem:") printf "%d/%dMB (%.2f%%)\\n",$3,$2,$3*100/$2}'`
#Disk Usage : `df -m | grep "^/dev" | awk '{u += $3;a+= $4;} END {printf "%d/%dGb (%d%%)\\n",u/1024,a/1024,u*100/a}'`
#Cpu load :  `top -bn1 | grep Cpu | awk '{printf("(%.2f%%)\\n",$2 + $4)}'`
#last boot : `who -b | awk '{print $3" " $4}'`
#LVM use : `vgdisplay | grep "Cur LV" | awk '{if ($3 >  0 ) print "yes" }'`
#Connections TCP : `netstat -tan | grep "ESTABLISHED" | wc -l | awk '{print  $1" ESTABLISHED"}'` 
#User log : `who | awk '{print $1}' | sort -u | wc -l`
#Network : IP `hostname -I` (`ifconfig | grep 'ether' | awk '{print($2)}'`)
#Sudo : `cat /var/log/auth.log | grep -a COMMAND | wc -l` cmd
