deploy-cent
===========

Deploying Django with Nginx, Gunicorn, Virtualenv, Supervisor and MySQL on CentOS

### [Configuring Network in CentOS Virtual Box](http://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/)

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
5. `cp Nginx.repo /etc/yum.repos.d/`
6. `yum update`

### MySQL
7. `yum install mysql-server`
8. `chkconfig mysqld on`
9. `service mysqld start`
10. `mysqladmin -u root password '...'`

    CREATE USER 'django'@'localhost' IDENTIFIED BY '...';
    CREATE DATABASE `django` CHARACTER SET utf8 COLLATE utf8_general_ci;
    GRANT ALL ON `django`.* TO `django`;
    FLUSH PRIVILEGES;

### pip
11. `curl -O https://pypi.python.org/packages/source/s/setuptools/setuptools-1.3.2.tar.gz`
12. `tar xzvf setuptools-1.3.2.tar.gz && cd setuptools-1.3.2`
13. `python setup.py install --force --verbose`
14. `cd ..`
15. `curl -O https://pypi.python.org/packages/source/p/pip/pip-1.4.1.tar.gz`
16. `tar xzvf pip-1.4.1.tar.gz && cd pip-1.4.1`
17. `python setup.py install --force --verbose`
18. `cd ..`

