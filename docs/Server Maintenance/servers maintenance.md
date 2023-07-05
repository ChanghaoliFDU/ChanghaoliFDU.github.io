---
layout: default
title: Servers Maintenance
tag: maintenance servers
has_children: true
nav_order: 4
---

# Maintenance of Servers in Reserach Group
{: .no_toc }
This is a guide mostly based on Ubuntu20.0.

<details open markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
1. TOC
{:toc}
</details>

---

## 1. Create Users

This is only a tutorial for <font color=MediumVioletRed>one server</font>. 
The guide for adding users in a computer group is [here](/ServerGroup.md).
 
### Normal Users

```shell
sudo adduser peter     # Add a user with the name peter
sudo deluser peter     # Delete the user with the name peter
sudo deluser --remove-home peter   # Delete the user peter and remove '/home/peter' directory
```

### Super Users(Administrators)

After adding a user, one can make it a super user. 

```shell
sudo vi /etc/sudoers
```
And then add the following sentence under `root ALL=(ALL:ALL) ALL` in the sudoers file.
```shell
peter ALL=(ALL:ALL) ALL
```
### Bug Fix

If other users can visit your personal files, change the permission of main directory.
```shell
  chmod -R o-rwx ~
```


## 2. Install Softwares

### Edit .bashrc

 - After the software is installed, one can edit the `.bashrc` file to export the path.
```shell
sudo vim ~/.bashrc
```
and add the following sentence to the end of the `.bahsrc` file.
```shell
export PATH=$PATH:/***/julia-1.6.1-linux-x86_64/julia-1.6.1/bin
# This is an example for julia.
# *** is the Absolute Path of the 'bin' directory.
```
Save changes by pressing `ESC`,`:wq!` in turns.
And source the `.bashrc` file.
```shell
source ~/.bashrc 
```
 - Change the color scheme of the terminal 
 Add the following sentence to `.bashrc` file.
 ```shell
  PS1='${debian_chroot:+($debian_chroot)}[\d \t]\[\033[01;32m\]\u@\h\[\033[00m\]:\[\033[01;34m\]\w\[\033[00m\]\$ '
 ```
 where `${debian_chroot:+($debian_chroot)}` is meaningless.

 The main body is `\u@\h:\w\$` where `\u` means `username`, `\h` means `hostname` and `\w` means the `working directory`.
 `[\d \t]` stands for *day* and *time*. 

 Color setting: `\[\033[XXm\]` and XX is the code for the chosen color.

 |  Color |  Code  |  Color | Code |
 | ---- | ---- | ---- | ---- |
 |  Default  |  00 |  Yellow    |  33  |
 |   Black   |  30 |   Blue    |   34 |
 |   Red   |  31  |   Purple   |  35  |
 |   Green   | 32 |   Cyan   |  36  |

## 3. Change Hostname of A Server

```shell
sudo vi /etc/hostname # Change a new hostname
sudo vi /etc/hosts
127.0.1.1 newhostname # If only the hostname in /etc/hostname is changed, there would be a warning.
```

