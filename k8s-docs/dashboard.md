
K8 dashboard UI
===============

    kubectl create namespace kube-system

    git clone https://github.com/kubernetes/dashboard.git
    vim dashboard/src/deploy/kubernetes-dashboard.yaml
      #uncomment (no dns on system)
      - --apiserver-host=http://master.example.com:8080

      #uncomment (dns running )
      - --apiserver-host=http://46.101.96.173:8080

    kubectl --namespace=kube-system describe service kubernetes-dashboard
    kubectl exec busybox -- nslookup kubernetes-dashboard.kube-system.svc.example.com
    kubectl describe -f dashboard/src/deploy/kubernetes-dashboard.yaml
    kubectl delete -f dashboard/src/deploy/kubernetes-dashboard.yaml
