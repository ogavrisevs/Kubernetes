K8 Master
===========

Add apiserver, controller-manager, scheduler pods
-------------------------------------------------

Add Pod config :

    mkdir -p /etc/kubernetes/manifests
    vim /etc/kubernetes/manifests/apiserver.pod.json
    vim /etc/kubernetes/manifests/controller-manager.pod.json
    vim /etc/kubernetes/manifests/scheduler.pod.json

Install k8.master (from source release)
---------------------------------------

Config `kubelet`:

    vim /etc/kubernetes/kubelet
    KUBELET_ADDRESS="--address=0.0.0.0"
    KUBELET_HOSTNAME="--hostname-override=master.example.com"
    KUBELET_API_SERVER="--api_servers=http://master.example.com:8080"
    KUBELET_ARGS="--config=/etc/kubernetes/manifests --register-node=true"

Install `kubelet`:

    curl -L https://github.com/kubernetes/kubernetes/releases/download/v1.3.6/kubernetes.tar.gz -o kubernetes.tar.gz
    tar -xvzf kubernetes.tar.gz
    tar -xvzf /root/kubernetes/server/kubernetes-server-linux-amd64.tar.gz
    mv /root/kubernetes/server/bin/kubelet /usr/bin/kubelet

Install `kubectl` :

    mv /root/kubernetes/server/bin/kubectl /usr/bin/kubectl

Set up systemd for `kubelet`:

    git clone https://github.com/kubernetes/contrib.git
    cp -v /root/contrib/init/systemd/kubelet.service /usr/lib/systemd/system/kubelet.service

    systemctl enable kubelet.service
    systemctl start kubelet.service
    systemctl status kubelet.service

Check:

    http 0.0.0.0:8080
    kubectl get componentstatuses
    curl -s http://localhost:8080/api
