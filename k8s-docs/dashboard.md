K8 dashboard UI
===============

    kubectl create namespace kube-system

    git clone https://github.com/kubernetes/dashboard.git
    vim dashboard/src/deploy/kubernetes-dashboard.yaml
      #uncomment
      - --apiserver-host=http://master.example.com:8080

    kubectl create -f dashboard/src/deploy/kubernetes-dashboard.yaml

    kubectl describe -f dashboard/src/deploy/kubernetes-dashboard.yaml
    kubectl delete -f dashboard/src/deploy/kubernetes-dashboard.yaml
