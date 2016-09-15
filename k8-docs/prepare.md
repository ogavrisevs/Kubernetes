
Prepare
============

Update Sys.
------------

    yum update
    yum install -y epel-release
    yum install -y vim httpie htop git tree telnet

Add hosts
----------

    vim /etc/hosts
    46.101.188.163 master master.example.com
    139.59.208.61  node1 node1.example.com

Install docker-engine (from yum extras) (for k8 v1.2 !)
-----------------------------------------------------------

    yum install -y docker-1.10.3
    systemctl start docker
    systemctl enable docker

Install docker-engine (from yum extras) (for k8 > v1.3 )
-----------------------------------------------------------

    vim /etc/yum.repos.d/docker.repo
    [dockerrepo]
    name=Docker Repository
    baseurl=https://yum.dockerproject.org/repo/main/centos/7/
    enabled=1
    gpgcheck=1
    gpgkey=https://yum.dockerproject.org/gpg

    yum install -y docker-engine
    systemctl start docker
    systemctl enable docker
