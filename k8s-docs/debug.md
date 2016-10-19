
kubectl get
-----------

    kubectl get pods --all-namespaces
    kubectl get service --all-namespaces
    kubectl get replicationcontrollers --all-namespaces
    kubectl get ep --all-namespaces
    kubectl get pods -l run=my-nginx -o yaml

kubectl describe
-----------------

    kubectl --namespace=kube-system describe pods kube-dns-v19-ecvra
    kubectl --namespace=kube-system describe service kube-dns
    kubectl --namespace=kube-system describe ep

kubectl logs
------------

    kubectl --namespace=kube-system logs kubernetes-dashboard-2039753577-p13z9
    kubectl logs nginx

kubectl run/exe
---------------

    kubectl run curl --image=radial/busyboxplus:curl -i --tty
    kubectl exec my-nginx-3800858182-jr4a2 -- command
    kubectl exec --namespace=kube-system kube-dns-v19-6udvw -- ip a
    kubectl exec centos -i --tty -- bash
    kubectl exec --namespace=kube-system kube-dns-v19-3boaj -c kubedns -i -t -- bash

Check services
----------------

    systemctl status flanneld
    systemctl status kubelet
      journalctl -u  kubelet
    systemctl status kube-proxy
    kubectl get pods -o yaml --namespace=kube-system
    kubectl --namespace=kube-system describe pods kube-dns-v19-3boaj
    kubectl --namespace=kube-system logs  kube-dns-v19-jbl7y kubedns
    kubectl get componentstatuses


Test security
--------------

    KUBE_TOKEN=$(</etc/kubernetes/tokens/kube-proxy.token)
    curl -sSk -H "Authorization: Bearer $KUBE_TOKEN" https://master.example.com:6443
    curl -sSk -H "Authorization: Bearer OMTQveASD8Ye4WAjEPmxa3xZQrCqXS9Q" https://138.68.86.61:6443

    #Basic BASE64ENCODED(USER:PASSWORD)
    KUBE_TOKEN=$(</etc/kubernetes/tokens/kube-proxy.token)
    curl -sSk -H "Authorization: Basic dXNlcjpwYXNzd29yZA==" https://master.example.com:6443

    curl --cacert /etc/kubernetes/certs/ca.crt -u user:password https://master.example.com:6443

Service Account
----------------

    kubectl get serviceaccount
    kubectl get serviceaccount default -o yaml
