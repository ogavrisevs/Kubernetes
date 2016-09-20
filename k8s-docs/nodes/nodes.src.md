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

Install k8 (`kubelet`, `kubectl`)
------------------------------------

Config `kubelet`:

    mkdir /etc/kubernetes
    vim /etc/kubernetes/kubelet
    KUBELET_ADDRESS="--address=0.0.0.0"
    KUBELET_HOSTNAME="--hostname-override=node1.example.com"
    KUBELET_API_SERVER="--api_servers=http://master.example.com:8080"
    KUBELET_ARGS="--register-node=true"

Config `kube-proxy`:

    vim /etc/kubernetes/proxy
    KUBE_MASTER="--master=http://master.example.com:8080"

Install `kubelet`, `kubectl`, `kube-proxy`:

    curl -L https://github.com/kubernetes/kubernetes/releases/download/v1.3.6/kubernetes.tar.gz -o kubernetes.tar.gz
    tar -xvzf kubernetes.tar.gz
    tar -xvzf /root/kubernetes/server/kubernetes-server-linux-amd64.tar.gz

    mv /root/kubernetes/server/bin/kubectl /usr/bin/kubectl
    mv /root/kubernetes/server/bin/kube-proxy /usr/bin/kube-proxy
    mv /root/kubernetes/server/bin/kubelet /usr/bin/kubelet

Configure `kubectl`:

    kubectl config set-cluster default-cluster --server=http://master.example.com:8080
    kubectl config set-context default-system --cluster=default-cluster --user=default-admin
    kubectl config use-context default-system


Set up systemd for `kubelet`, `kube-proxy`:

    git clone https://github.com/kubernetes/contrib.git
    cp -v /root/contrib/init/systemd/kubelet.service /usr/lib/systemd/system/kubelet.service
    cp -v /root/contrib/init/systemd/kube-proxy.service /usr/lib/systemd/system/kube-proxy.service

    systemctl enable kubelet.service
    systemctl start kubelet.service
    systemctl status kubelet.service

    systemctl enable kube-proxy
    systemctl start  kube-proxy
    systemctl status kube-proxy

Check:

    kubectl --server=http://master.example.com:8080 get nodes
