deploy-cent
===========

Deploying Django with Nginx, Gunicorn, Virtualenv, Supervisor and MySQL on CentOS

## [Configuring Network in CentOS Virtual Box](http://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/)

    [root@cent ~]# cat /etc/sysconfig/network-scripts/ifcfg-eth0
    DEVICE=eth0
    HWADDR=08:00:27:7E:78:1B
    TYPE=Ethernet
    UUID=e7da3df0-08ff-4fb0-bf49-76e9aa0dfdbc
    ONBOOT=yes
    NM_CONTROLLED=no
    BOOTPROTO=dhcp

1. `yum update`
2. `yum groupinstall "Development Tools"`
3. `yum install man`
4. `git clone https://github.com/yashiro1899/deploy-cent.git && cd deploy-cent`

## MySQL
5. `yum install mysql`

