

    vim /root/busybox.yaml
    kubectl create -f /root/busybox.yaml
    kubectl get pods busybox
    kubectl exec busybox -- nslookup frontend
    kubectl exec busybox -- nslookup frontend.default.svc.example.com
