---
layout: default
title: Local Web
parent: Servers Maintenance
nav_order: 1
---

# Ubuntu 20.04版本配置静态ip分配主子节点

通过交换机连接到主节点`n0`

- 主节点连接到互联网，子节点通过交换机连接主节点
- 主节点网络设置
   1. 先通过`ifconfig`确认网络端口的连接 
      
      <img src="/Figures/ifconfig.png" alt="ifconfig" style="zoom:100%;" />
      
      如上图情况，`eno1`网口连接外网，`enp4s0f1`网口连接交换机，并作为网络输入口。
      
   2. 修改网络配置文件
  ```shell
     cd /etc/netplan
  ```
  接下来查看.yaml文件名，并修改该文件
  ```shell
  sudo vim 01-network-manager-all.yaml
  
  # Let NetworkManager manage all devices on this system
  network:
     version: 2
     renderer: NetworkManager
     ethernets:  # 注意缩进是必需的
             enp4s0f1:  # 此处为交换机连接网口
               dhcp4: false  # 关闭自动获取ip
               addresses: [192.168.1.1/24]  # 设置本机ip地址
               nameservers:
                       addresses: [202.120.224.26] # 复旦通用DNS
   ```
  修改完成后：
  ```shell               
      sudo netplan apply
   ```

- 子节点网络设置
  ```shell
  cd /etc/netplan
  ```
  接下来查看.yaml文件名，并修改该文件
  ```shell
  sudo vim 01-network-manager-all.yaml
  # Let NetworkManager manage all devices on this system
  network:
    version: 2
    renderer: NetworkManager
    ethernets:  # 注意缩进是必需的
            enp4s0f1:  # 此处为交换机连接网口
              dhcp4: false  # 关闭自动获取ip
              addresses: [192.168.1.101/24]  # 设置本机ip地址，可选范围192.168.1.2-254
              gateway4: 192.168.1.1 # 此处为n0主节点的静态ip地址，并且注意没有方括号
              nameservers:
                      addresses: [202.120.224.26] # 复旦通用DNS
  ```                  
  修改完成后：
  ```shell               
  sudo netplan apply
  ```
