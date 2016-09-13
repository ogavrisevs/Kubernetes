
    kubectl get pods --all-namespaces
    kubectl get service --all-namespaces
    kubectl --namespace=kube-system describe pods kube-dns-v19-ecvra
    kubectl --namespace=kube-system describe service kube-dns
    kubectl get replicationcontrollers --all-namespaces
    kubectl get ep --all-namespaces
    kubectl --namespace=kube-system describe ep
    kubectl --namespace=kube-system logs kubernetes-dashboard-2039753577-p13z9
