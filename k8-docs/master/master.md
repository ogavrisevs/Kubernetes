K8 Master
===========

Install etcd
-------------

    yum install -y etcd

Config:

  vim  /etc/etcd/etcd.conf
    ETCD_NAME=default
    ETCD_DATA_DIR="/var/lib/etcd/default.etcd"
    ETCD_LISTEN_CLIENT_URLS="http://0.0.0.0:2379"
    ETCD_LISTEN_PEER_URLS="http://localhost:2380"
    ETCD_ADVERTISE_CLIENT_URLS="http://0.0.0.0:2379"

Start:

    systemctl start etcd
    systemctl enable etcd

Check:

    http 127.0.0.1:2379/version
    etcdctl cluster-health

Install Flannel
----------------

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

Start :

    systemctl enable flanneld
    systemctl start flanneld
    systemctl reboot

Check2:

  2x.nodes

    docker run -it fedora:latest bash
    yum -y install iproute iputils
    setcap cap_net_raw-ep /usr/bin/ping
    ip -4 a l eth0 | grep inet

    ping first container with second one 

Install k8.master (from repo)
-----------------------------

Install :

    yum install -y kubernetes-node

    vim /etc/kubernetes/config
    KUBE_MASTER="--master=http://master.example.com:8080
    "

Config:

    vim /etc/kubernetes/kubelet
    KUBELET_ADDRESS="--address=0.0.0.0"
    KUBELET_HOSTNAME="--hostname-override=master.example.com"
    KUBELET_ARGS="--register-node=true"
    KUBELET_API_SERVER="--api_servers=http://master.example.com:8080"
    KUBELET_ARGS="--config=/etc/kubernetes/manifests"
    KUBELET_POD_INFRA_CONTAINER="--pod-infra-container-image=registry.access.redhat.com/rhel7/pod-infrastructure:latest"

Add apiserver, controller-manager, scheduler pods
-------------------------------------------------

Add Pod config :

    vim /etc/kubernetes/manifests/apiserver.pod.json
    vim /etc/kubernetes/manifests/controller-manager.pod.json
    vim /etc/kubernetes/manifests/scheduler.pod.json

Start Pods:

    systemctl enable kube-proxy kubelet
    systemctl start kube-proxy kubelet

Reboot:

    reboot

Check:

    http 0.0.0.0:8080
