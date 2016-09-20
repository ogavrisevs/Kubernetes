
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
