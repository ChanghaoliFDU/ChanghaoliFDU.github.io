---
layout: default
title: Servers Maintenance
tag: maintenance servers
has_children: true
nav_order: 4
---

# Maintenance of Servers in Reserach Group

This is a guide mostly based on Ubuntu20.04.

## Create Users

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
And then add the following sentence under <root ALL=(ALL:ALL) ALL> in the sudoers file.
```shell
peter ALL=(ALL:ALL) ALL
```
