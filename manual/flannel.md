flannel Configuration
=====================

    sudo mkdir /etc/flannel
    sudo vi /etc/flannel/options.env

```
FLANNELD_IFACE=178.62.34.94
FLANNELD_ETCD_ENDPOINTS=http://178.62.34.94:2379
```

    sudo mkdir /etc/systemd/system/flanneld.service.d/
    sudo vi /etc/systemd/system/flanneld.service.d/40-ExecStartPre-symlink.conf

````
[Service]
ExecStartPre=/usr/bin/ln -sf /etc/flannel/options.env /run/flannel/options.env

sudo mkdir /etc/systemd/system/docker.service.d
sudo vi /etc/systemd/system/docker.service.d/40-flannel.conf

[Unit]
Requires=flanneld.service
After=flanneld.service
```

    etcdctl set /coreos.com/network/config '{ "Network": "192.168.1.0/24" }'
