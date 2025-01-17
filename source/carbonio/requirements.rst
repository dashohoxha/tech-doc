.. SPDX-FileCopyrightText: 2022 Zextras <https://www.zextras.com/>
..
.. SPDX-License-Identifier: CC-BY-NC-SA-4.0

.. _carbonio-requirements:

Requirements
------------

.. _system-requirements:

System Requirements
~~~~~~~~~~~~~~~~~~~


.. grid:: 1 1 1 2
   :gutter: 2

   .. grid-item-card::
      :columns: 12 12 12 6

      Hardware requirements
      ^^^^^

      .. csv-table::

	 "CPU", "Intel/AMD 64-bit CPU 1.5 GHz"
	 "RAM", "8 GB min, 16GB recommended"
	 "Disk space (Operating system and Carbonio)", "40 GB"

      These requirements are valid for Carbonio Single-Server or for
      each Carbonio Node in a Multi-Server Installation and may vary
      depending on the size on the infrastructure, which includes the
      number of mailboxes and the functionalities running.

   .. grid-item-card::
      :columns: 12 12 12 6

      Supported Virtualization Platforms
      ^^^^^

      .. csv-table::

	 VMware vSphere 6.x
	 VMware vSphere 7.x
	 XenServer
	 KVM
	 Virtualbox (testing purposes only)

.. _software-requirements:

Software Requirements
~~~~~~~~~~~~~~~~~~~~~

|product| is available for **64-bit** CPUs only and can be installed
on top of any vanilla **Ubuntu 20.04 LTS Server Edition** or **RHEL
8** installation.

The following requirements must be satisfied before attempting to
install |product|.

#. valid DNS resolution for both the domain (``MX`` and ``A`` records) and the
   FQDN (``A`` record)
#. Python 3, latest version available on the Operating System chosen
#. Perl, latest version available on the Operating System chosen
#. IPv6 must be disabled. Make also sure that the :file:`/etc/hosts`
   does not contain any IPv6 entries.

See :ref:`the dedicated box below <config-dns>` for details and examples.

Support for other distributions will be announced in due course
when it becomes available.

Additional Requirements
~~~~~~~~~~~~~~~~~~~~~~~

* Acquaintance with the use of CLI is necessary.  All ``carbonio``
  commands must be executed as the ``zextras`` user (these commands
  will feature a ``zextras$`` prompt), while all other commands must
  be issued as the ``root`` user, unless stated otherwise.
* Commands or groups of commands may be different between Ubuntu and
  RHEL 8. This is shown by blue tabs: click on the tab of your choice
  to find the correct command.
* When no such tabs are given, the commands to run are the same on
  Ubuntu and RHEL 8.

.. _config-dns:

.. topic:: Configuring DNS resolution

   To make sure that the DNS is correctly configured for both **A** and
   **MX** records: to do so, you can use any DNS resolution server,
   including `dnsmasq`, `systemd-resolved`, and `bind`.

   We show as an example, only suitable for **demo** or **testing
   purposes**, how to install and configure ``dnsmasq`` for DNS
   resolution.

   .. dropdown:: Example: Set up of dnsmasq for demo or test environment

      Follow these simple steps to set up ``dnsmasq``. These
      instructions are suitable for a demo or testing environment
      only.

      .. warning:: On Ubuntu **20.04**, installing and running dnsmasq
	 may raise a port conflict over port **53 UDP** with the
	 default `systemd-resolved` service, so make sure to disable
	 the latter before continuing with the next steps.

      .. tab-set::

	 .. tab-item:: Ubuntu
	    :sync: ubuntu

	    .. code:: console

	       # apt install dnsmasq

	 .. tab-item:: RHEL
	    :sync: rhel

	    .. code:: console

	       # dnf install dnsmasq

      To configure it, add the following lines to file
      :file:`/etc/dnsmasq.conf`::

	  server=1.1.1.1
	  mx-host=example.com,mail.example.com,50
	  host-record=example.com,172.16.0.10
	  host-record=mail.example.com,172.16.0.10

      Remember to replace the **172.16.0.10** IP address with the one
      of your server. Then, make sure that the :file:`etc/resolv.conf`
      contains the line::

	nameserver 127.0.0.1

      This will ensure that the local running :command:`dnsmasq` is
      used for DNS resolution. Finally, restart the **dnsmasq**
      service

      .. code:: console

	 # systemctl restart dnsmasq

.. _fw-ports:

Firewall Ports
~~~~~~~~~~~~~~

For |carbonio| to operate properly, it is necessary to allow network
communication on specific ports.  On a Single-Server installation,
only ports in the *External Connections* must be opened, because all
the remaining traffic does not leave the Server.

In Multi-Server installation, ports listed in the *Internal
Connections* and *Carbonio Mesh* must be opened on **all** nodes,
while those in the *External Connections* only on the node on which
the service runs. For example, port 443 should be opened only on the
node hosting the **Proxy** Role.

.. dropdown:: TCP External Connections
   :open:

   .. csv-table::
      :header: "Port", "Service"
      :widths: 10 90

      "25", "Postfix incoming mail"
      "80", "unsecured connection to the Carbonio web client"
      "110", "external POP3 services"
      "143", "external IMAP services"
      "443", "secure connection to the Carbonio web client"
      "465", ":bdg-danger:`deprecated` SMTP authentication relay [1]_"
      "587", "Port for smtp autenticated relay, requires STARTTLS
      (or opportunistic SSL/TLS)"
      "993", "external IMAP secure access"
      "995", "external POP3 secure access"
      "8636", "access to LDAP address books"

   .. [1] This port is still used since in some cases it is
      considered safer than 587. It requires on-connection SSL.

   .. warning:: SMTP, IMAP, and POP3 ports should be exposed only if
      really needed, and preferably only accessible from a VPN tunnel,
      if possible, to reduce the attack surface.

.. dropdown:: TCP Internal Connections
   :open:

   .. csv-table::
      :header: "Port", "Service"
      :widths: 10 90

      "22", "SSH access"
      "389", "unsecure LDAP connection"
      "636", "secure LDAP connection"
      "3310", "ClamAV antivirus access"
      "6071", "secure access to the Admin Panel"
      "7025", "local mail exchange using the LMTP protocol"
      "7026", "bind address of the Milter service"
      "7047", "used by the server to convert attachments"
      "7071", "Port for SOAP services communication"
      "7072", "NGINX discovery and authentication"
      "7073", "SASL discovery and authentication"
      "7110", "internal POP3 services"
      "7143", "internal IMAP services"
      "7171", "access Carbonio configuration daemon (zmconfigd)"
      "7306", "MySQL access"
      "7780", "the spell checker service access"
      "7993", "internal IMAP secure access"
      "7995", "internal POP3 secure access"
      "8080", "internal HTTP services access"
      "8443", "internal HTTPS services access"
      "8735", "Internal mailbox :octicon:`arrow-both` mailbox communication"
      "8742", "internal HTTP services"
      "8743", "internal HTTPS services"
      "9071", "used only in one case [2]_"
      "10024", "Amavis :octicon:`arrow-both` Postfix"
      "10025", "Amavis :octicon:`arrow-both`  OpenDKIM"
      "10026", "configuring Amavis policies"
      "10028", "Amavis :octicon:`arrow-both` content filter"
      "10029", "Postfix archives access"
      "10032", "Amavis :octicon:`arrow-both` SpamAssassin"
      "23232", "internal Amavis services access"
      "23233", "SNMP-responder access"
      "11211", "memcached access"

   .. [2] When the NGINX support for Administration Console and the
      ``mailboxd`` service run on the same host, this port can be used
      to avoid overlaps between the two services

.. dropdown:: Ports Used by |mesh|
   :open:

   These ports are used by |mesh| internally.

   .. csv-table::
      :header: "Port", "Protocol", "Service"
      :widths: 10 20 70

      "8300", "TCP Only", "management of incoming requests from other agents"
      "8301", "TCP and UDP", "management of gossip protocol [3]_ in the LAN"
      "8600", "TCP and UDP", "DNS resolutions"
      "8500", "TCP Only", "clients access to HTTP API"
      "21000-21255", "TCP range only", "Automatical Sidecar service
      registrations"


   .. [3] The Gossip protocol is an encrypted communication protocol
      used by |mesh| for message broadcasting and membership
      management.
      
.. dropdown:: Ports Used by |vs|
   :open:

   If you install the |vs|, you need to open these additional ports:

   .. csv-table::
      :header: "Port", "Protocol", "Service"
      :widths: 10 20 70

      "8188", "TCP", "Internal connection"
      "20000-40000", "UDP", "Client connections for the audio and
      video streams" 
