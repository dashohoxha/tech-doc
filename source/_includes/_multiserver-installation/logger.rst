.. SPDX-FileCopyrightText: 2022 Zextras <https://www.zextras.com/>
..
.. SPDX-License-Identifier: CC-BY-NC-SA-4.0

The log system in |product| is ``rsyslog``, which supports a
**centralised setup**: in other words, all log files produced by
|product| can be sent to a unique host server, that is appropriately
configured to receive log files.

In a Multi-Server installation, we elect this server as the one on
which the *Logger* is installed.

.. card::

   Logger Node Setup
   ^^^^
   
   On the Logger node, open file :file:`/etc/rsyslog.conf`, find the
   following lines, and uncomment them (i.e., remove the ``#``
   character at the beginning of the line).

   .. code::

      $ModLoad imudp
      $UDPServerRun 514

      $ModLoad imtcp
      $TCPServerRun 514

   Then, restart the ``rsyslog`` service.

   .. code:: console

      # systemctl restart rsyslog


   Finally, specify the host server that will receive logs. Since  is the
   Logger node, we need |srv6h|.

   .. code:: console

      zextras$ carbonio prov mcf zimbraLogHostname SRV6_hostname

   .. note:: Since ``zimbraLogHostname`` is a global attribute, this
      command must be run only once on one node.

.. card::

   Other Nodes Setup
   ^^^^
   
   Once the Logger node has properly been initialised, on **all other
   nodes**, execute

   .. code:: console

      # /opt/zextras/libexec/zmsyslogsetup  && service rsyslog restart
