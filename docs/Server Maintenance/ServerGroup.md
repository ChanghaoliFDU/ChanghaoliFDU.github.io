---
layout: default
title: Build Servers Group
parent: Servers Maintenance
nav_order: 2
---


# 搭建计算机群
{: .no_toc }
<details open markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
1. TOC
{:toc}
</details>

## 0. 目的：

---

`n0`:  储存/管理用户名/用户文件。

`n1-nx`:  计算节点，共享`n0`主节点的软件、用户、文件。

## 1. 准备工作：

- 保证`n0`主节点的稳定性/可靠性。
   建议`n0`使用raid 1的两硬盘做系统盘，raid 5的三块硬盘做存储盘，稳定性较子节点更高。（当前1080Ti和2080Ti集群都仅为1块raid 1硬盘做系统盘，1块raid 5做存储，即主子节点架构相同）

- 主节点`n0`与子节点`nx`之间确保低延迟的通信（彼此可ping通，通过ssh到彼此账户验证)
   `n0`与`nx`的`/etc/hosts`文件中都有彼此的IP地址和hostname，目的是改IP登录为hostname登录
   ```shell
   vim /etc/hosts #键入下面这行
   192.168.1.xxx   XXX   #xxx=2:256, XXX为任意名称如：n1、n1-2080 
   ```

## 2. 安装 NFS 服务

---

NFS(Network File System, 网络文件服务)是一种分布式文件系统协议， 允许客户端主机像访问本地存储一样访问服务器文件

- 在`n0`主节点创建共享文件夹
```shell
	sudo mkdir /home/home_public    #计算集群内所有用户的账户及文件都创建在此文件夹下。
	sudo mkdir /home/software_public # 计算集群内所用到的软件都创建在此文件夹下。
```

### 在`n0`主节点设置 NFS 服务器

```shell
    sudo apt install nfs-kernel-server
    
    sudo vim /etc/idmapd.conf #键入下面一行
    Domain=yanggroup  #这里可以随便起名字
    
    sudo vim /etc/exports #键入下面四行
    /home/home_public 10.158.145.0/24(rw,no_root_squash)
    /home/home_public 192.168.1.0/24(rw,no_root_squash)
    /home/software_public 10.158.145.0/24(rw,no_root_squash)
    /home/software_public 192.168.1.0/24(rw,no_root_squash)
    # 允许这些 IP 主机 mount 该磁盘 , 10.158.145.0 代表 ip 地址为10.158.145.x 的ip地址都被允许
    # 10.158.145.0: 化学楼 B3 层的 IP 网段, 192.168.1.0: 内网地址
    
	sudo systemctl restart nfs-server
```

### 设置`nX`子节点的NFS 客户端

```shell
	# 挂载硬盘
	sudo mkdir /home/home_public /home/software_public
	
	sudo apt install nfs-common
	
	sudo vim /etc/idmapd.conf #键入下面这行
	Domain=yanggroup #此处Domain名与上面n0主节点服务器Domain名相同
	
	sudo mount -t nfs n0:/home/home_public /home/home_public
	sudo mount -t nfs n0:/home/software_public /home/software_public
	# 自动挂载
	sudo apt install autofs
	sudo umount /home/home_public
	sudo umount /home/software_public
	
	sudo vim /etc/auto.master #键入下面这行
	/- /etc/auto.mount
	
	sudo vim /etc/auto.mount #键入下面两行
	/home/home_public -fstype=nfs,rw n0:/home/home_public
	/home/software_public -fstype=nfs,rw n0:/home/software_public
	
	sudo systemctl restart autofs
```

## 3. 安装 NIS

---

NIS(Network Information Services, 又称Sun Yellow Pages)管理计算机群的账号和密码。

### 在`n0`主节点设置 NIS 服务器

```shell
    sudo apt install nis nfs-kernel-server
    # enter the name of the domain: yanggroup
    
    sudo vim /etc/default/nis #键入下面这行
    NISSERVER=master
    
    sudo vim /etc/ypserv.securenets
    # 0.0.0.0 0.0.0.
    # add to the end: IP range you allow to access
    255.255.255.0  10.158.145.0
    
    sudo vim /var/yp/Makefile #键入下面两行
    MERGE_PASSWD=true
    MERGE_GROUP=true
    
    sudo vim /etc/hosts #键入下面这行
    127.0.0.1 localhost
    # add own IP address for NIS
    10.158.145.xx yanggroup n0
    #10.158.145.xx为n0节点的校园ip地址，yanggroup为前面Domain名
    
    sudo systemctl restart nis  # update NIS database
    sudo /usr/lib/yp/ypinit -m
    # add nis server (ctrl + D 结束输入)
```

### 在`nx`子节点设置 NIS 客户端

```shell
sudo apt install nis
# 无网络链接时，可从其他节点拷贝nis.deb文件到此节点，然后sudo dpkg -i nis.deb安装
# enter nis domain
yanggroup #之前设置的Domain名
#无法显示图像时，修改/etc/defaultdomain文件，添加 domainName

sudo vim /etc/yp.conf  #键入下面这行
# ypserver ypserver.network.com
# add to the end: [domain name] [server] [NIS server's hostname]
domain yanggroup server n0

sudo vim /etc/nsswitch.conf #键入下面四行
passwd: compat nis # line 7; add
group: compat nis # add
shadow: compat nis # add
hosts: files dns nis # add

sudo systemctl restart nis

ypwhich # 安装成功后，该命令会输出domain name, 即这里的yanggroup
# 重新登录
```

##  4. 计算机群使用

### NIS账户管理

- 在`n0`主节点添加账户
	```shell
		sudo adduser XXXXX --home /home/home_public/XXXXX # XXXXX是用户名
	```
	然后同步至各子节点
	```shell
		cd /var/yp
		sudo make
	```
- 删除账户
	```shell
		sudo userdel -r XXXXX
	```

### 免密码登陆

- 两独立主机间免密码登陆
	1. 生成密钥：`ssh-keygen -t rsa`
	2. 将登陆节点的公钥（`~/.ssh/id_rsa.pub`中的内容）添加到被登陆节点`~/.ssh/authorized_keys`中
	3. 两台主机上互有对方的公钥时，ssh或scp拷贝文件时可以免密码。

- 对于搭建好的使用NIS管理用户的计算机群
	```shell
		ssh-keygen -t rsa
		# default setting, just press Enter
		cat ~/.ssh/id_rsa.pub >>~/.ssh/authorized_keys
	```
### 修改登录信息

```shell
touch ~/.hushlogin # 关闭所有欢迎消息
cd /etc/update-motd.d # vim修改此文件夹下各文件内容
00-header # Ubuntu 版本信息
10-help-text # 网址信息
90-updates-available # 可用更新信息
```

### 重启后`ypbind`无法通信

- 硬盘没有挂载上
	- 检查硬盘没有`mount`上，`umount`共享盘后重新`mount`下试试
	- `umount`硬盘一般卡死或者提示`device is busy`
	   解决方法:
	   ```shell
		# sudo systemctl restart nfs
		sudo umount -f -l /mounted/dir
		sudo mount /the/dir/you/want/mount     /mount/dir
		sudo systemctl restart nis
		ypwhich
		# if show the name of nis master, relogin
	   ```
- `ypbind`服务没有启动
	解决方法: 启动`ypbind`
	
	```shell
		which ypbind
		/usr/sbin/ypbind
		sudo ./usr/sbin/ypbind
	```
