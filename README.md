Ceph object server backend for OpenStack Swift
==============================================

These are some changes I made in order to make this work with my version of Ceph (0.94) and Swift (Juno). This version does also work for Openstack Kilo. Unfortunately it doesn't work in Liberty version.

Remind the base project is:  https://github.com/stackforge/swift-ceph-backend and the changes I made aren't expected to work anywhere but on my own installation. Feel free to use it on your own risk, but no liability will be accepted for any use of this software.

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

