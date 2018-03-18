ansible-tomcat
===============

Oracle JDK 8 + Tomcat 8.0

See: roles/tomcat8/tasks/main.yml

Requirements
------------
systemd, firewalld, alternatives

Building
--------

sudo yum install -y epel-release
sudo yum install -y --enablerepo=epel python-pip python-paramiko
sudo pip install ansible


/etc/hosts
192.168.56.10 tomcat-server

cd ansible-tomcat; ./ansible-build.sh
http://tomcat-server:8080/
