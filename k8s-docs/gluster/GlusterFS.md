
Set Hosts
------------

  yum install htop vim -y
  vim /etc/hosts
  138.68.75.23 server1.example.com server1
  138.68.75.7  server2.example.com server2
  138.68.78.83 client1.example.com client1

  hostnamectl set-hostname [server1, server2, client1]

Install glusterfs server on nodes [server1, server2]
-----------------------------------------------------

  yum -y install epel-release
  yum -y install centos-release-gluster
  yum -y install glusterfs-server
  systemctl enable glusterd.service
  systemctl start glusterd.service

Join cluster [ server1 / server2]
----------------------------------

  gluster peer probe node-1.example.com
  gluster peer probe node-2.example.com
  gluster peer status

Create volume
--------------

  gluster volume create gluster_vol-1 replica 2 transport tcp node-1.example.com:/gluster_vol-1 node-2.example.com:/gluster_vol-1 force
  gluster volume start gluster_vol-1

  gluster volume set testvol auth.allow client1.example.com
  gluster volume set testvol auth.allow 138.68.78.83


Prepare client
--------------

  yum -y install glusterfs-client
  mkdir /mnt/glusterfs
  mount.glusterfs node-1.example.com:/gluster_vol-1 /mnt/glusterfs


Test cluster
-------------

    client1$ touch /mnt/glusterfs/big_file
    server-1$ rm /mnt/glusterfs/big_file
    gluster volume status
