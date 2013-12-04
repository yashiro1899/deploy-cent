deploy-cent
===========

Deploying Django with Nginx, Gunicorn, Virtualenv, Supervisor and MySQL on CentOS

## [Configuring Network in CentOS Virtual Box](http://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/)

vi /etc/sysconfig/network-scripts/ifcfg-eth0

    ONBOOT=yes
    NM_CONTROLLED=no

1. `yum update`
2. `yum groupinstall "Development Tools"`
3. `yum install man`
4. `git clone https://github.com/yashiro1899/deploy-cent.git && cd deploy-cent`

## MySQL
5. `yum install mysql`

