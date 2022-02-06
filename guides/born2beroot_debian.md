# Born2beRoot with Debian OS

## Debian Installation

- Download VirtualBox virtual machine [here](https://www.virtualbox.org/)
- Download Debian OS [here](https://www.debian.org/)
- Watch partition (mandatory) set-up [here]()
- Watch partition (bonus) set-up [here]()

## Sudo

<b style="font-size:16px"> Step 1: Install sudo </b>

Change user to root account, simply run `su` or `su –` without any arguments.

```sh
$ su
Password: (characters will not be shown here)
```

Install sudo using `apt install sudo`.

```sh
$ apt install sudo
```

To verify if sudo is installed successfully, run `dpkg -l | grep sudo` or `sudo`

```sh
$ dpkg -l | grep sudo
```

```sh
$ sudo
# if sudo is installed, it will display a short help message
# if not, it will display a message "sudo command not found"
```

<b style="font-size:16px"> Step 2: Adding User to sudo Group </b>

Add user to sudo group by running either of the commands: `adduser <username> sudo` or `usermod -aG sudo <username>`

```sh
$ adduser <username> sudo
```

```sh
$ usermod -aG sudo <username>
```

To verify if user has been added to sudo, check the following commands below:

```sh
$ groups <username>
<username> : <username> cdrom floppy sudo audio dip video plugdev netdev bluetooth
$ getent group sudo
sudo:x:27:<username>
$ id -Gn sudo
<username> cdrom floppy sudo audio dip video plugdev netdev bluetooth
```

To make changes take effect, run `reboot` and login using your user.

```sh
$ reboot
<--->
Debian GNU/Linux 10 <hostname> tty1

<hostname> login: <username>
Password: <password>
<--->
```

To verify sudopowers of user, check the following commands below:

```sh
# It is usually used to extend your sudo password timeout, but can be used for
# determining whether you have any sudo privileges. It won't show any message if user
# has sudopowers.
$ sudo -v
[sudo] password for <username>: <password>
Sorry, user [username] may not run sudo on [hostname].
```

```sh
# It will list any sudo privileges you have.
$ sudo -l
[sudo] password for <username>: <password>
```

<b style="font-size:16px"> Step 3: Running root-Privileged Commands </b>

Run root-privileged commands via prefix `sudo`. For instance:

```sh
$ sudo apt install vim
# Vim (Vi IMproved) is a text editor. It is an improved version of vi.
$ sudo apt update
# update installed packages
```

<b style="font-size:16px"> Step 4: Configure sudo Group </b>

Create directory `/var/log/sudo`. This is where the log file will be saved.

```sh
$ sudo mkdir /var/log/sudo
```

Configure sudo in this path `/etc/sudoers.d/<filename>`. `<filename>` shall not end in `~` or contain `.`.

```sh
$ sudo vim /etc/sudoers.d/<filename>

# Why use /etc/sudoers.d/ ?

# - Typically /etc/sudoers is under control of your distribution\'s package manager.
# If you have made changes to that file and the package manager wants to upgrade it,
# you will have to manually inspect the changes and approve how they are merged into
# the new version. By placing your local changes into a file in the /etc/sudoers.d/
# directory, you avoid this manual step and upgrades can proceed automatically.
```

Edit the file `/etc/sudoers.d/<filename>`. Then, configure the new sudo rules. Just to make sure, right after `Defaults` there is a tab space.

```sh
# Limit authentication using sudo to 3 attempts (defaults to 3 anyway) in the event of an incorrect password
Defaults        passwd_tries=3

# Add a custom error message in the event of an incorrect password
Defaults        badpass_message="<custom-error-message>"

# Log all sudo commands to /var/log/sudo/<filename>
Defaults        logfile="/var/log/sudo/<filename>"

# To archive all sudo inputs & outputs to /var/log/sudo/:
# The default I/O log directory is /var/log/sudo-io
Defaults        log_input,log_output
Defaults        iolog_dir="/var/log/sudo"

# To require TTY:
# Why use tty? If some non-root code is exploited (a PHP script, for example), the requiretty option means that the exploit code won't be able to directly upgrade its privileges by running sudo.)
Defaults        requiretty

# Define secure paths
Defaults        secure_path="/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/snap/bin"
```

## SSH & UFW

<b style="font-size:16px"> Step 1: Install & Configure SSH </b>

Install openssh-server

```sh
$ sudo apt install openssh-server
```

Verify if openssh-server is installed

```
$ ssh -V
```

```
$ dpkg -l | grep sudo
```

Configure SSH in `/etc/ssh/sshd_config`

```
$ sudo vim /etc/ssh/sshd_config
```

Find and change the following lines in `/etc/ssh/sshd_config`

```
# Set-up SSH using Port 4242
#Port22 -> Port 4242

# Disable SSH login as root
#PermitRootLogin prohibit-password -> PermitRootLogin no
```

Check status of SSH

```sh
$ sudo service ssh status
```

```sh
$ sudo systemctl status ssh
```

<b style="font-size:16px"> Step 2: Install & Configure UFW (Uncomplicated Firewall)</b>

Install UFW

```sh
$ sudo apt install ufw
```

Verify if UFW is installed

```sh
$ dpkg -l | grep ufw
```

Enable UFW (firewall)

```sh
$ sudo ufw enable
```

Allow incoming connections using Port 4242

```sh
$ sudo ufw allow 4242
```

Check UFW status

```sh
$ sudo ufw status
```

<b style="font-size:16px"> Step 3: Connecting to Server via SSH</b>

SSH into your virtual machine using Port 4242. To check IP address, use command `ip addr show` or `ip a`

```sh
$ ssh <username>@<ip_address> -p 4242
```

To leave SSH connection use either of the following commands below:

```
$ logout
```

```
$ exit
```
