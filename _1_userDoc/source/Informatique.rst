============
Informatique
============

.. contents::
   :backlinks: top
   :depth: 3

####

Ce document réuni un ensemble d'informations, Manip et autre tips concernant 
la gestion / Maintenance des postes utilisateur et la gestion maintenance des parcs
informatiques.

####

---------------------------------
Cours et connaissances génériques
---------------------------------

    #. `Microsoft Azure`_ : Liste de Webinar en français sur l'utilisation et l'administration 
       d'Azure
    
    #. Les Expressions Régulières (`RegEx`_) : Une rubrique spéciale RegEx a été créer dans le 
       journal de manip
        
    #. `Microsoft Virtual Academy`_ : Cours en ligne gratuis dispenser par microsoft
        
    #. `VIM / VI`_ : une rubrique spéciale VIM a été créer dans le journal de manip

    #. `Logical Unit Number (LUN)`_

    #. `Maximum Transmission Unit (MTU)`_

    #. `Server Message Block Protocol (SMB protocol)`_

.. _`Logical Unit Number (LUN)`: https://en.wikipedia.org/wiki/Logical_unit_number
.. _`Maximum Transmission Unit (MTU)`: https://www.cloudflare.com/fr-fr/learning/network-layer/what-is-mtu/
.. _`Server Message Block Protocol (SMB protocol)`: https://searchnetworking.techtarget.com/definition/Server-Message-Block-Protocol

.. glossary::

    LUN

        In computer storage, a logical unit number, or LUN, is a number used to identify a logical
        unit, which is a device addressed by the SCSI protocol or by Storage Area Network protocols
        that encapsulate SCSI, such as Fibre Channel or iSCSI.

        A LUN may be used with any device which supports read/write operations, such as a tape
        drive, but is most often used to refer to a logical disk as created on a SAN. Though not
        technically correct, the term "LUN" is often also used to refer to the logical disk itself.
        

    MTU

        Dans les réseaux, `Maximum Transmission Unit (MTU)`_ est une mesure représentant le plus
        grand paquet de données qu'un appareil connecté au réseau acceptera. Imaginez cette mesure
        comme une hauteur limitée dans les voies souterraines ou les tunnels : les voitures et les
        camions qui dépassent la hauteur limitée ne peuvent pas passer, tout comme les paquets qui
        dépassent le MTU d'un réseau ne peuvent pas passer par ce réseau.

        Cependant, contrairement aux voitures et aux camions, les paquets de données qui dépassent
        le MTU sont fragmentés en plus petites parties pour pouvoir passer. Ce processus est appelé
        fragmentation. Les paquets fragmentés sont réassemblés une fois arrivés à destination.

        Le MTU est mesurée en octets - un « octet » est égal à 8 bits d'information, c'est-à-dire 8
        uns et zéros. 1 500 octets est la taille maximale du MTU.

        N.B : Il est possible d'autoriser l'utilisation de paquet de 9000 octets en activant le
        Jumbo Frame. Le jumbo devra alors être autorisé / Activé sur tous les equipements devant
        recevoir les paquets envoyés.

####

----------
Protocoles
----------

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

iSCSI LUNs are configured and used the same as any other block storage by the client operating system.

.. glossary::

SMB
===
        
SMB - Server Message Bloc protocol is a client server communication used for sharing acces to files,
printers, serial ports and other resources on a network.

Servers make file systems and other resources (printers, named pipes, APIs) available to clients on
the network. Client computers may have their own hard disks, but they also want access to the shared
file systems and printers on the servers.

The SMB protocol is known as a response-request protocol, meaning that it transmits multiple
messages between the client and server to establish a connection. Clients connect to servers using
TCP/IP (actually NetBIOS over TCP/IP as specified in RFC1001 and RFC1002), NetBEUI or IPX/SPX.

Once they have established a connection, clients can then send commands (SMBs) to the server that
allow them to access shares, open files, read and write files, and generally do all the sort of
things that you want to do with a file system. However, in the case of SMB, these things are done 
over the network.

.. glossary::

TELNET
======

Telnet is an application protocol which allows you, with the use of a telnet client, to connect to
and execute commands on a remote machine that's hosting a telnet server.

The telnet client will establish a connection with the server. The client will then become a virtual
terminal- allowing you to interact with the remote host.

**How does Telnet work?**
The user connects to the server by using the Telnet protocol, which means entering "telnet" into a
command prompt. The user then executes commands on the server by using specific Telnet commands in
the Telnet prompt. You can connect to a telnet server with the following syntax: "telnet [ip] [port]"

**Replacement**
Telnet sends all messages in clear text and has no specific security mechanisms. Thus, in many
applications and services, Telnet has been replaced by SSH in most implementations.

####
        
--------
Matériel
--------

Information pour la gestion et maintenance des matériel

Trouver le numéro de série d'un poste / serveur en CLI
======================================================

    .. code::

        wmic bios get serialnumber

Vérifier les garantie constructeur
==================================

    #. `Garantie Dell`_
    
    #. `Garantie HP`_

####
        
----------------
Poste de travail
----------------

Toutes les informations concernant l'utilisation et la maintenance des postes utilisateurs.

Lancer la restauration système depuis windows
=============================================

L'utilitaire de restauration système se nomme : ::

    rstrui.exe

Nettoyer / Réparer
==================

:Liens_Web:
        * `Medicat`_ : Un bon remplaçant de Hiren' Boot CD

Forcer la suppression d'une partition
=====================================

    :Liens_Web:
                * `Utiliser diskpart`_ :  voir le #2

    #. dispart 

        Depuis une invite de command Administrateur

        .. code:: PowerShell

            c:\>diskpart
            DISKPART>rescan
            DISKPART>list disk
            DISKPART>slelect disk x
            # x = numéro du disque à effacer, attention à ne pas se tromper
            DISKPART>list partition
            DISKPART>select partition x
            # x = numéro de la partition à effacer, attention à ne pas se tromper
            DISKPART>delete partition override

Ajouter un élément dans le menu contextuel
==========================================

    :Liens_Web:

            * `Ajouter des commandes au menu contextuel`_
            * `Aouter un script au menu contextuel`_

Excel
=====

Colorer une ligne sur deux dans un tableau Excel
------------------------------------------------
        
:Liens_Web:
        * `Excel 1 ligne sur 2`_ 
    
    #. La commande à saisir pour calculer une les lignes pair : ::
        
        =MOD(LIGNE() ;2)
            
    #. Pour les lignes impair : ::
        
        =NON(MOD(LIGNE() ;2))

Navigateur Web
==============

How to fix Cross Origin Request Security (CORS) error
-----------------------------------------------------

:Liens_Web:
        * `fix Cross Origin Request Security (CORS)`_

:Info:          Cette erreur peut enpêcher la lecture de certaine page en HTTP ou certain fichiers.
                Ce problème est notament vrai en AJAX avec l'utilisation de **XMLHttpRequest**.
                Cette erreur est signalée dans la console du navigateur.

####
        
--------
SysAdmin
--------

Ensemble d'informations relative à l'administration Système

Sysinternals
============

    :Liens_Web:
        * `Sysinternals pack`_: Ensemble d'utilitaire pour l'administration et la gestion de parc 
          informatique.

        ex:
            - Disk2vhd
            - AdRestore
            - Whois
            - BGinfo
            - etc ...

Exchange
========

Renouveler un certificats sur Exchange 2010
-------------------------------------------

    :Liens_Web:
            * `Certificat Exchange`_ 

Exporter en CSV la taille et le nombre d'item des BAL
-----------------------------------------------------

    .. code:: PowerShell

        # Dans la console exchange PS

        Get-MailboxStatistics -server [nom_du_serveur] | Sort-Object TotalItemSize -Descending | select DisplayName, TotalItemSize, ItemCount | export-csv -Path "[chemin_et_nom_du_fichiers.csv]" -Delimiter ";" -Encoding "Default"

WSUS
====

Libération de l’espace disque sur le serveur WSUS
-------------------------------------------------

    :Liens_Web:
        * `Nettoyage WSUS`_ : description simple (et en Français) pour l'utilisation de l'assistant 
          de nettoyage WSUS.

Hyper-V
=======

Sysprep
-------

Configurer un VHD Sysprep
+++++++++++++++++++++++++

:Liens_Web:
        * `CFG Sysprer sur VHD`_ : Une explication simple et en français

        * `Script VHD+Sysprep`_ : Un script permettant de créer automatiquement un VHD 'Sysprepé'

    #. Installer tous les éléments nécessaires et faire les MAJ (on peut aussi intégrer des
       fonctionnalité)

    #. Executer la commande Syprep 

        .. code:: PowerShell

            C:\Windows\System32\Sysprep.exe /Generalize /OOBE /Shutdown

    #. Copier le VHD 'sysprepé' ::

        ex:
        Model_VHD

Mettre à jour une image VHD
+++++++++++++++++++++++++++

:Liens_Web:
        *  `UPD SysprepImg`_ : Script permettant de mettre à jour une image VHD sans devoir l'associer à une VM

        * `ex UPD SysprepImg`_ : Exemple d'utilisation du script 'Update-SysprepImage.ps1'

Check point (anciennement nommés Snapshot)
------------------------------------------

:Liens_Web:
        * `Utilisation de points de contrôle`_ : technet Microsoft

:/!\\Attention/!\\:
        
        L'application d'un point de contrôle ne le supprime pas

Réplication Hyper-V en workgroup
--------------------------------

:Liens_Web:
        * `Hyper-V replication in a workgroup or across domains using a self signed certificate`_ 

CLI : CMD et Powershell
=======================

Lister les rôles FSMO
---------------------

    :Liens_Web:
        * `Get FSMO in CLI`_

    .. code:: shell
    
        # en CMD : Lister tous les rôles d'un coup
        Netdom Query FSMO

    .. code:: PowerShell

        # En Powershell :
        Get-ADDomainController -Filter * | Select-Object Name, Domain, Forest, OperationMasterRoles | Where-Object {$_.OperationMasterRoles} | Ft -AutoSize

Installer le module PowerShell ActiveDirectory sous Windows 10
--------------------------------------------------------------
    
    :Liens_Web:
        * `HowTo install AD on w10`_ : Explication par l'auteur du script
            
        * `Script install AD on w10`_ : Le script lui même
    
    
Identifier les PC qui ne se sont pas connecter au domaine depuis au moins 180 Jours
-----------------------------------------------------------------------------------
       
    .. code:: PowerShell
       
        import-module ActiveDirectory
        $vdate = (Get-Date).adddays(-180)
        Get-ADComputer -filter {(Enabled -eq "True") -and (LastLogonDate -le $vdate)} -property * | ft LastLogonDate, CN
            # applique un filtre sur les élément qui ne sont pas désactivé et qui ne
            # se sont pas connecter de puis au moins 180 Jours
        
Pour ne pas filtrer le résultat et voir toutes les propriété
------------------------------------------------------------

    .. code:: PowerShell
        
        Get-ADComputer -filter * -property *
            # N.B : Fonctionne aussi avec get-ADUser
            
Identifier les comptes utilisateurs qui ne se sont pas connecter au domaine depuis au moins 180 Jours

    .. code:: PowerShell

        import-module ActiveDirectory
        $vdate = (Get-Date).adddays(-180)
        Get-ADuser -filter {(Enabled -eq "True") -and (LastLogonDate -le $vdate)} -property * | ft LastLogonDate, CanonicalName
            # applique un filtre sur les élément qui ne sont pas désactivé et qui ne
            # se sont pas connécter de puis au moins 180 Jours
                
Connaitre la date du dernier démarrage d'un serveur
---------------------------------------------------

    .. code:: PowerShell
    
        Get-CimInstance -ClassName Win32_OperatingSystem | Select CSName, LastBootUpTime
            # Windows2012 r2 et +
            
        # ou :
            
        $LastBootTime = (Get-WmiObject win32_Operatingsystem).LastBootUpTime
        [System.Management.ManagementDateTimeConverter]::ToDateTime($LastBootTime)

Se connecter à Exchange
-----------------------

    .. code:: PowerShell
    
        $Credentials = Get-Credential
        $ExSession = New-PSSession –ConfigurationName Microsoft.Exchange –ConnectionUri ‘http://SRV-MAIL.poree.local/PowerShell/?SerializationLevel=Full’ -Credential $Credentials –Authentication Kerberos
        Import-PSSession $ExSession
        # ...
        Remove-PSSession $ExSession

Connaitre le niveau fonctionnel Active Directory
------------------------------------------------

    .. code:: PowerShell

        (Get-ADDomain).DomainMode

Service DHCP
============

Replication et bascullement DHCP entre deux serveurs
----------------------------------------------------

    :Liens_Web:
        * `Réplication du service DHCP et basculement entre 2 serveurs`_

            

####

----------
Webography
----------

.. target-notes::

.. _`Microsoft Azure`: https://docs.djangoproject.com/en/2.1/topics/db/models/
.. _`RegEx`: https://poltergeist42.github.io/JDM/Regex.html
.. _`Microsoft Virtual Academy`: https://mva.microsoft.com/
.. _`VIM / VI`: https://poltergeist42.github.io/JDM/VIM.html
.. _`Garantie Dell`: http://www.dell.com/support/home/fr/fr/frdhs1/products/?app=warranty&c=fr&l=fr&s=dhs 
.. _`Garantie HP`: http://h20565.www2.hpe.com/hpsc/wc/public/home?lang=fr-fr&cc=fr 
.. _`Mise en place de VLANs et de routage inter-VLANs`: https://www.it-connect.fr/mise-en-place-de-vlans-et-de-routage-inter-vlans/
.. _`initiation au VLAN`: https://networkcorp.fr/vlan-virtual-local-area-network/
.. _`Configuration d'un switch HP avec l'interface WEB`: https://fucking-it.com/fr/tutoriel/switch-hp/422-switch-hp-configurez-vlan-interface-web
.. _`Configuration d'un switch Aruba (HP) en CLI`: https://www.clemanet.com/hp/configuration-vlan.php
.. _`Guide switch HP type Procurve`: http://idum.fr/spip.php?article295
.. _`Switch Aruba : configurer un Trunk LACP`: https://www.it-connect.fr/switch-aruba-configurer-un-trunk-lacp/
.. _`Medicat`: https://www.tech2tech.fr/medicat-lutilitaire-utlime-pour-le-depannage-informatique/ 
.. _`Utiliser diskpart`: http://www.aidewindows.net/win10/partition-recuperation.php
.. _`Ajouter des commandes au menu contextuel`: https://www.01net.com/astuces/ajouter-des-commandes-dos-au-menu-contextuel-de-lexplorateur-555224.html
.. _`Aouter un script au menu contextuel`: http://www.pumbaa.ch/blog/tutoriaux/?d=2016/12/05/23/12/10-ajouter-un-script-home-made-au-menu-contextuel-de-windows
.. _`Excel 1 ligne sur 2`: http://www.pcastuces.com/pratique/astuces/4180.htm
.. _`fix Cross Origin Request Security (CORS)`: http://testingfreak.com/how-to-fix-cross-origin-request-security-cors-error-in-firefox-chrome-and-ie/
.. _`Sysinternals pack`: https://docs.microsoft.com/en-us/sysinternals/
.. _`Certificat Exchange`: https://www.adminpasbete.fr/renouveler-certificat-exchange-2010-facilement/
.. _`Nettoyage WSUS`:  https://www.supinfo.com/articles/single/1912-liberation-espace-disque-serveur-wsus
.. _`CFG Sysprer sur VHD`: https://www.remylarrieu.com/fr/configurer-un-vhd-sysprep/
.. _`Script VHD+Sysprep`: https://github.com/remylarrieu/PowerShell/tree/master/Virtualization
.. _`UPD SysprepImg`: https://github.com/remylarrieu/PowerShell/tree/master/Virtualization
.. _`ex UPD SysprepImg`: https://www.remylarrieu.com/fr/mettre-a-jour-une-image-vhd/
.. _`Hyper-V replication in a workgroup or across domains using a self signed certificate`: https://nerddrivel.com/2016/03/07/hyper-v-replication-in-a-workgroup-or-across-domains-using-a-self-signed-certificate/
.. _`Get FSMO in CLI`: https://blog.alphorm.com/howto-lister-les-dcs-qui-detiennent-les-roles-fsmo/
.. _`Utilisation de points de contrôle`: https://docs.microsoft.com/fr-fr/virtualization/hyper-v-on-windows/user-guide/checkpoints
.. _`HowTo install AD on w10`: https://blogs.technet.microsoft.com/ashleymcglone/2016/02/26/install-the-active-directory-powershell-module-on-windows-10/
.. _`Script install AD on w10`: https://gallery.technet.microsoft.com/Install-the-Active-fd32e541
.. _Réplication du service DHCP et basculement entre 2 serveurs: https://vadmintic.wordpress.com/systemes-windows/haute-disponibilite-continuite-des-services/replication-du-service-dhcp/
.. _`Basic settings in 12 step`: https://techbast.com/2015/03/perform-a-basic-configuration-sophos-utm-in-12-simple-steps.html
.. _`UTM90 Remote Access via SSL`: https://www.sophos.com/en-us/medialibrary/PDFs/documentation/utm90_Remote_Access_Via_SSL_geng.pdf
