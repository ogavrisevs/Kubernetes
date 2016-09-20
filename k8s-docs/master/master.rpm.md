Install k8.master (from rpm repo)
-----------------------------

Install :

    yum install -y kubernetes-node

    vim /etc/kubernetes/config

Config `kubectl`:

    KUBE_MASTER="--master=http://master.example.com:8080"

Config `kublet`:

    vim /etc/kubernetes/kubelet
    KUBELET_ADDRESS="--address=0.0.0.0"
    KUBELET_HOSTNAME="--hostname-override=master.example.com"
    KUBELET_ARGS="--register-node=true"
    KUBELET_API_SERVER="--api_servers=http://master.example.com:8080"
    KUBELET_ARGS="--config=/etc/kubernetes/manifests"
    KUBELET_POD_INFRA_CONTAINER="--pod-infra-container-image=registry.access.redhat.com/rhel7/pod-infrastructure:latest"

Check:

    kubectl get componentstatuses

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
