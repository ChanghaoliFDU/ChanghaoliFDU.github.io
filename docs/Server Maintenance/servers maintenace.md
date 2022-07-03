---
layout: default
title: Servers Maintenance
tag: maintenance servers
has_children: true
nav_order: 4
---

# Maintenance of Servers in Reserach Group

This is a guide mostly based on Ubuntu20.04.

## 1. Create Users

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
 
