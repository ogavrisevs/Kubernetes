Etcd2 config
============

Get token
----------

    http https://discovery.etcd.io/new?size=2
    http https://discovery.etcd.io/dc629df6dc2b557dbfe9c8909fabbd15

Manual setup
-------------

Master
```
etcd2 -name infra0 -v \
  -advertise-client-urls=http://178.62.124.52:2379 \
  -initial-advertise-peer-urls=http://178.62.124.52:2380 \
  -listen-peer-urls=http://178.62.124.52:2380 \
  -listen-client-urls=http://178.62.124.52:2379 \
  -discovery=https://discovery.etcd.io/040d3daf1a03a6fe4ec505584c114568
```

Node01
```
etcd2 -name infra1 -v \
  -advertise-client-urls=http://46.101.73.78:2379 \
  -initial-advertise-peer-urls=http://46.101.73.78:2380 \
  -listen-peer-urls=http://46.101.73.78:2380 \
  -listen-client-urls=http://46.101.73.78:2379 \
  -discovery=https://discovery.etcd.io/040d3daf1a03a6fe4ec505584c114568
```

Systemd
-------

     sudo vi /etc/systemd/system/etcd2.service

```
[Unit]
Description=etcd2
Conflicts=etcd.service

[Service]
User=etcd
Environment=ETCD_DATA_DIR=/var/lib/etcd2
Environment=ETCD_NAME=%m
ExecStart=/usr/bin/etcd2
Restart=always
RestartSec=10s
LimitNOFILE=40000

[Install]
WantedBy=multi-user.target
```

    sudo mkdir /run/systemd/system/etcd2.service.d
    sudo vi /run/systemd/system/etcd2.service.d/20-cloudinit.conf

```
[Service]
Environment="ETCD_DISCOVERY=https://discovery.etcd.io/040d3daf1a03a6fe4ec505584c114568"
Environment="ETCD_ADVERTISE_CLIENT_URLS=http://178.62.34.94:2379,http://178.62.34.94:4001"
Environment="ETCD_INITIAL_ADVERTISE_PEER_URLS=http://178.62.34.94:2380"
Environment="ETCD_LISTEN_PEER_URLS=http://178.62.34.94:2380"
Environment="ETCD_LISTEN_CLIENT_URLS=http://0.0.0.0:2379,http://0.0.0.0:4001"
```

Start etcd2
-----------

    sudo systemctl start etcd2
    sudo systemctl enable etcd2
    sudo systemctl status etcd2
    sudo systemctl list-dependencies etcd2
    sudo journalctl -u etcd2
    sudo systemctl list-units
    sudo systemctl daemon-reload

Test etcd2 work
---------------

    etcdctl set /message Hello
    etcdctl get /message
    http http://178.62.34.94:2379/v2/keys/message
    etcdctl cluster-health
    etcdctl ls / --recursive
