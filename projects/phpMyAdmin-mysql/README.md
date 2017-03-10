Create (GlusterFs)
------------------

    kubectl create -f glusterfs-endpoints.yaml
    kubectl create -f glusterfs-service.yaml
    kubectl create -f glusterfs-pv.yaml

    kubectl create -f mysql-pvc.yaml
    echo "password" > password.txt
    kubectl create secret generic mysql-pass --from-file=password.txt

    kubectl create -f mysql-deployment.yaml
    kubectl create -f pmd-deployment.yaml

    rsync -avz . root@46.101.230.181:/root/phpMyAdmin-mysql

Delete
---------

    kubectl delete -f glusterfs-endpoints.yaml
    kubectl delete -f glusterfs-service.yaml
    kubectl delete -f glusterfs-pv.yaml
    kubectl delete secret mysql-pass
    kubectl delete -f mysql-pvc.yaml
    kubectl delete -f mysql-deployment.yaml
    kubectl delete -f pmd-deployment.yaml
