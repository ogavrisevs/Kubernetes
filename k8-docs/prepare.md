
Preapare
============

Update Sys.
------------

    yum update
    yum install -y epel-release
    yum install -y vim httpie htop git

Add hosts
----------

    vim /etc/hosts
      139.59.213.115 master master.example.com
      139.59.213.138 node1 node1.example.com

Install docker-engine (from yum extras)
----------------------------------------

    yum install -y docker-1.10.3
    systemctl start docker
    systemctl enable docker
