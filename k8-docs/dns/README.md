SkyDNS
--------------

[Kube-Dns](https://github.com/kubernetes/kubernetes/blob/master/build/kube-dns/README.md)

Check for updates  :

    git clone https://github.com/kubernetes/kubernetes.git kubernetes-src
    /root/kubernetes-src/cluster/addons/dns/skydns-rc.yaml.sed
    /root/kubernetes-src/cluster/addons/dns/skydns-svc.yaml.sed

Create config:

    mkdir /root/dns/
    vim /root/dns/skydns-rc.yaml
    vim /root/dns/skydns-svc.yaml

Env.var (opt.):

    export DNS_SERVER_IP="10.0.0.10"
    export DNS_DOMAIN="example.com"
    export DNS_REPLICAS=1

Create service :

    kubectl create -f /root/dns/skydns-rc.yaml
    kubectl create -f /root/dns/skydns-svc.yaml

Check :

  Start example `dns-busybox.yaml`

On `kubelet` agents:

    vim /etc/kubernetes/kubelet
    KUBELET_ARGS="--cluster-dns=10.254.8.8 --cluster-domain=example.com"
    systemctl restart kubelet
    systemctl status kubelet
