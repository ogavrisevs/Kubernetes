Install Flannel
----------------

Install:

    yum install -y flannel

Load network cfg.:

    vim flannel-config.json
    {
      "Network": "10.20.0.0/16",
      "SubnetLen": 24,
      "Backend": {
        "Type": "vxlan",
        "VNI": 1
      }
    }

    etcdctl set atomic.io/network/config < flannel-config.json

Delete docekr bridge
--------------------

    systemctl stop docker
    ip link delete docker0
    systemctl start flanneld
    systemctl start docker

Check:

    etcdctl get atomic.io/network/config

    ip -4 a|grep inet
      inet 127.0.0.1/8 scope host lo
      inet 192.168.122.77/24 brd 192.168.122.255 scope global dynamic eth0
      inet 18.16.29.0/16 scope global flannel.1
      inet 18.16.29.1/24 scope global docker0

Config (optional):

    vim /etc/sysconfig/flanneld
    FLANNEL_ETCD="http://master.example.com:2379"
    FLANNEL_ETCD_KEY="/atomic.io/network"

Start:

    systemctl enable flanneld
    systemctl start flanneld
    systemctl status flanneld
    systemctl reboot

Check2 (2x.nodes):

    docker run -it fedora:latest bash
    yum -y install iproute iputils
    setcap cap_net_raw-ep /usr/bin/ping
    ip -4 a l eth0 | grep inet

    ping first container with second one
