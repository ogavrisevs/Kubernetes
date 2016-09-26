


Create (GlusterFs)
------------------

    kubectl create -f glusterfs-endpoints.yaml
    kubectl create -f glusterfs-service.json
    kubectl create -f glusterfs-pv.yaml

    kubectl create -f mysql-pvc.yaml
    echo "password" > password.txt
    kubectl create secret generic mysql-pass --from-file=password.txt
    kubectl create -f mysql-deployment.yaml
    kubectl create -f pmd-deployment.yaml
    kubectl create -f php-deployment.yaml


Delete
---------

    kubectl delete -f local-volumes.yaml
    kubectl delete -f mysql-deployment.yaml
    kubectl delete -f php-deployment.yaml
    kubectl delete -f php-deployment.yaml
