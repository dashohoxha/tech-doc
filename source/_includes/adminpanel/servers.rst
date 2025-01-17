.. SPDX-FileCopyrightText: 2022 Zextras <https://www.zextras.com/>
..
.. SPDX-License-Identifier: CC-BY-NC-SA-4.0

This section is used to configure the Global e-mail server. 

Global Servers
--------------

The lists of all configured server and buckets are shown here.

Server Details
--------------

In the Server Details section it is possible to select a server, check
its currently used volumes and assign new ones, and finally configure
HSM policies.

Data Volumes
~~~~~~~~~~~~

After you selected the server, the volumes it currently uses are
shown, along with a few configured options. To add a new Volume, click
on the :bdg-primary-line:`NEW VOLUME` button.

In the dialog window, provide the basic information of the new volume
in the first tab: The allocation type, name, and path.

The second tab depends on the allocation:

* **Local**: decide whether this is a primary, secondary, or index volume,
  select a compression threshold if necessary, and finally if this
  will become the new current volume.

* **External**, **Sproxy**, **Centralized**: primary, secondary, or
  index volume, select the type of Object Storage and a prefix to
  identify the volume. You can set this volume as *Centralized*, which
  proves useful in case it will be shared by multiple servers.

HSM Settings
~~~~~~~~~~~~

HSM settings are policies for automatically processing objects in the
mailstore: e-mails, documents, contacts, and events.

HSM Policies can be scheduled to be run automatically at given times
and days; after this operation, deduplication can be enabled to save
space in case of duplicated items, by keeping only one copy of an
item.


Create a New Policy
~~~~~~~~~~~~~~~~~~~

The dialog that opens after clicking the :bdg-primary-line:`NEW
VOLUME` button allows to create a new HSM policy in a few steps.

.. card:: Step 1. Policy settings
   
   In this step, first select to which items the policy will be
   applied.

   .. hint:: A click on the :octicon:`square;2em;sd-text-primary`
      **All** checkbox toggles all items at once.

   The policy can be applied on the size of the items or on a time
   interval. in our example, we remove all messages older than 7
   days whose size is larger than 20Mb.


   .. image:: /img/adminpanel/new-hsm-settings.png
      :scale: 50
      :align: center

.. card:: Step 2. Select Volumes


   We now chose the volumes to which the policy is applied. By
   default, **all the primary volumes** are selected. While it is
   possible to manually specify the volumes from the list, we do not
   change this.

   .. image:: /img/adminpanel/new-hsm-volumes.png
      :scale: 50
      :align: center
              
.. card:: Step 3. Create Policy

   The last stop shows the settings for review. You can go back to
   change any options or create the policy.

   .. image:: /img/adminpanel/new-hsm-create.png
      :scale: 50
      :align: center
              
