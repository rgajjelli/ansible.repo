Ansible Installation

1. YUM Based Installation
2. PIP based Installation.

==> For both installations, common thing is EPEL repository to be installaed.

cat /etc/centos-release


master  (ansible server)  =192.168.146.199
jenkins (client01)        =192.168.146.198
minion1 (client01)        =192.168.146.201

++++  master  (ansible server)  =192.168.146.199 ++++

1. YUM Based Installation
  yum install https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm -y
  yum makecache
  yum install http://releases.ansible.com/ansible/rpm/release/epel-7-x86_64/ansible-2.4.0.0-1.el7.ans.noarch.rpm -y
  >> ansible --version
  >> yum install openssl git
  Note: Remove Ansible from the host.
  >> rpm -e ansible

2. PIP based Installation
  yum install https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm -y
  pip install ansible
  yum install python2-pip
  pip install ansible
  >> ansible --version
  >> yum install openssl git

3. ANSIBLE - Configuration

  3.1  Generic configiration changes
        /etc/ansible/ansible.cfg
          inventory =/etc/ansible/hosts
          sudo_user =root

        mv /etc/ansible/hosts /etc/ansible/hosts.org
        ** update hosts file as below **

        [local]
        localhost

        [centos7]
        192.168.146.198

        [centos7-dev]
        192.168.146.201

  3.2  user entry setup
      > adduser ansible
      > passwd ansible
      > visudo
          ansible    ALL=NOPASSWD:       ALL      (or)
          ansible   ALL=(ALL)       NOPASSWD: ALL


++++  Ansible clients  192.168.146.198/192.168.146.201 ++++

4.  On NODE/ Client servers, i.e  centos7/centos7-dev groups)

      > adduser ansible
      > passwd ansible
      > visudo
          ansible    ALL=NOPASSWD:       ALL      (or)
          ansible   ALL=(ALL)       NOPASSWD: ALL

++++  master  (ansible server)  =192.168.146.199 ++++

5.  Generate ssh-key on master server and copy it over to client servers
    ssh-keygen -t rsa -b 2048
    ssh-copy-id -i ~/.ssh/id_rsa.pub ansible@192.168.146.198
    ssh-copy-id -i ~/.ssh/id_rsa.pub ansible@192.168.146.201
    ssh-copy-id -i ~/.ssh/id_rsa.pub ansible@localhost (On the master server too!! :) )
