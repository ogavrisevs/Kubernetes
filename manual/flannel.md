flannel Configuration
=====================

Install
--------

    git clone https://github.com/coreos/flannel.git
    cd flannel
    docker run -v /home/core/flannel:/opt/flannel -i -t google/golang /bin/bash -c "cd /opt/flannel && ./build"

Manual Start
------------    

    sudo /home/core/flannel/bin/flanneld -iface=eth0 &
    sudo systemctl status flannel
    cat /run/flannel/subnet.env

Set Unit File by (coreos-cloudinit)
-----------------------------------

    sudo vi cloud-config.yaml

```
#cloud-config

coreos:
  units:
    - name: flanneld.service
      drop-ins:
        - name: 50-network-config.conf
          content: |
            [Service]
            ExecStartPre=/usr/bin/etcdctl set /coreos.com/network/config '{ "Network": "10.1.0.0/16" }'
      command: start
    - name: fleet.service
      command: start      
````

    sudo coreos-cloudinit -from-file cloud-config.yaml

    sudo systemctl start flanneld
    sudo systemctl enable flanneld
    sudo systemctl status flanneld
    sudo systemctl list-dependencies flanneld
    sudo journalctl -u flanneld
    sudo systemctl list-units
    sudo systemctl daemon-reload

Set Unit File manual
-------------------

    sudo vi /etc/systemd/system/flanneld.service.d/50-network-config.conf

```
[Service]
ExecStartPre=/usr/bin/etcdctl set /coreos.com/network/config '{"Network":"10.244.0.0/16"}'
```

Config
--------

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
````

sudo mkdir /etc/systemd/system/docker.service.d
sudo vi /etc/systemd/system/docker.service.d/40-flannel.conf

```
[Unit]
Requires=flanneld.service
After=flanneld.service
```

    etcdctl set /coreos.com/network/config '{ "Network": "192.168.1.0/24" }'
