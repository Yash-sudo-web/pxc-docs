.. rn:: 5.7.17-29.20

===================================
Percona XtraDB Cluster 5.7.17-29.20
===================================

Percona is glad to announce the release of
|Percona XtraDB Cluster| 5.7.17-29.20 on April 19, 2017.
Binaries are available from the `downloads section
<http://www.percona.com/downloads/Percona-XtraDB-Cluster-57/>`_
or from our :ref:`software repositories <install>`.

Percona XtraDB Cluster 5.7.17-29.20 is now the current release,
based on the following:

* `Percona Server 5.7.17-13 <http://www.percona.com/doc/percona-server/5.7/release-notes/Percona-Server-5.7.17-13.html>`_

* Galera Replication library 3.20

* wsrep API version 29

All Percona software is open-source and free.

Performance Improvements
========================

This release was focused on performance
and scaling capability with increasing workload threads.
Tests show up to 10 times increase in performance.

Fixed Bugs
==========

* Improved parallelism for better scaling with multiple threads.

* Updated semantics for gcache page cleanup
  to trigger when either :option:`gcache.keep_pages_size`
  or :option:`gcache.keep_pages_count` exceeds the limit,
  instead of both at the same time.

* Improved SST and IST log messages
  for better readability and unification.

* Excluded the ``garbd`` node from flow control calculations.

* Added extra checks to verify that SSL files
  (certificate, certificate authority, and key)
  are compatible before opening connection.

* Added validations for ``DISCARD TABLESPACE``
  and ``IMPORT TABLESPACE`` in :ref:`pxc-strict-mode`
  to prevent data inconsistency.

* Added support for passing the XtraBackup buffer pool size
  with the ``use-memory`` option under ``[xtrabackup]``
  and the ``innodb_buffer_pool_size`` option under ``[mysqld]``
  when the ``--use-memory`` option is not passed
  with the ``inno-apply-opts`` option under ``[sst]``.

* Added the :variable:`wsrep_flow_control_status` variable
  to indicate if node is in flow control (paused).

* Fixed gcache page cleanup not triggering
  when limits are exceeded.

* :jirabug:`PXC-766`: Added the :variable:`wsrep_ist_receive_status` variable
  to show progress during an IST.

* Allowed ``CREATE TABLE ... AS SELECT`` (CTAS) statements
  with temporary tables (``CREATE TEMPORARY TABLE ... AS SELECT``)
  in :ref:`pxc-strict-mode`.
  For more information, see :bug:`1666899`.

* :jirabug:`PXC-782`: Updated ``xtrabackup-v2`` script
  to use the :option:`tmpdir` option
  (if it is set under ``[sst]``, ``[xtrabackup]`` or ``[mysqld]``,
  in that order).

* :jirabug:`PXC-783`: Improved the wsrep stage framework.

* :jirabug:`PXC-784`: Fixed the ``pc.recovery`` procedure to abort
  if the :file:`gvwstate.dat` file is empty or invalid,
  and fall back to normal joining process.
  For more information, see :bug:`1669333`.

* :jirabug:`PXC-794`: Updated the :option:`sockopt` option
  to include a comma at the beginning if it is not set by the user.

* :jirabug:`PXC-795`: Set ``--parallel=4`` as default option
  for ``wsrep_sst_xtrabackup-v2`` to run four threads with XtraBackup.

* :jirabug:`PXC-797`: Blocked :option:`wsrep_desync` toggling
  while node is paused
  to avoid halting the cluster when running ``FLUSH TABLES WITH READ LOCK``.
  For more information, see :bug:`1370532`.

* :jirabug:`PXC-805`: Inherited upstream fix
  to avoid using deprecated variables,
  such as ``INFORMATION_SCHEMA.SESSION_VARIABLE``.
  For more information, see :bug:`1676401`.

* :jirabug:`PXC-811`: Changed default values for the following variables:

  * ``fc_limit`` from ``16`` to ``100``
  * ``send_window`` from ``4`` to ``10``
  * ``user_send_window`` from ``2`` to ``4``

* Moved wsrep settings into a separate configuration file
  (:file:`/etc/my.cnf.d/wsrep.cnf`).

* Fixed ``mysqladmin shutdown`` to correctly stop the server
  on systems using ``systemd``.

* Fixed several minor packaging and dependency issues.

