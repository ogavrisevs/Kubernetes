Install heketi
---------------

    yum install heketi heketi-client
    # copy config  
    vim /etc/heketi/heketi.json

    su heketi
    ssh-keygen
    # add key to nodes
    $master /var/lib/heketi/.ssh/id_rsa.pub -> node$ /root/.ssh/authorized_keys

    systemctl enable heketi
    systemctl start heketi
    heketi-cli topology load --json=topo.json

Check heketi
---------------

    heketi-cli volume create --size=10 --replica=1
    gluster volume list
