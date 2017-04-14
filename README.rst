node_exporter-deb
=================

Debian package for the Prometheus node_exporter.

The Prometheus Node Exporter exports hardware and OS metrics exposed by
\*NIX kernels, written in Go with pluggable metric collectors.


------------------
Build instructions
------------------

Check out https://github.com/prometheus/node_exporter/ in a go-style path.

E.g.:

.. code-block:: console

    $ mkdir -p ~/GOPATH/src/github.com/prometheus
    $ cd ~/GOPATH/src/github.com/prometheus
    $ git clone https://github.com/prometheus/node_exporter.git

Check out https://github.com/ossobv/node_exporter-deb/ as the ``debian/``
directory.

.. code-block:: console

    $ cd node_exporter
    $ git clone https://github.com/ossobv/node_exporter-deb/

Check current version and update changelog appropriately.

.. code-block:: console

    $ git describe --tags | sed -e 's/^v//;s/-/+/g;s/$/-osso0~all/g'
    0.14.0+23+g636c88a-osso0~all

Prepend something like this to the changelog::

    node-exporter (0.14.0+23+g636c88a-osso0~all) all; urgency=low

      * CHANGES SINCE LAST RELEASE HERE..

     -- JOHN DOE <JOHN.DOE@EXAMPLE.COM>  Fri, 14 Apr 2017 0F:IX:ME +0200

Run dpkg-buildpackage to create the package:

.. code-block:: console

    $ GOPATH=~/GOPATH dpkg-buildpackage -uc -b
    ...

At this point, you'll have these two files in the parent directory::

    node-exporter_0.14.0+23+g636c88a-osso0~all_amd64.changes
    node-exporter_0.14.0+23+g636c88a-osso0~all_amd64.deb


----
TODO
----

* Add config files.
* Improve control file docs.
