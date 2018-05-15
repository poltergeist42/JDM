=====
LINUX
=====

rappel des commandes de bases
=============================

:Liens web:
            * http://wiki.linux-france.org/wiki/Les_commandes_fondamentales_de_Linux

        +--------------------------+--------------------------------------------------+
        |    --- Command ---       |      --- Meaning ---                             |
        +==========================+==================================================+
        | ls                       | list files in current directory                  |
        |                          |    # pour afficher la list de tous les éléments, |
        |                          |    même cachés                                   |
        |                          |                                                  |
        |                          |        * ls -a                                   |
        +--------------------------+--------------------------------------------------+
        | cd                       | change directory                                 |
        +--------------------------+--------------------------------------------------+
        | pwd                      | print working directory                          |
        +--------------------------+--------------------------------------------------+
        | rm                       | filename remove filename                         |
        |                          |    # Pour forcer la suppression d'un             | 
        |                          |    # répertoir non vide                          |
        |                          |                                                  |
        |                          |        * rm -Rf monrepertoire                    |
        +--------------------------+--------------------------------------------------+
        | mkdir *directoryname*    | make directory with directoryname                |
        +--------------------------+--------------------------------------------------+
        | rmdir *directoryname*    | remove empty directory                           |
        +--------------------------+--------------------------------------------------+
        | cat textfile             | display contents of textfile in the terminal     |
        +--------------------------+--------------------------------------------------+
        | mv oldfile newfile       | move (rename) oldfile to newfile                 |
        +--------------------------+--------------------------------------------------+
        | cp oldfile newfile       | copy oldfile to newfile                          |
        +--------------------------+--------------------------------------------------+
        | man command              | display manual of command                        |
        +--------------------------+--------------------------------------------------+
        | date                     | read system date/time                            |
        +--------------------------+--------------------------------------------------+
        | echo                     | echo what is typed back in the terminal          |
        +--------------------------+--------------------------------------------------+
        | grep                     | search program that uses regular expressions     |
        +--------------------------+--------------------------------------------------+
        | sudo                     | perform as root user                             |
        +--------------------------+--------------------------------------------------+
        | ./program                | run program                                      |
        +--------------------------+--------------------------------------------------+
        | exit                     | quit terminal session                            |
        +--------------------------+--------------------------------------------------+
        
------------------------------------------------------------------------------------------

rappel des raccourcis de navigation dans le shell
=================================================

        +----------------------------+----------------------------------------------+
        |   Key or Key Combination   |                  Function                    |
        +============================+==============================================+
        | Ctrl + A                   | Move cursor to beginning of line             |
        +----------------------------+----------------------------------------------+
        | Ctrl + C                   | Stop currently-executing process             |
        +----------------------------+----------------------------------------------+
        | Ctrl + D                   | Log out—equivalent to typing exit            |
        +----------------------------+----------------------------------------------+
        | Ctrl + E                   | Move cursor to end of line                   |
        +----------------------------+----------------------------------------------+
        | Ctrl + H                   | Delete character in front of cursor          |
        +----------------------------+----------------------------------------------+
        | Ctrl + L                   | Clear terminal                               |
        +----------------------------+----------------------------------------------+
        | Ctrl + R                   | Search command history                       |
        +----------------------------+----------------------------------------------+
        | Ctrl + Z                   | Suspend a program                            |
        +----------------------------+----------------------------------------------+
        | Arrow Left/Right           | Move cursor left/right one character         |
        +----------------------------+----------------------------------------------+
        | Arrow Up/Down              | Scrolls through previous commands            |
        +----------------------------+----------------------------------------------+
        | Shift + PageUp/PageDown    | Move one page up or down in terminal output  |
        +----------------------------+----------------------------------------------+
        | Tab                        | Command or file name completion              |
        +----------------------------+----------------------------------------------+
        | Tab Tab                    | Shows all command or file name possibilities |
        +----------------------------+----------------------------------------------+

------------------------------------------------------------------------------------------

activer le compte root
======================
    ::
    
        sudo passwd root
        
------------------------------------------------------------------------------------------

faire une élévation valable toute la durée de la session
========================================================
    ::
    
        sudo -s
        # N.B : Le prompt devrais passer en root@[nom_de_machine]
        
------------------------------------------------------------------------------------------

Gestion des permissions
=======================

Groupes
-------

    #. Connaître la liste des groupes aux quels appartient un utilisateur
        ::
    
            groups [nom_d'utilisateur]
            
            ex :
            
            $ groups polter
            polter : polter adm cdrom sudo dip plugdev
            
    #. Ajouter un utilisateur à un groupes
        ::

            sudo usermod -aG [nom_du_groupe] [nom_de_l'utilisateur]
            
            ex :
            
            $ usermod -aG docker polter
            
ACL (Propriétaire, RWX)
-----------------------

    #. Changer le propriétaire d'un dossier (ownership)
        ::
    
            chown root:[nom_d'utilisateur] [nom_du_dossier]/
            
            ex :
            
                chown root:volab echanges/
                
    #. Mettre les droits sur un dossier
        ::
    
            chmod -R 0777 [nom_du_dossier]
            
            ex :
            
                chmod -R 0777 echanges

    #. Pour rendre un fichier "Exécutable"
        ::

                chmod a+x [nomDuFichier]

------------------------------------------------------------------------------------------

Date et heure
=============

Conaitre la date et l'heure du système
--------------------------------------
    ::
    
        date
        
Synchronyser la date et l'heure avec un serveur de temp (NTP)
-------------------------------------------------------------

:Liens_Web:
            * https://www1.zonewebmaster.eu/serveur-debian-general:regler-date-heure
            * https://www.system-linux.eu/index.php?post/2010/01/05/Mettre-vos-serveurs-%C3%A0-la-bonne-heure-avec-NTP
                # N.B : Les explications ci-dessous sont un mixe en les 2 liens
                
    #. Télécharger et installer les paquets
        ::
        
            sudo apt-get update
            sudo apt-get install ntp ntpdate
            
    #. Editer le fichier ntp.conf et ajouter les serveurs NTP.fr
        ::
        
            nano /etc/ntp.conf
            
            ## Ajouter les serveur NTP français
            server 0.fr.pool.ntp.org prefer # Le terme 'prefer' indique le serveur NTP
                                            # à utiliser de préférence
            server 1.fr.pool.ntp.org
            server 2.fr.pool.ntp.org
            server 3.fr.pool.ntp.org
            
    #. Synchronyser le deamon avec les serveurs NTP
        ::
    
            service ntp stop
            ntpdate pool.ntp.org
            service ntp start
            
    #. Vérifier le décallage avec tous les serveur NTP
        ::
        
            ntpq -p

------------------------------------------------------------------------------------------

Arrêter / Démarrer les services (deamon)
========================================

    #. Arrêter / démarrer un service
        ::
        
            service [nom_du_service] [action]
            
            ex :
            service ntp stop
            
    #. Connaitre la liste est l'état de tous les services
        ::
        
            service --status-all

------------------------------------------------------------------------------------------

Créer une tâche planifié (cron)
===============================

:Liens Web:     
                - https://openclassrooms.com/courses/reprenez-le-controle-a-l-aide-de-linux/executer-un-programme-a-une-heure-differee
                - https://technique.arscenic.org/commandes-linux-de-base/article/cron-gestion-des-taches-planifiees
                
:cron:          C'est le soft qui exécute les taches planifiées
:crontab:       C'est le gestionnaire des taches planifiées. Il y en a un par utilisateur

    #. Option de crontab : ::
    
        crontab -l
            # Pour lister les tâches planifiées
            
        crontab -e
            # Pour Créer / éditer les tâches planifiées
            
        crontab -r
            # Pour supprimer le crontab
            # !!! Suppression immédiate, pas d'avertissement, pas de confirmation



------------------------------------------------------------------------------------------

connaître la version du système
===============================

installation de lsb-release
---------------------------
    ::
    
        apt-get install lsb-release
                    
utilisation de lsb-release
--------------------------
    ::
    
        lsb_release -a
                    
------------------------------------------------------------------------------------------

connaître la version d'un paquet
================================

installation de apt-show-versions
---------------------------------
    ::
    
        apt-get install apt-show-versions
                    
utilisation de apt-show-versions
--------------------------------
    ::
    
        apt-show-versions *nom_du_paquet*

------------------------------------------------------------------------------------------

Pour copier des fichiers en root depuis l'interface graphique
=============================================================

        Installation du logiciel "gksu"
        ::
        
            apt-get install gksu
            
        Ouvrir l'explorateur de fichier.
        dans le menu **"Aide"**, cliquer sur l'item **"A propos"**
        dans la fenêtre d'information qui s'affiche, relever le nom de l'explorateur
        
            ex : Thunar
            
            
        Dans une fenêtre terminal entrer :
            ::
            
                gksu *nom_de_l_explorateur*
            
            ex : gksu Thunar
            
        L'explorateur de fichier doit s'ouvrir. Un bandeau orange vous signal que l'on se
        trouve sur le compte root.

------------------------------------------------------------------------------------------

Changer la disposition du clavier
=================================
    ::
    
        sudo dpkg-reconfigure keyboard-configuration

------------------------------------------------------------------------------------------

SSH
===

Activer la connection ssh
-------------------------

:Liens_Web:
            * https://coagul.org/drupal/article/installation-et-utilisation-ssh-sous-linux
            
    :: 
    
        sudo aptitude install openssh-client openssh-server

Désactiver la demande de mot de passe de la commande sudo au travers du ssh
---------------------------------------------------------------------------

    #. Ajouter l'utilisateur au fichiers sudoers
    
        - Ouvrir le fichier /etc/sudoers
        - Ajouter A LA FIN DU FICHIER l'utilisateur sour la forme : ::
        
            [nom_d'utilisateur] ALL=(ALL) NOPASSWD: ALL
            
            ex :
            polter ALL=(ALL) NOPASSWD: ALL
            
    #. modifier le fichier /etc/ssh//sshd_config
    
        - Repérer et commenter la ligne : ::
        
            #PermitRootLogin prohibit-password
            
        - Ajouter juste après : ::
        
            PermitRootLogin yes
 
------------------------------------------------------------------------------------------

Pour pouvoir se connecter en RDP sur un poste Linux
===================================================

:Liens_Web:
            * https://www.maketecheasier.com/enabling-remote-desktop-access-on-raspberry-pi/
            * https://doc.ubuntu-fr.org/xrdp

    ::
    
            sudo apt-get install xrdp

------------------------------------------------------------------------------------------

pour faire du XForwarding
=========================

:Liens WEB:
            * http://blog.sckyzo.com/x11-forwarding-en-ssh-via-putty-windows/
            * http://frans-web.com/?p=18
                    
------------------------------------------------------------------------------------------

Pour mettre une IP fixe sur une interfaces réseau
=================================================

:Liens Web:
           * http://www.cyberciti.biz/tips/howto-ubuntu-linux-convert-dhcp-network-configuration-to-static-ip-configuration.html

    Ouvrir le fichiers de configuration des interfaces :
    ::
            
            sudo nano /etc/network/interfaces

    Remplacer :
    
    ::
    
                iface eth0 inet dhcp

            par
                iface eth0 inet static
                address 172.16.32.254
                netmask 255.255.255.0
                network 172.16.32.0 (optionel)
                gateway 172.16.32.1 (optionel)

                    
    Redémarrer le réseau
    ::
    
                /etc/init.d/networking restart

------------------------------------------------------------------------------------------

Pour active le WIFI
===================

:liens Web:
           * https://wiki.debian.org/fr/WiFi/HowToUse

    Ouvrir le fichiers de configuration des interfaces :
    ::
    
            sudo nano/etc/network/interfaces

    remplacer :
    ::
    
            iface wlan0 inet manual
        
        par             
            iface wlan0 inet dhcp
        
    Redémarrer les interfaces réseau
    ::
    
            ifdown -a && ifup -a

------------------------------------------------------------------------------------------

Se connecter a un réseau wifi en ligne de commande
==================================================

:liens Web:
           * http://korben.info/comment-se-connecter-a-un-reseau-wifi-en-ligne-de-commande-sous-linux.html

    Démarrer la carte wifi
    ::

        sudo ifconfig wlan0 up
                    
    Rechercher les différents réseau a porter
    ::
    
        iwlist ath0 scan
                    
------------------------------------------------------------------------------------------

Connaître la liste des matériel usb
===================================
    ::

            lsusb

------------------------------------------------------------------------------------------

Connaître l’espace disque utilise et celui disponible
=====================================================
    ::

            df -h
                    
------------------------------------------------------------------------------------------

Les ports séries
================

:Liens Web:
           * http://www.instructables.com/id/Read-and-write-from-serial-port-with-Raspberry-Pi/

Rappel (équivalence de la notation Windows / Linux
    
    +---------+------------+
    | Windows |    Linux   |
    +=========+============+
    | COM1    | /dev/ttyS0 |
    +---------+------------+
    | COM2    | /dev/ttyS1 |
    +---------+------------+
    | COM3    | /dev/ttyS2 |
    +---------+------------+
    | COM4    | /dev/ttyS3 |
    +---------+------------+
                        
Connaître la liste des ports série :
------------------------------------
    ::
    
        ls /dev/tty*
            # La commande retourne généralement plus de 50 tty.
              Cependant, les tty associés au port USB disposent d'une nomenclature différente.
              Ils contiennent habituellement USB ou ACM (Abstract Control Model)
                        
interroger le journal sur les ports série :
-------------------------------------------
    ::

        dmesg | grep tty
            # Information plus complète qu'avec l'instruction précédente

------------------------------------------------------------------------------------------

faire du multi-screen  sur une fenêtre terminal
===============================================

Installation de screen
----------------------
::

    sudo apt-get install screen
                
Lancer l'application "screen"
-----------------------------
::

    screen
                
Liste des commandes des bases pour screen
-----------------------------------------

    +--------------------------+------------------------------------------------------------+
    | Raccourcis clavier       |                        Fonctions                           |
    +==========================+============================================================+
    | screen                   | Lancer screen                                              |
    +--------------------------+------------------------------------------------------------+
    | CTRL+[a]    --> [c]      | Ouvrir un nouveau screen                                   |        
    +--------------------------+------------------------------------------------------------+
    | CTRL+[a]    --> [espace] | Basculer vers le screen suivant                            |
    +--------------------------+------------------------------------------------------------+
    | CTRL+[a][a]              | Basculer entre le teminal actif et le dernier consulté     |
    +--------------------------+------------------------------------------------------------+
    | CTRL+[a]    --> d        | Détacher la session screen (permet) de fermer la console   |
    |                          | sans arréter les process                                   |
    +--------------------------+------------------------------------------------------------+
    | screen -r                | Se reconnecter à la session screen tel qu'elle était       |
    |                          | lors du détachement avec CTRL[a][d]. On parle de rattacher |
    |                          | le screen                                                  |
    +--------------------------+------------------------------------------------------------+
    | exit                     | Ferme le screen courrant                                   |
    +--------------------------+------------------------------------------------------------+

------------------------------------------------------------------------------------------

pour créer un script qui s’exécute au démarrage du système
==========================================================

Pour faire en sorte qu'un script s’exécute au démarrage, il faut 2 éléments distincts :
    * Un script shell placé dans **/etc/init.d**
        # **N.B :** le "d" dans "int.d" signifie : deamon.
        C'est le nom des services sous linux
                                                
        exemple de script : **/etc/init.d/skeleton**
            # Le fichier skeleton, dans linux, est donné a titre de model.
            Il est conseillé de se faire une copie du fichier
            dans ses documents et de travailler à partir de cette exemple
                                                
    * un script (notre code python) placé dans **/usr/sbin**
        # **N.B :** le "s" dans "sbin", signifie : system.
        Le bin repésente les Binnaires,
        c'est à dire les executables.
        Le dossier sbin est donc le dossier
        qui contien les executable du systeme,
        autremant dit les services.
                                                
Préparation du script shell
---------------------------
    
    #. ouvrir une copie du fichier "skeleton". et modifier les ligne suivante :
    
    ::

        #! /bin/sh
        ### BEGIN INIT INFO
        # Provides:          skeleton                   <-- le titre
        # Required-Start:    $remote_fs $syslog
        # Required-Stop:     $remote_fs $syslog
        # Default-Start:     2 3 4 5
        # Default-Stop:      0 1 6
        # Short-Description: Example initscript         <-- description courte
        # Description:       This file should be used   <-- description longue
        #                    to construct scripts to be
        #                    placed in /etc/init.d.
        ### END INIT INFO

        # Author: Foo Bar <foobar@baz.org>              <-- votre nom
        #
        # Please remove the "Author" lines above and replace them
        # with your own name if you copy and modify this script.

        # Do NOT "set -e"

        # PATH should only include /usr/* if it runs after the mountnfs.sh script
        PATH=/sbin:/usr/sbin:/bin:/usr/bin
        DESC="Description of the service"
        NAME=daemonexecutablename                       <-- le nom de votre deamon        
        DAEMON=/usr/sbin/$NAME                          <-- le chemin de votre script si
                                                            ce dernier est différent du
                                                            chemin ci contre

        #! /bin/sh
        ### BEGIN INIT INFO
        # Provides:          skeleton
        # Required-Start:    $remote_fs $syslog
        # Required-Stop:     $remote_fs $syslog
        # Default-Start:     2 3 4 5
        # Default-Stop:      0 1 6
        # Short-Description: Example initscript
        # Description:       This file should be used to construct scripts to be
        #                    placed in /etc/init.d.
        ### END INIT INFO

        # Author: Foo Bar <foobar@baz.org>
        #
        # Please remove the "Author" lines above and replace them
        # with your own name if you copy and modify this script.

        # Do NOT "set -e"

        # PATH should only include /usr/* if it runs after the mountnfs.sh script
        PATH=/sbin:/usr/sbin:/bin:/usr/bin
        DESC="Description of the service"
        NAME=daemonexecutablename
        DAEMON=/usr/sbin/$NAME
        DAEMON_ARGS="--options args"
        PIDFILE=/var/run/$NAME.pid
        SCRIPTNAME=/etc/init.d/$NAME

    #. après avoir effectuer les modification, enregistrer le fichier
    sous un autre nom (ex : blink_init) dans le dossier :
    
        ::
        
            /etc/init.d/
    
    #. depuis le dossier **/etc/init.d**, ouvrir une fenêtre terminale
    et rendre le script exécutable avec la commande suivante :
    
        ::
    
            chmod a+x [nom_du_script]
            
        ex : chmod a+x blink_init
 
Préparation du script python
----------------------------
     
    #. Si se n'est pas déjà fait, éditer le script et ajouter la ligne suivante
    sur la première ligne de votre fichier
    
        ::
        
            #!/usr/bin/env python3

    #. Copier le fichier dans le dossier **/usr/sbin/**
    
    #. rendre le script exécutable
        ::
        
            chmod a+x [nom_du_script.py]
        
        ex: chmod a+x blink.py

------------------------------------------------------------------------------------------

linux rediriger sortie vers null
================================

:Liens_Web:
            * http://www.lanterne-rouge.info/article-que-signifie-dev-null-2-1-70233357.html
                # Une explication (fr) sur les sortie STDOUT et STDERR
                
------------------------------------------------------------------------------------------

Télécharger un fichier en ligne de commande (wget)
==================================================

:Liens_Web:
            * https://doc.ubuntu-fr.org/wget
            
    ::
    
        ex :
        wget https://github.com/docker-library/mongo/blob/2e3e1bdbb31389c8bc8d43f5a3cc439134b7956b/3.6/Dockerfile
        
------------------------------------------------------------------------------------------

Emplacement des programmes
==========================

    #. Connaitre l'emplacement d'un programme
        ::
        
            whereis [Nom_du_programme]

            ex:
            whereis python

    #. Emplacement par défaut des programmes

        Les programmes sont généralement placés dans **'usr/bin/'**. Par convention, les programmes tiers
        que nous installons, doivent être installés dans : **'/usr/local/'**

------------------------------------------------------------------------------------------

Créer un dossier partagé avec samba
===================================

:Liens_Web:
            * https://help.ubuntu.com/community/How%20to%20Create%20a%20Network%20Share%20Via%20Samba%20Via%20CLI%20%28Command-line%20interface/Linux%20Terminal%29%20-%20Uncomplicated%2C%20Simple%20and%20Brief%20Way%21

    #. installation de samba
        ::

            sudo apt-get update
            sudo apt-get install samba

    #. Création du mot de passe pour l'utilisateur

        Samba gère les mot de passe dans un espace de stockage différent du reste du système. ::

            sudo smbpassword -a <user_name>

            ex:
            sudo smbpassword -a pi

    #. Création du dossier à partager

        Par commodité, ce dossier est défini dans '/home' directement. ::

            sudo mkdir /home/share

    #. Attribution des droits sur le dossier pour l'utilisateur et pour le groupe de l'utilisateur
        ::

            sudo chown <user_name> /dossier/partagé
            sudo chown :<user_name> /dossier/partagé

            ex:
            sudo chown pi /home/share
            sudo chown :pi /home/share

    #. Modification du fichier 'smb.conf'
        #. Création d'une copie du fichier (par sécurité) ::

            sudo cp /etc/samba/smb.conf ~
                # cette copie se trouve dans '/home/<user>/'

        #. Edition de smb.conf ::

            sudo vim /etc/samba/smb.conf

        #. Ajout, à la fin du fichier, des informations sur le dossier partagé
                ::
                    
                    [<folder_name>]
                    path = /home/<user_name>/<folder_name>
                    valid users = <user_name>
                    read only = no

            :/!\\Attention/!\\:
                        * Le bloc commençant par **[<folder_name>]** doit être séparer du code
                          existant par au moins une ligne vide (hors commentaire)a

                        * Un espace doit entouré chaque signe '='. ex: ' = '

    #. Redémarrage du service samba ::

        sudo service smbd restart

    #. Accès au dossier partagé ::

        \\IP_Distante\share
        ou
        \\hostname\share

        ex:
        \\192.168.1.31\share
        \\pi_crachTest\share
