.. SPDX-FileCopyrightText: 2022 Zextras <https://www.zextras.com/>
..
.. SPDX-License-Identifier: CC-BY-NC-SA-4.0


In the suggested scenario we will set up a |product| Multi-Server
environment, composed by **six nodes** (that we will denote as *SRV1*,
..., *SRV6*) as follows:

#. **SRV1** features a dedicated installation of Postgres
#. **SRV2** represents the core infrastructure of |product| and
   installs Directory Server, |mesh|, and DB connection
#. **SRV3** is equipped with MTA, the mail server
#. **SRV4** hosts the Proxy, which allows web access to all
   components
#. **SRV5** is an AppServer which installs |file| & |docs|, that
   provide sharing and collaborative editing of documents, and the
   |storage| instance
#. **SRV6** is another AppServer and consists of |pv|, |carbonio|\'s
   ability to preview snippets or thumbnails of a document, the
   Logger, and the User Management

The Logger and |storage| Roles must be unique within a |product|
infrastructure, but for different reasons. Logging is centralised so
all logs produced by the various software running are available in a
same place and ease the search for issues or
troubleshooting. |storage| is a dependency for |file| and therefore it
is installed on the first node on which you install |file|. When you
install |file| on another node, |carbonio| will recognise via |mesh|
that there is already an instance of |storage|, prevent its
installation, and rely on the existent one.

In our scenario, we start |product| installation from 6 nodes equipped
with *Ubuntu 20.04 LTS*. The instructions are valid for nodes which
are installed with RHEL 8: the only difference is the command for the
package installation, while the commands to configure the nodes are
the same.

We also assume that the IP address of each node is ``172.16.0.1X``,
with ``X`` the *n-th* node. In other words, IPs will be in the range
``172.16.0.11`` (SRV1) :octicon:`dash` ``172.16.0.16`` (second
AppServer). These values will be used in configuration files that need
to be manually modified during the installation or upgrade procedures.

In most Multi-Server scenarios, it proves useful to install a **Replica
Directory Server** in a Master/Slave setup for improved reliability
and load-balancing. We describe in a :ref:`dedicated section
<replica-ds-install>` the procedure to install the Replica on a
dedicated node, **SRV7** (which must be equipped with the same OS as
the other six). However, you can install the Replica on any node other
than **SRV2**, following the same procedure.
