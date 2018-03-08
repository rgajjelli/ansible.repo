ansible-playbook variables-subst-debug/varibales-extravars.yaml

# remove telnet package
ansible centos7-dev -s -m yum -a "name=telnet state=absent"

ansible-playbook variables-subst-debug/variable-telnet-package.yaml --extra-vars "myhosts=centos7-dev gather=yes pkg=telnet"
