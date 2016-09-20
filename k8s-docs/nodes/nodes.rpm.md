K8 nodes
=========

Install flannel
---------------

Install:

    yum install -y flannel

Config:

    vim  /etc/sysconfig/flanneld
    FLANNEL_ETCD="http://master.example.com:2379"
    FLANNEL_ETCD_KEY="/atomic.io/network"

Start :

    systemctl start flanneld
    systemctl enable flanneld


Install k8 apps
----------------

Install kublet:

    yum install -y kubernetes-node

Config:

    vim /etc/kubernetes/config
    KUBE_MASTER="--master=http://master.example.com:8080"

    vim /etc/kubernetes/kubelet
    KUBELET_ADDRESS="--address=0.0.0.0"
    KUBELET_HOSTNAME="--hostname-override=node1.example.com"
    KUBELET_ARGS="--register-node=true"
    KUBELET_API_SERVER="--api_servers=http://master.example.com:8080"

Start :

    systemctl enable kube-proxy kubelet
    systemctl start kube-proxy kubelet
