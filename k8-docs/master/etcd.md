etcd
-------------

Install:

    yum install -y etcd

Config:

    vim /etc/etcd/etcd.conf
    ETCD_NAME=default
    ETCD_DATA_DIR="/var/lib/etcd/default.etcd"
    ETCD_LISTEN_CLIENT_URLS="http://0.0.0.0:2379"
    ETCD_LISTEN_PEER_URLS="http://localhost:2380"
    ETCD_ADVERTISE_CLIENT_URLS="http://0.0.0.0:2379"

Start:

    systemctl start etcd
    systemctl enable etcd

Check:

    http 127.0.0.1:2379/version
    etcdctl cluster-health
