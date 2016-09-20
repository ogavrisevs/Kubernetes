

    vim /root/busybox.yaml
    kubectl create -f /root/busybox.yaml
    kubectl get pods busybox
    kubectl exec busybox -- nslookup frontend
    kubectl exec busybox -- nslookup frontend.default.svc.example.com


    vim /root/centos.yaml
    kubectl create -f /root/centos.yaml

      telnet  10.254.8.8 53

      dig @10.254.8.8 centos  +answer
