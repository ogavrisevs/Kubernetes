K8 dashboard UI
===============

    kubectl create namespace kube-system

    git clone https://github.com/kubernetes/dashboard.git
    vim dashboard/src/deploy/kubernetes-dashboard.yaml
    kubectl create -f dashboard/src/deploy/kubernetes-dashboard.yaml

    kubectl describe -f dashboard/src/deploy/kubernetes-dashboard.yaml
    kubectl delete -f dashboard/src/deploy/kubernetes-dashboard.yaml

    kubectl get pods --all-namespaces
    kubectl --namespace=kube-system describe pods kubernetes-dashboard-4275189467-u1skx
    kubectl get replicationcontrollers --all-namespaces
    kubectl get ep --all-namespaces
    kubectl --namespace=kube-system describe ep
    kubectl --namespace=kube-system logs kubernetes-dashboard-2039753577-p13z9
