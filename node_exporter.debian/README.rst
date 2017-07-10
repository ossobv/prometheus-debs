prometheus-node_exporter-deb
============================

Debian package for the Prometheus prometheus/node_exporter.

The Prometheus Node Exporter exports hardware and OS metrics exposed by
\*NIX kernels, written in Go with pluggable metric collectors.


------------------
Build instructions
------------------

Check out https://github.com/prometheus/node_exporter/ in a go-style path.

E.g.:

.. code-block:: console

    $ export GOPATH=$HOME/GOPATH

.. code-block:: console

    $ mkdir -p $GOPATH/src/github.com/prometheus
    $ git clone https://github.com/prometheus/node_exporter.git \
        $GOPATH/src/github.com/prometheus/node_exporter

Check out https://github.com/ossobv/prometheus-debs/ as the ``debian/``
directory.

.. code-block:: console

    $ mkdir -p $GOPATH/src/github.com/ossobv
    $ git clone https://github.com/ossobv/prometheus-debs.git \
        $GOPATH/src/github.com/ossobv/prometheus-debs

Use a bind mount:

.. code-block:: console

    $ mkdir $GOPATH/src/github.com/prometheus/node_exporter/debian
    $ sudo mount -t none -o bind \
        $GOPATH/src/github.com/ossobv/prometheus-debs/node_exporter.debian \
        $GOPATH/src/github.com/prometheus/node_exporter/debian

Check current version and update changelog appropriately.

.. code-block:: console

    $ cd $GOPATH/src/github.com/prometheus/node_exporter
    $ git describe --tags | sed -e 's/^v//;s/-/+/g;s/$/-osso0~all/g'
    0.14.0+23+g636c88a-osso0~all

Prepend something like this to the ``debian/changelog``::

    prometheus-node-exporter (0.14.0+23+g636c88a-osso0~all) all; urgency=low

      * CHANGES SINCE LAST RELEASE HERE..

     -- JOHN DOE <JOHN.DOE@EXAMPLE.COM>  Fri, 14 Apr 2017 0F:IX:ME +0200

Run dpkg-buildpackage to create the package:

.. code-block:: console

    $ dpkg-buildpackage -uc -b
    ...

At this point, you'll have these two files in the parent directory::

    prometheus-node-exporter_0.14.0+23+g636c88a-osso0~all_amd64.changes
    prometheus-node-exporter_0.14.0+23+g636c88a-osso0~all_amd64.deb


----
TODO
----

* Add config files?
* Add more docs?
