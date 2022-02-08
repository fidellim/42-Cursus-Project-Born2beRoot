# Born2beRoot Evaluation Answer

## Project Overview

- How a virtual machine works.
    - A software that allows one to run an operating system within another operating system. (e.g. Virtualbox and VMware).
    - A virtual machine is a computer file, typically called an image, which behaves like an actual computer. It can run in a window as a separate computing environment, often to run a different operating system or even to function as the user's entire computer experience. 
    - The virtual machine is partitioned from the rest of the system, meaning that the software inside a VM cannot interfere with the host computer's primary operating system.

- Their choice of operating system.
    - Debian
- The basic differences between CentOS and Debian.

|  Paramaters  |  CentOS  |  Debian  |
|  :-:  |  ----------------------------  |  ---------------------------------------------  |
|  Community  |  Supported by Red Hat community  |  Supported by Debian individuals  |
|  Market Presence  |  Large market due to its user-friendly nature  |  Lacks market due to its terminal end usage  |
|  Architecture Support  | Doesn't come with multiple architecture support | Has multiple architecture support |
|  Release Cycle  | New updates and upgrades take time, thus making it stable | Has a release cycle of 2 years |
|  Version Upgrade  | Better to install a new CentOS version rather than go for upgrading the older version as it is cumbersome | Can be easily upgraded from one stable version to another |
|  User Interface | Has complicated GUI | Has user-friendly apps and GUI |
|  Package Manager  | Uses Yum | Uses Apt |
|  Package Number  | Has limited packages | Has vast amount of packages in its default repository |

    - CentOS is the most popular distribution when it comes to server environments.
    - Debian is by far the most secure and stable Linux distribution available to date. It has a bug tracking system to resolve issues.
    - If you use these distributions as a server, you should select CentOS as long-term support and updates. Debian is mostly preferred by experienced users who want to work as an admin. In contrast, a business person mostly prefers CentOS who wants a stable and secure Linux distribution for their applications.

- The purpose of virtual machines.
    - Building and deploying apps to the cloud.
    - Trying out a new operating system (OS).
    - Spinning up a new environment to make it simpler and quicker for developers to run dev-test scenarios.
    - Backing up your existing OS.
    - VMs allow you to more easily scale your apps by adding more physical or virtual servers to distribute the workload across multiple VMs.
- `If the evaluated student chose CentOS: what SELinux and DNF are.`
- If the evaluated student chose Debian: the difference between Aptitude and Apt, and what APPArmor is.
    - Aptitiude VS APT
        - Aptitude is a high-level package manager while APT is lower-level package manager which can be used by other higher-level package managers.
        - Aptitude has an interface while apt doesn't.
    - AppArmor
        - is a Linux kernel security module that allows the system administrator to restrict programs' capabilities with per-program profiles.
        - allows you to define a security policy that provides granular permissions for all users, programs, processes, files, and devices.
        - provides the flexibility to define policies only on those processes/scripts you like.
        - enforces protection over objects as per configuration. That means, the application "immunizes" other apps one by one. By default, something that has not been previously set as "protected" is, by all means, vulnerable.
        - AppArmor might not be considered as efficient and secure as SELinux, for example, but it has an easier interface and is more user-friendly. For someone who is not all-accustomed to system administration, it becomes a great alternative for managing access control.

## Simple Setup

- Ensure that the machine does not have a graphical environment at launch.
    - A password will be requested before attempting to connect to this machine. Finally, connect with a user with the help of the student being evaluated. This user must not be root.
- Pay attention to the password chosen, it must follow the rules imposed in the subject.
- Check that the UFW service is started with the help of the evaluator.
    - `sudo ufw status`
- Check that the SSH service is started with the help of the evaluator.
    - `sudo systemctl status ssh`
    - `sudo service ssh status`
- Check that the chosen operating system is Debian or CentOS with the help of the evaluator.
    - `head -n 2 /etc/os-release`

## User

The subject requests that a user with the login of the student being evaluated is present on the virtual machine. Check that it has been added and that it belongs to the “sudo” and “user42” groups.
Make sure the rules imposed in the subject concerning the password policy have been put in place by following the following steps.
First, create a new user. Assign it to a password of your choice, respecting the subject rules. The student being evaluated must now explain to you how they were able to set up the rules requested in the subject on their virtual machine.
Normally there should be one or two modified files. If there is any problem, the evaluation stops here.

- Now that you have a new user, ask the student being evaluated to create a group named “evaluating” in front of you and assign it to this user. Finally, check that this user belongs to the “evaluating” group.
- Finally, ask the student being evaluated to explain the advantages of this password policy, as well as the advantages and disadvantages of its implementation. Of course, answering that it is because the subject asks for it does not count.

## Hostname and Partitions

Check that the hostname of the machine is correctly formatted as follows: login42 (login of the student being evaluated).
Modify this hostname by replacing the login with yours, then restart the machine. If on restart, the hostname has not been updated, the evaluation stops here.
You can now restore the machine to the original hostname.
Ask the student being evaluated how to view the partitions for this virtual machine.
Compare the output with the example given in the subject.
Please note: If the student evaluated makes the bonuses, it will be necessary to refer to the bonus example
This part is an opportunity to discuss the scores! The student being evaluated should give you a brief explanation of how LVM works and what it is all about. If something does not work as expected or is not clearly explained, the evaluation stops here.

## Sudo

Check that the “sudo” program is properly installed on the virtual machine.
The student being evaluated should now show assigning your new user to the “sudo”
Group.
The subject imposes strict rules for sudo. The student being evaluated must first explain the value and operation of sudo using examples of their choice. In a second step, it must show you the implementation of the rules imposed by the subject.
Verify that the “var/log/sudo” folder exists and has at least one file. Check the contents of the files in this folder, you should see a history of the commands used with sudo. Finally, try to run a command via sudo. See if the file(s) in the “var/log/sudo” folder has been updated.

## UFW

Check that the “UFW” program is properly installed on the virtual machine.
Check that it is working properly.
The student being evaluated should explain to you basically what UFW is and the value
of using it.
List the active rules in UFW. A rule must exist for port 4242.
Add a new rule to open port 8080. Check that this one has been added by listing the active rules.
Finally, delete this new rule with the help of the student being evaluated.

## SSH

Check that the SSH service is properly installed on the virtual machine
Check that it is working properly.
The student being evaluated must be able to explain to you basically what SSH is and
the value of using it.
Verify that the SSH service only uses port 4242.
The student being evaluated should help you use SSH in order to log in with the newly created user. To do this, you can use a key or a simple password. It will depend on the student being evaluated. Of course, you have to make sure that you cannot use SSH with the “root” user as stated in the subject.

# Script Monitoring

How their script works by showing you the code.
What “Cron” is.
How the student being evaluated set up their script so that it runs every 10 minutes from when the server starts
Once the correct functioning of the script has been verified, the student being evaluated should ensure that this script runs every minute. You can run whatever you want to make sure the script runs with dynamic values correctly. Finally, the student being evaluated should make the script stop running when the server has started up, but without modifying the script itself. To check this point, you will have to restart the server one last time. At startup, it will be necessary to check that the script still exists in the same place, that its rights have remained unchanged, and that it has not been modified.

## Bonus

Setting up partitions is worth 2 points.
Setting up WordPress, only with the services required by the subject, is worth 2 points.
The free choice service is worth 1 point.
Verify and test the proper functioning and implementation of each extra service.
For the free choice service, the student being evaluated has to give you a simple explanation about how it works and why they think it is useful. Please note that NGINX and Apache2 are prohibited.
