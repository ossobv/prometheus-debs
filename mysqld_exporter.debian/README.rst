prometheus-mysqld_exporter-deb
==============================

Debian package for the Prometheus prometheus/mysqld_exporter.

The Prometheus Node Exporter exports hardware and OS metrics exposed by
\*NIX kernels, written in Go with pluggable metric collectors.


------------------
Build instructions
------------------

Check out https://github.com/prometheus/mysqld_exporter/ in a go-style path.

E.g.:

.. code-block:: console

    $ export GOPATH=$HOME/GOPATH

.. code-block:: console

    $ mkdir -p $GOPATH/src/github.com/prometheus
    $ git clone https://github.com/prometheus/mysqld_exporter.git \
        $GOPATH/src/github.com/prometheus/mysqld_exporter

Check out https://github.com/ossobv/prometheus-debs/ as the ``debian/``
directory.

.. code-block:: console

    $ git clone https://github.com/ossobv/prometheus-debs.git \
        $GOPATH/src/github.com/prometheus/prometheus-debs

Use a bind mount:

.. code-block:: console

    $ mkdir $GOPATH/src/github.com/prometheus/mysqld_exporter/debian
    $ sudo mount -t none -o bind \
        $GOPATH/src/github.com/prometheus/prometheus-debs/mysqld_exporter.debian \
        $GOPATH/src/github.com/prometheus/mysqld_exporter/debian

Check current version and update changelog appropriately.

.. code-block:: console

    $ cd $GOPATH/src/github.com/prometheus/mysqld_exporter
    $ git describe --tags | sed -e 's/^v//;s/-/+/g;s/$/-osso0~all/g'
    0.10.0+4+g36b2b8b-osso0~all

Prepend something like this to the ``debian/changelog``::

    prometheus-mysqld-exporter (0.10.0+4+g36b2b8b-osso0~all) all; urgency=low

      * CHANGES SINCE LAST RELEASE HERE..

     -- JOHN DOE <JOHN.DOE@EXAMPLE.COM>  Mon, 22 May 2017 0F:IX:ME +0200

Run dpkg-buildpackage to create the package:

.. code-block:: console

    $ dpkg-buildpackage -uc -b
    ...

At this point, you'll have these two files in the parent directory::

    prometheus-mysqld-exporter_0.10.0+4+g36b2b8b-osso0~all_amd64.changes
    prometheus-mysqld-exporter_0.10.0+4+g36b2b8b-osso0~all_amd64.deb


----
TODO
----

* Add more docs from the main repo into /usr/share/doc?
* Add manpage?
* Allow /etc/default/prometheus-mysqld-exporter to override the my.cnf?
