
++++++ Mislenious ++++++
### Create RPM & upload it to Nexus

1. With Dockerfile - create rpm
ref: https://tecadmin.net/create-rpm-of-your-own-script-in-centosredhat/#
2. Upload RPM to Nexus
curl -v -u admin:admin123 --upload-file slashbin-1.0-1.x86_64.rpm http://127.0.0.1:8081/nexus/content/repositories/releases/com/github/diegopacheco/sandbox/devops/fpmtest/1.0.1/fpmtest-1.0.1.rpm



++++++++ Ansible - Master ++++++++++

cat /etc/ansible/hosts
> ansible all -m ping
> ansible all -a "ls -alrt du -sg /opt"
> ansible all -a "ls -alrt df -h"
> ansible all -a "ls -alrt /home/ansible"
> ansible all -a "cat /var/log/messages"    *** error ***
> sudo ansible all -a "cat /var/log/messages" *** error ***

?? how ansible to run privileged commands ??
>  ansible all -s -a "cat /var/log/messages | tail -1000f"
>  ansible local -s -a "cat /var/log/messages | tail -1000f"  *** master ansible server ***
>  ansible centos7 -s -a "cat /var/log/messages | tail -1000f"
>  ansible centos7-dev -s -a "cat /var/log/messages | tail -1000f"

mkdir -p /tmp/ansible
echo "Hello file - ansible" >> /tmp/ansible/ansible-file.txt

?? how to copy files from master ansible server to clients ??
ansible centos7 -m copy -a "src=/tmp/ansible/ansible-file.txt dest=/tmp/ansible-file.txt"
ansible centos7-dev -m copy -a "src=/tmp/ansible/ansible-file.txt dest=/tmp/ansibledev-file.txt"

?? Install Packages on remote hosts??
ansible centos7 -s -m yum -a "name=ntp state=latest"
s=super power (sudo)
m=modules
a=attributes
ansible centos7 -s -m yum -a "name=httpd state=latest"

?? Remove packages ??
ansible centos7 -s -m yum -a "name=ntp state=absent"

?? Create user in remote hosts ??
ansible all -s -m user -a "name=httpd"

ansible centos7-dev -s -m user -a "name=opsadmin"
ansible all -s -m user -a "name=opsadmin"

?? Remove user from remote hosts ??
ansible centos7-dev -s -m user -a "name=opsadmin state=abscent"

?? gathering facts ??
ansible centos7-dev -m setup
ansible centos7-prod -m setup
ansible all -m setup -a 'filter=*ipv4*'
ansible centos7-prod -m setup --tree facts
