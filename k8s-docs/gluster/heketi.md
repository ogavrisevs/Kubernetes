Install heketi
---------------

    yum install heketi heketi-client -y
    # copy config  
    vim /etc/heketi/heketi.json

    vim /etc/passwd
      heketi:x:995:991:heketi user:/var/lib/heketi:/bin/bash  

    su heketi
    ssh-keygen
    # add key to nodes
    $master /var/lib/heketi/.ssh/id_rsa.pub -> node$ /root/.ssh/authorized_keys

    systemctl enable heketi
    systemctl start heketi
    export HEKETI_CLI_SERVER=http://localhost:8081
    heketi-cli topology load --json=topo.json

Check heketi
---------------

    heketi-cli volume create --size=10 --replica=0
    gluster volume list
