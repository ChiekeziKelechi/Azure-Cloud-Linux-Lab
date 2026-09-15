# Azure VM & Linux Cloud Lab

## About This Project

This project is a practical Azure cloud lab I worked on as part of my Cloud and DevOps training.

The main goal was to get comfortable with creating and managing a virtual machine, working with Linux from the terminal, managing users and permissions, setting up a web server, working with storage, and understanding how a VM behaves when its resources are changed.

I also used this lab to understand some basic cloud concepts by actually testing them instead of just reading about them.

---

## 1. Creating the Virtual Machine

I started by creating an Ubuntu virtual machine on Microsoft Azure.

During the setup, I worked with:

- Resource groups
- Tags
- VM size
- vCPU and RAM
- OS disk
- Network interface
- Public IP address
- Private IP address
- Subnet
- SSH access

After creating the VM, I connected to it through SSH using MobaXterm and started working from the Ubuntu terminal.

![Azure VM Deployment](screenshots/Screenshot%202026-09-07%20134738.png)

---

## 2. Exploring the VM

After connecting to the VM, I used different Linux commands to understand what was running inside the machine.

Some of the commands I used were:


lscpu
free -h
df -h
lsblk
ip a
id
lscpu helped me check the CPU information.

free -h showed the available RAM and how much memory was being used.

df -h showed the available disk space and how much of it was being used.

lsblk helped me see the disks attached to the VM.

ip a showed the network interfaces and IP addresses.

id showed information about the current Linux user.

This helped me understand that a cloud VM is basically a computer in the cloud, with its own CPU, memory, storage and network connection.

##3. Linux Users, Groups and Permissions

I also practiced basic Linux user management.

I created users and learned how Linux groups and permissions work.

I used commands such as:

sudo adduser azurecloudstudent
sudo usermod -aG sudo azurecloudstudent

I learned that sudo allows a normal user to run commands that require administrator privileges.

I also worked with files and directories and practiced changing file permissions using chmod.

For example:

chmod +x filename

This gives the file execute permission.

##4. Installing Nginx

I installed Nginx on the Ubuntu VM and used it as a web server.

I first updated the package information and installed Nginx:

sudo apt update
sudo apt install nginx -y

I then checked whether the Nginx service was running:

sudo systemctl status nginx

I also tested the web server from inside the VM using:

curl localhost

This confirmed that Nginx was responding locally.

![Nginx Status](screenshots/Screenshot%202026-09-11%20104007.png)

![Nginx Test](screenshots/Screenshot%202026-09-11%20104030.png)

![Nginx Test](screenshots/Screenshot%202026-09-11%20104603.png)


##5. Accessing the Website Through the Public IP

After getting Nginx running, I allowed HTTP traffic through port 80 on the Azure VM.

I then opened the VM's public IP address in a web browser using HTTP.

The Nginx welcome page appeared in the browser.

This helped me understand the basic path of a web request:

My Browser
     ↓
Public IP Address
     ↓
Port 80
     ↓
Nginx
     ↓
Ubuntu VM


This was one of the parts of the lab that helped me understand how a web server on a cloud VM can actually be reached from the internet.

![NginxTest](screenshots/Screenshot%202026-09-11%20105705.png)

##6. VM Shutdown and Lifecycle Experiment

I also carried out a VM lifecycle experiment.

The purpose was to understand what happens when a virtual machine is started, rebooted and stopped.

I checked things such as:

Public IP
Private IP
Disk
Files and data
Installed applications

After restarting the VM, I checked the environment again to see what remained.

The operating system did not need to be reinstalled, and the installed applications and data on the persistent disk remained.

I also confirmed that Nginx was still installed and running after the VM changes.

Stop vs Reboot vs Delete

Reboot restarts the operating system while keeping the VM and its resources.

Stop/Deallocate shuts down the VM and releases its compute resources. The VM's persistent disks remain.

Delete removes the VM resource. Other resources such as disks, network interfaces or public IPs may be kept or deleted depending on how they are configured.

One thing I learned from this experiment is that stopping or restarting a VM is not the same thing as deleting the machine and its data.



##7. Additional Storage

I also worked with attaching an additional disk to the VM.

After attaching the disk, I used:

lsblk

to check the block devices available on the VM.

The additional disk appeared as:

nvme1n1

while the original system disk appeared as:

nvme0n1

This was different from the sda and sdb names I had expected, which helped me understand that Linux device names can vary depending on the type of storage and VM configuration.

I also learned the difference between seeing a disk with lsblk and seeing mounted filesystems with df -h.

![Additional Storage](screenshots/Screenshot%202026-09-12%20113536.png)

![Checking Storage](screenshots/Screenshot%202026-09-14%20235931.png)



##8. Resizing the Virtual Machine

The next part of the lab was to understand compute scaling.

I resized the existing VM to give it more CPU and RAM.

Before resizing, the VM had:

2 vCPUs
3.8 GB RAM

After resizing, it had:

4 vCPUs
7.8 GB RAM

The CPU and RAM increased, but the existing operating system, applications, files and attached storage remained.

I checked Nginx again after the resize and confirmed that it was still installed and running.

This showed me that increasing the size of a VM does not mean creating a new machine or reinstalling the operating system.

![Rsizing storage](screenshots/Screenshot%202026-09-15%20000611.png)

##9. Vertical Scaling

This VM resize was an example of vertical scaling.

Vertical scaling means increasing the resources of an existing machine.

For example:


Before:
2 vCPU + 3.8 GB RAM

        ↓ Resize

After:
4 vCPU + 7.8 GB RAM


The reason for doing this would be when an application or workload needs more CPU or RAM.

Instead of creating a completely new VM, I can increase the resources of the existing VM.

![Nginx After Resize](screenshots/Screenshot%202026-09-15%20001637.png)

##10. What I Learned

This lab gave me more practical understanding of how cloud virtual machines work.

Some of the main things I learned were:

How to create and connect to an Azure VM
How CPU and RAM affect a VM
How public and private IP addresses work
How Linux users and groups work
How sudo works
How Linux file permissions work
How to install and manage Nginx
How a web server can be accessed through a public IP
How to check disks and storage from Linux
How VM shutdown and reboot affect the machine
How additional storage can be attached to a VM
How to resize a VM
How vertical scaling works

Most importantly, I got to actually test these things on a real cloud VM instead of only learning the theory.

## Conclusion

This lab gave me a better understanding of how cloud virtual machines work in practice. I was able to create and manage an Azure VM, work with Linux, manage users and permissions, install and access Nginx, work with storage, test the VM lifecycle, and resize the VM by increasing its CPU and RAM.

The biggest thing I took from this lab is understanding that a cloud VM is not just something you create and leave running. I learned how its compute, storage, networking and applications work together, and how I can manage and scale the VM as the workload changes.

This was a good hands-on step in my Cloud and DevOps learning journey.
