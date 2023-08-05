=====
iSCSI
=====

.. index::
   single: iSCSI
   single: Protocoles; iSCSI

.. contents::
    :depth: 3
    :backlinks: top

####

.. glossary::

iSCSI
=====

:Liens_WEB:
    * `How iSCSI works?`_
    * `iSCSI (page wiki - fr)`_
    * `iSCSI en pratique`_
    * `ESXi 6.7 - Création d’un datastore en iSCSI`_

.. _`How iSCSI works?`: https://stonefly.com/blog/what-is-internet-small-computer-system-interface-iscsi
.. _`iSCSI (page wiki - fr)`: https://fr.wikipedia.org/wiki/ISCSI
.. _`iSCSI en pratique`: https://silverhive.com/informatique/41-reseau/51-iscsi-en-pratique
.. _`ESXi 6.7 - Création d’un datastore en iSCSI`: http://www.oameri.com/esxi-67-creation-dun-datastore-en-iscsi/


iSCSI is an acronym that stands for Internet Small Computer System Interface. It is a
storage area networking (SAN) protocol used to send block storage from storage arrays or
devices to client computers that aren’t directly connected to those devices.

iSCSI Targets and iSCSI Initiators
----------------------------------

Storage = Taget
client = Initiator

An iSCSI storage area network consists of iSCSI targets on storage array controllers and iSCSI
initiators on storage clients. These targets and initiators are used by the iSCSI protocol to
connect storage to clients and are represented by a unique name called the iSCSI Qualified Name or
IQN.

On the client side, the initiator is linked to the target. 

Once the client initiators are configured, an iSCSI LUN (Logical Unit Number) is created on the
storage device and is assigned to an initiator group or client definition. At this point, assuming
the target and initiator are on the same IP network, the client may be able to automatically
discover the target. Once the initiator is connected to the target, the iSCSI LUN at that target IQN
is available for use.

iSCSI LUNs are configured and used the same as any other block storage by the client operating
system.

####

--------
Weblinks
--------

.. target-notes::