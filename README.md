deploy-cent
===========

[Deploying Django with Nginx, Gunicorn, Virtualenv, Supervisor and MySQL on CentOS](http://michal.karzynski.pl/blog/2013/06/09/django-nginx-gunicorn-virtualenv-supervisor/)

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


```
CREATE USER 'django'@'localhost' IDENTIFIED BY '...';
CREATE DATABASE `django` CHARACTER SET utf8 COLLATE utf8_general_ci;
GRANT ALL ON `django`.* TO `django`;
FLUSH PRIVILEGES;
```


### pip
11. `curl -O https://pypi.python.org/packages/source/s/setuptools/setuptools-1.3.2.tar.gz`
12. `tar xzvf setuptools-1.3.2.tar.gz && cd setuptools-1.3.2`
13. `python setup.py install --force --verbose`
14. `cd ..`
15. `curl -O https://pypi.python.org/packages/source/p/pip/pip-1.4.1.tar.gz`
16. `tar xzvf pip-1.4.1.tar.gz && cd pip-1.4.1`
17. `python setup.py install --force --verbose`

### Virtualenv
18. `pip install virtualenv`
19. `mkdir /webapps && cd /webapps`
20. `virtualenv django`
21. `cd django && source bin/activate`

### Django
22. `pip install django`
23. `django-admin.py startproject taobao && cd taobao`
24. `python manage.py runserver` for test
25. `yum install python-devel mysql-devel` for next
26. `pip install MYSQL-python`
27. `python manage.py syncdb`


```
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.mysql',
        'NAME': 'django',
        'USER': 'django',
        'PASSWORD': '...',
        'HOST': '/var/lib/mysql/mysql.sock',
        'PORT': '',    # Set to empty string for default.
    }
}
```


### Application user
28. `groupadd --system webapps`
29. `useradd --system --gid webapps --home /webapps/django django`
30. `usermod -a -G users ice`

### Gunicorn
31. `pip install gunicorn`
32. `gunicorn taobao.wsgi:application` for test
33. `cp /root/deploy-cent/gunicorn_start.bash ../bin/`
34. `pip install setproctitle`

### Supervisor
35. `deactivate`
36. `pip install supervisor`
37. `mkdir -p /etc/supervisor/conf.d`
38. `cp /root/deploy-cent/taobao.supervisor.conf /etc/supervisor/conf.d/taobao.conf`
39. `mkdir /webapps/django/logs/`
40. `chown -R django:users /webapps/django`
41. `chmod -R g+w /webapps/django`
42. `echo_supervisord_conf > /etc/supervisor/supervisord.conf`
43. `vi /etc/sysconfig/iptables` open the port 9001
44. `service iptables restart`
45. `chkconfig --add supervisord`
46. `cp /root/deploy-cent/supervisord /etc/init.d/` from [prototype](https://raw.github.com/Supervisor/initscripts/master/redhat-init-mingalevme)
47. `chmod a+x /etc/init.d/supervisord`
48. `chkconfig supervisord on`

### Nginx
49. `yum install nginx`
50. `service nginx start`
51. `cp /root/deploy-cent/taobao.nginx.conf /etc/nginx/conf.d/taobao.conf`
52. `service nginx restart`
53. `vi /etc/sysconfig/iptables` open the port 80
54. `service iptables restart`

Done!

