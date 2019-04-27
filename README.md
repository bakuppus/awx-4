Hardware requirements

========  requirements ============ :

    RAM: at leasts 4GB of memory.
    CPU: at least 2 cpu cores.
    HDD: at least 20GB of space.
    Running Docker, Openshift, or Kubernetes.
    If you choose to use an external PostgreSQL database, please note that the minimum version is 9.4.

Install the dependency package

Step 1: Disable SElinux and reboot the server.

You run the following command to replace enforcing with disabled in the config file of SElinux.

# sed -i 's|SELINUX=enforcing|SELINUX=disabled|g' /etc/selinux/config

And then reboot the server:

# reboot

Step 2: Install the dependency packages required for AWX.

You run the following commands in turn:

# yum -y install epel-release
# yum -y install git gcc gcc-c++ lvm2 bzip2 gettext nodejs yum-utils device-mapper-persistent-data ansible python-pip

Step 3: Install Docker-CE.

First, you run the command below to remove the old version of Docker on the server (if any).

# yum -y remove docker docker-common docker-selinux docker-engine

Next, you add the Docker-CE repository to the server.

# yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo

And now you run the command below to install Docker-CE.

# yum -y install docker-ce

After installing Docker-CE, you enable and start the docker service.

# systemctl start docker && systemctl enable docker

AWX require docker python module and you can install it via pip.

# pip install -U docker-py

Then run the following command to check the installed version.


Install Ansible AWX on CentOS 7

Step 1: Clone AWX from the repository.
git clone  https://github.com/bakuppus/awx-4.git

Step 2: Install
$ cd /opt/
$ cd awx-4
$ kubectl create -f StorageClass.yaml 
$ cd /opt/awx-4/installer
$ ansible-playbook -i inventory install.yml 

AWX user: admin/password

That's it
