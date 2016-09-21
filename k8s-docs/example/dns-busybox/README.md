

    vim /root/busybox.yaml
    kubectl create -f /root/busybox.yaml
    kubectl get pods busybox

    vim /root/centos.yaml
    kubectl create -f /root/centos.yaml

    kubectl exec busybox -- nslookup kubernetes
    kubectl exec busybox -- nslookup kubernetes.default.svc.example.com
    kubectl exec centos -- dig kubernetes.default.svc.example.com

    kubectl exec busybox -- nslookup 10-20-76-2.default.pod.example.com
    kubectl exec centos -- dig 10-20-76-2.default.pod.example.com

    yum install telnet -y
    telnet  10.254.8.8 53
