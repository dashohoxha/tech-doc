.. SPDX-FileCopyrightText: 2022 Zextras <https://www.zextras.com/>
..
.. SPDX-License-Identifier: CC-BY-NC-SA-4.0

The Mails module is where you store, create, and arrange new e-mails.

.. _mail-folders:

Folders and Shares
------------------

E-mail are arranged in folders, which by default are **Inbox**,
**Junk**, **Sent**, **Drafts**, and **Trash**. New folders can be
created by right-clicking on any item in the folder list and placed in
a hierarchy. 

.. note:: Initially, there's no folder hierarchy, because all the
   default folders are at the same level.

Whenever a folder contains unread e-mails, a blue icon with the number
will be displayed on the right of the folder name, with **99+**
meaning there are at least 99 emails to read.

A right-click also allows to carry out other actions on the selected
folder: *move*, *wipe* (i.e., remove all e-mails in the folder),
*edit*, *delete*, and *share* (with internal colleagues or even make
it freely readable).

.. hint:: An e-mail can be placed in exactly one folder.
          
To find shares, click on the :bdg-primary-line:`FIND SHARES`
underneath the `Share Folders`. In the dialog, enter the e-mail
address of the colleague of which you want to find the shares. If the
colleague has shared some folder, you'll be presented with a list.

While e-mails by default are marked as *read* when they are first
accessed, it is possible to mark each of them manually. This option is
particularly useful in case of shared account, to make sure that
everybody who has access to the e-mail has read it.


.. _mail-tags:

Tags
----

A **tag** is a label, added to either an e-mail or a calendar event
item that helps to improve both the organisation of the e-mails or
events themselves and the search among them.

New tags can be added with a right click on the **tags** menu item,
while an existing tag can be modified or deleted by right-clicking on
it.

To search for a tag, in the :ref:`Search quickbar <global-search>` use
the syntax ``tag:name``, replacing *name* with the name of the
tag. The same tags used for e-mail can be used to mark :ref:`Calendar
appointment <calendar-comp>`.

.. _mail-working:

Working with E-mails
--------------------

By default, e-mails are placed in the **Inbox** folder upon arrival
(unless they are marked as *junk email*) and in the **Sent** folder
when sent. These landing folders can be changed via the :ref:`Mails
settings <settings-mails>` page, by setting up **filters** and move
automatically any email to a given folder.

E-mails are arranged in *Conversations*, meaning that an e-mail with
all the replies it receives is packed in one single element in the
list. Messages and conversations can be drag-and-dropped to any
folder.

.. hint:: Moving a single e-mail in a conversation is not possible,
   the whole conversation will be moved.
   
On the top-right corner of each e-mail there are a few icons that
allow to carry out a number of actions; click the
:material-regular:`more_vert` icon to access them and many more: mark
e-mail as read/unread or as spam, print, delete, tag, or flag it. A
flag is a simple indicator for an email that can be adapted to one's
preference: to name a few, it has some importance compared to other,
it needs some action, or it has been processed and can be archived or
deleted.

More actions are available and shown upon right-clicking an email.

|product| has support for **e-mail receipts**: when composing an
email, a click on the :material-regular:`more_vert` icon on the
right-hand side of the subject will add a request for a read receipt
from the e-mail recipient.

When opening for the first time an email with a receipt request, a
modal will appear and ask to send a read receipt to the author. Click
:bdg-primary:`NOTIFY` to send the receipt, otherwise no receipt will
be sent.

In |product|, to prevent sending an incomplete e-mail, an automatic
delay of three seconds takes places, and a message appears on the
bottom right corner: click :bdg-info:`UNDO` to stop the sending and
continue editing the e-mail.

.. _mail-attachments:

Attachments Management
----------------------

|product| supports e-mail attachments; depending whether the e-mail is
written before it is sent or it has been received, the following
actions are available

.. grid:: 1 1 2 2
   :gutter: 3

   .. grid-item-card::
      :columns: 4

      Composing an e-mail
      ^^^^

      While composing an e-mail, any file can be added as an
      attachment for either a local directory on the workstation or on
      the user's personal storage on |file|.
   
   .. grid-item-card::
      :columns: 4
		
      Inline Attachments
      ^^^^^

      Images on the local workstation can be included as inline
      attachments in the body of the e-mails, using the button in the
      bar above the editor to select them.
      
   .. grid-item-card::
      :columns: 4

      Receiving an e-mail
      ^^^^^

      When receiving an e-mail with attachments, the user has the
      option to either download the file to a local directory on the
      workstation, or to save it in the user's personal's storage on
      |file|.
      

.. _mail-trash-folder:

Trash Folder
------------

The trash folder is a special folder in which e-mails marked for
deletion are temporary stored, in case they need to be recovered.
An e-mail in the Trash folder will be automatically deleted after a
period equivalent to the retention time, by default **30 days**.

.. _mail-junk-folder:

Junk Folder
-----------

Like the *trash folder*, this is a special folder in which e-mails
that are wither marked as **spam**, or otherwise are unsolicited or
undesired, are stored.

|product| ships with anti-virus and anti-spam engines that are able to
automatically infer whether an e-mail is legit or not and mark it as
spam. However, in case you think an e-mail is spam but was not
processed, it can be manually marked as spam by right-clicking it and
selecting *Mark as spam*. Also that vice-versa is valid: an e-mail in
the *Junk* folder (i.e., recognised as spam) can be marked as *not
spam*: it will land in the **Inbox**.

All the content of the junk folder helps the anti-spam engine to learn
and improve its results.

.. topic:: Massive e-mail sending

   A *massive e-mail sending* is the process of sending legitimate
   e-mails to a large number of e-mail addresses, often used for
   marketing purposes and using a specific software or online service
   for this purpose.

   |product| users may be allowed to send an e-mail to all or to most
   of their colleagues (*internal users*) in special circumstances
   (e.g., company-wide announcements), but they should never send
   massive e-mails to external e-mail addresses, because the risk is
   that the company's e-mail server enter a **blacklist** and all the
   e-mails it delivers are marked as spam,making communication with
   external companies (like suppliers and customers) very difficult.
