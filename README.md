Ceph object server backend for OpenStack Swift
==============================================

Installation
------------

1. Install the RADOS object server:

        sudo python setup.py install

2. Modify your object-server.conf to use the new object server:

        [app:object-server]
        use = egg:swift_ceph_backend#rados_object

3. Set the user and pool for Ceph in the [DEFAULT] section in the same file. The original version recomends doing this:

        [DEFAULT]
        rados_user = swift
        rados_pool = swift

However, that version isn't good to me, so I changed to:

        [DEFAULT]
        #rados_user = in ceph.conf, not here.
        rados_pool = swift.buckets
        rados_ceph_conf = /etc/ceph/ceph.conf

