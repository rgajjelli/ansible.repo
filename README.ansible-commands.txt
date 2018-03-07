++++++++ Master ++++++++++

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
ansible centos7 -s -m yum -a "name=ntp state=abscent"

?? Create user in remote hosts ??
ansible centos7 -s -m user -a "name=opsadmin"

?? Remove user from remote hosts ??
ansible centos7 -s -m user -a "name=opsadmin state=abscent"
