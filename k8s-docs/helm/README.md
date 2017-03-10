Install helm
------------

    curl http://storage.googleapis.com/kubernetes-helm/helm-v2.0.0-beta.1-linux-amd64.tar.gz -o  helm-linux-amd64.tar.gz
    tar -zxvf helm-linux-amd64.tar.gz
    mv linux-amd64/helm /usr/local/bin/helm

Install helm (canary)
---------------------

    curl http://storage.googleapis.com/kubernetes-helm/helm-canary-linux-amd64.tar.gz -o helm-canary-linux-amd64.tar.gz
    tar -zxvf helm-canary-linux-amd64.tar.gz
    mv linux-amd64/helm /usr/local/bin/helm

Install helm from source
------------------------

    wget https://storage.googleapis.com/golang/go1.7.1.linux-amd64.tar.gz
    export PATH=$PATH:/usr/local/go/bin
    export GOROOT=$HOME/go
    export PATH=$PATH:$GOROOT/bin
    tar -C /usr/local -xzf go1.7.1.linux-amd64.tar.gz
    curl https://glide.sh/get | sh

Install tiller
--------------

    # auth. with ServiceAccount (notworking )
    helm init
    or

    mkdir /etc/kubernetes
    #copy token and master ip
    vim /etc/kubernetes/tiller.kubeconfig
    vim /root/tiller-do.yaml
    kubectl create -f tiller-do.yaml


Remove tiller
-------------

    kubectl delete deploy tiller-deploy --namespace=kube-system

Set up helm
------------

    helm init --client-only
    helm version --host 10.20.8.4:44134

Check
-------

    curl -v 10.20.31.2:44135/liveness
    export HELM_HOST=10.20.97.4:44135
    or
    helm list --host 10.20.97.4:44134
