============
Informatique
============

.. contents:: Table of Contents
.. section-numbering::

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
        
####
        
--------
Matériel
--------

Information pour la gestion et maintenance des matériel

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

        depuis une invite de command Administrateur

        .. code:: powershell

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

    .. code:: powershell

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

        .. code:: powershell

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

PowerShell
==========

Installer le module PowerShell ActiveDirectory sous Windows 10
--------------------------------------------------------------
    
    :Liens_Web:
        * `HowTo install AD on w10`_ : Explication par l'auteur du script
            
        * `Script install AD on w10`_ : Le script lui même
    
    
Identifier les PC qui ne se sont pas connecter au domaine depuis au moins 180 Jours
-----------------------------------------------------------------------------------
       
    .. code:: powershell
       
        import-module ActiveDirectory
        $vdate = (Get-Date).adddays(-180)
        Get-ADComputer -filter {(Enabled -eq "True") -and (LastLogonDate -le $vdate)} -property * | ft LastLogonDate, CN
            # applique un filtre sur les élément qui ne sont pas désactivé et qui ne
            # se sont pas connecter de puis au moins 180 Jours
        
Pour ne pas filtrer le résultat et voir toutes les propriété
------------------------------------------------------------

    .. code:: powershell
        
        Get-ADComputer -filter * -property *
            # N.B : Fonctionne aussi avec get-ADUser
            
Identifier les comptes utilisateurs qui ne se sont pas connecter au domaine depuis au moins 180 Jours

    .. code:: powershell

        import-module ActiveDirectory
        $vdate = (Get-Date).adddays(-180)
        Get-ADuser -filter {(Enabled -eq "True") -and (LastLogonDate -le $vdate)} -property * | ft LastLogonDate, CanonicalName
            # applique un filtre sur les élément qui ne sont pas désactivé et qui ne
            # se sont pas connécter de puis au moins 180 Jours
                
Connaitre la date du dernier démarrage d'un serveur
---------------------------------------------------

    .. code:: powershell
    
        Get-CimInstance -ClassName Win32_OperatingSystem | Select CSName, LastBootUpTime
            # Windows2012 r2 et +
            
        # ou :
            
        $LastBootTime = (Get-WmiObject win32_Operatingsystem).LastBootUpTime
        [System.Management.ManagementDateTimeConverter]::ToDateTime($LastBootTime)

Se connecter à Exchange
-----------------------

    .. code:: powershell
    
        $Credentials = Get-Credential
        $ExSession = New-PSSession –ConfigurationName Microsoft.Exchange –ConnectionUri ‘http://SRV-MAIL.poree.local/PowerShell/?SerializationLevel=Full’ -Credential $Credentials –Authentication Kerberos
        Import-PSSession $ExSession
        # ...
        Remove-PSSession $ExSession

Connaitre le niveau fonctionnel Active Directory
------------------------------------------------

    .. code:: powershell

        (Get-ADDomain).DomainMode

            
####
            
-----------------------
Router, Firewall, Proxy
-----------------------

Sophos
======

    #. Basic settings

        :Liens_Web:
            * `Basic settings in 12 step`_

    #. Configurer le VPN en SSL
    
        :Liens_Web:
            * `UTM90 Remote Access via SSL`_ 

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
.. _`Utilisation de points de contrôle`: https://docs.microsoft.com/fr-fr/virtualization/hyper-v-on-windows/user-guide/checkpoints
.. _`HowTo install AD on w10`: https://blogs.technet.microsoft.com/ashleymcglone/2016/02/26/install-the-active-directory-powershell-module-on-windows-10/
.. _`Script install AD on w10`: https://gallery.technet.microsoft.com/Install-the-Active-fd32e541
.. _`Basic settings in 12 step`: https://techbast.com/2015/03/perform-a-basic-configuration-sophos-utm-in-12-simple-steps.html
.. _`UTM90 Remote Access via SSL`: https://www.sophos.com/en-us/medialibrary/PDFs/documentation/utm90_Remote_Access_Via_SSL_geng.pdf
