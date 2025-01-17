.. SPDX-FileCopyrightText: 2022 Zextras <https://www.zextras.com/>
..
.. SPDX-License-Identifier: CC-BY-NC-SA-4.0

.. srv5 - Advanced, AppServer, Files, and Docs

On this node, first install all the required packages for |file|, then
configure the various services needed.

.. tab-set::

   .. tab-item:: Ubuntu
      :sync: ubuntu

      .. code:: console

         # apt install service-discover-agent carbonio-appserver \
           carbonio-storages-ce carbonio-user-management \
           carbonio-files-ce carbonio-docs-connector-ce \
           carbonio-docs-editor

   .. tab-item:: RHEL
      :sync: rhel

      Make sure to respect the order of installation.

      .. code:: console

         # dnf install service-discover-agent carbonio-appserver
         # dnf install carbonio-storages-ce carbonio-user-management
         # dnf install carbonio-files-ce carbonio-docs-connector-ce
         # dnf install carbonio-docs-editor

Execute the following tasks.

#. Bootstrap |carbonio|

   .. code:: console

      # carbonio-bootstrap

   In the bootstrap menu, use |srv2h|, |ldappwd|, and
   |nginxpwd| in the following items to complete successfully the
   bootstrap.

   * ``Ldap master host``: |srv2h|
   * ``Ldap Admin password``: |ldappwd|
   * ``Bind password for nginx ldap user``: |nginxpwd|

#. Run |mesh| setup using |meshsec|

   .. code:: console

      # service-discover setup-wizard

   Since this node is not the |mesh| Server, the
   :file:`cluster-credentials.tar.gpg` file will be automatically
   downloaded.
   
#. Complete |mesh| setup

   .. code:: console

      # pending-setups -a

   .. hint:: The **secret** needed to run the above command is stored
      in file :file:`/var/lib/service-discover/password` which is
      accessible only by the ``root`` user.
