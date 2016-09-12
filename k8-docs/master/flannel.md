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

Check:

    etcdctl get atomic.io/network/config

Config:

    vim /etc/sysconfig/flanneld
    FLANNEL_ETCD="http://master.example.com:2379"
    FLANNEL_ETCD_KEY="/atomic.io/network"

Start:

    systemctl enable flanneld
    systemctl start flanneld
    systemctl reboot

Check2 (2x.nodes):

    docker run -it fedora:latest bash
    yum -y install iproute iputils
    setcap cap_net_raw-ep /usr/bin/ping
    ip -4 a l eth0 | grep inet

    ping first container with second one
