prometheus-nginxvts_exporter-deb
================================

Debian package for the Prometheus hnlq715/nginx-vts-exporter.

The Prometheus Nginx VTS-module exporter scrapes nginx-module-vts stats
and exports them via HTTP for Prometheus consumption.


------------------
Build instructions
------------------

Check out https://github.com/phnlq715/nginx-vts-exporter/ in a go-style path.

E.g.:

.. code-block:: console

    $ export GOPATH=$HOME/GOPATH

.. code-block:: console

    $ mkdir -p $GOPATH/src/github.com/hnlq715
    $ git clone https://github.com/hnlq715/nginx-vts-exporter.git \
        $GOPATH/src/github.com/hnlq715/nginx-vts-exporter

Check out https://github.com/ossobv/prometheus-debs/ as the ``debian/``
directory.

.. code-block:: console

    $ mkdir -p $GOPATH/src/github.com/ossobv
    $ git clone https://github.com/ossobv/prometheus-debs.git \
        $GOPATH/src/github.com/ossobv/prometheus-debs

Use a bind mount:

.. code-block:: console

    $ mkdir $GOPATH/src/github.com/hnlq715/nginx-vts-exporter/debian
    $ sudo mount -t none -o bind \
        $GOPATH/src/github.com/ossobv/prometheus-debs/nginxvts_exporter.debian \
        $GOPATH/src/github.com/hnlq715/nginx-vts-exporter/debian

Check current version and update changelog appropriately.

.. code-block:: console

    $ cd $GOPATH/src/github.com/hnlq715/nginx-vts-exporter
    $ git describe --tags | sed -e 's/^v//;s/-/+/g;s/$/-osso0~all/g'
    0.5+4+g878bfa1-osso0~all

Prepend something like this to the ``debian/changelog``::

    prometheus-nginxvts-exporter (0.5+4+g878bfa1-osso0~all) all; urgency=low

      * CHANGES SINCE LAST RELEASE HERE..

     -- JOHN DOE <JOHN.DOE@EXAMPLE.COM>  Mon, 22 May 2017 0F:IX:ME +0200

Run dpkg-buildpackage to create the package:

.. code-block:: console

    $ dpkg-buildpackage -uc -b
    ...

At this point, you'll have these two files in the parent directory::

    prometheus-nginxvts-exporter_0.5+4+g878bfa1-osso0~all_amd64.changes
    prometheus-nginxvts-exporter_0.5+4+g878bfa1-osso0~all_amd64.deb


----
TODO
----

* Add manpage?
