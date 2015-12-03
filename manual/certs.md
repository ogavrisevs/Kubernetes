Generate Certs
==============

Create a Cluster Root CA
------------------------
    openssl genrsa -out ca-key.pem 2048
    openssl req -x509 -new -nodes -key ca-key.pem -days 10000 -out ca.pem -subj "/CN=kube-ca"

    nano >> openssl.cnf

Generate the API Server Keypair
--------------------------------

    openssl genrsa -out apiserver-key.pem 2048
    openssl req -new -key apiserver-key.pem -out apiserver.csr -subj "/CN=kube-apiserver" -config openssl.cnf
    openssl x509 -req -in apiserver.csr -CA ca.pem -CAkey ca-key.pem -CAcreateserial -out apiserver.pem -days 365 -extensions v3_req -extfile openssl.cnf


Generate the Kubernetes Worker Keypair
--------------------------------------

    openssl genrsa -out worker-key.pem 2048
    openssl req -new -key worker-key.pem -out worker.csr -subj "/CN=kube-worker"
    openssl x509 -req -in worker.csr -CA ca.pem -CAkey ca-key.pem -CAcreateserial -out worker.pem -days 365

Generate the Cluster Administrator Keypair
-------------------------------------------

    openssl genrsa -out admin-key.pem 2048
    openssl req -new -key admin-key.pem -out admin.csr -subj "/CN=kube-admin"
    openssl x509 -req -in admin.csr -CA ca.pem -CAkey ca-key.pem -CAcreateserial -out admin.pem -days 365


Configure Service Components
-----------------------------

    sudo mkdir /etc/kubernetes
    sudo mkdir /etc/kubernetes/ssl

    sudo vi /etc/kubernetes/ssl/ca.pem
    sudo vi /etc/kubernetes/ssl/apiserver.pem
    sudo vi /etc/kubernetes/ssl/apiserver-key.pem

    sudo chmod 600 /etc/kubernetes/ssl/*-key.pem
    sudo chown root:root /etc/kubernetes/ssl/*-key.pem
