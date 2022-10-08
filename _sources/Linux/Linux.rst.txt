=====
LINUX
=====

.. contents::
    :backlinks: top
    :depth: 3
 
.. toctree::
   :titlesonly:
   :maxdepth: 2

   shell/shell
   multiscreen/multiscreen
   scripting/scripting
   UsersGroupsACL/UsersGroupsACL
   sysAdmin/sysAdmin
   network/network
   sharedFolders/sharedFolders
   hardwareMgnt/hardwareMgnt
   Raspberry/Raspberry
   bugError/bugError


####

Créer un alias permanent
========================

    :Liens_Web:
            * https://doc.ubuntu-fr.org/alias

    #. Editer le fichier '**.bashrc**'

        Il faut éditer le fichier '**~/.bashrc**' et ajouter cette commande 
        à la suite de la ligne : '**some more ls aliases**' ::

            if [ -f ~/.bash_aliases ]; then
                . ~/.bash_aliases
            fi

    #. Créer ou éditer le fichier '**~/.bash_aliases**'

        Ajouter le nouvel alias sous la forme ::

            alias nom_de_votre_alias='commande de votre alias'

            ex:
            alias python='/user/local/bin/python3.6'
            alias pip='/usr/local/bin/pip3.6'

    #. Relancer '.bashrc'
        ::

            source ~/.bashrc

####

---------------------
Configuration Système
---------------------

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
            
    #. Synchroniser le deamon avec les serveurs NTP
        ::
    
            service ntp stop
            ntpdate pool.ntp.org
            service ntp start
            
    #. Vérifier le décalage avec tous les serveur NTP
        ::
        
            ntpq -p

####

Changer la disposition du clavier
=================================
    ::
    
        sudo dpkg-reconfigure keyboard-configuration

####

----------------------
Administration système
----------------------

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

####

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

####

Pour créer un script qui s’exécute au démarrage du système
==========================================================

Pour faire en sorte qu'un script s’exécute au démarrage, il faut 2 éléments distincts :
    * Un script shell placé dans **/etc/init.d**
        # **N.B :** le "d" dans "int.d" signifie : deamon.
        C'est le nom des services sous linux
                                                
        Exemple de script : **/etc/init.d/skeleton**
            # Le fichier skeleton, dans linux, est donné a titre de modèle.
            Il est conseillé de se faire une copie du fichier
            dans ses documents et de travailler à partir de cette exemple
                                                
    * un script (notre code python) placé dans **/usr/sbin**
        # **N.B :** le "s" dans "sbin", signifie : system.
        Le bin représente les Binnaires,
        c'est à dire les exécutables.
        Le dossier sbin est donc le dossier
        qui contiens les exécutable du système,
        autrement dit les services.
                                                
Préparation du script shell
---------------------------
    
    #. Ouvrir une copie du fichier "skeleton" et modifier les ligne suivante :
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

    #. Après avoir effectuer les modification, enregistrer le fichier
       sous un autre nom (ex : blink_init) dans le dossier :
       ::
        
            /etc/init.d/
    
    #. Depuis le dossier **/etc/init.d**, ouvrir une fenêtre terminale
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
    
    #. Rendre le script exécutable
       ::
        
            chmod a+x [nom_du_script.py]
            
            ex: chmod a+x blink.py

####

Connaître la version du système
===============================

    #. Installation de lsb-release
        ::
    
            apt-get install lsb-release
                    
    #. Utilisation de lsb-release
        ::
    
            lsb_release -a

####

Connaître la version d'un paquet
================================

    #. Installation de apt-show-versions
        ::

            apt-get install apt-show-versions

    #. Utilisation de apt-show-versions
        ::
    
            apt-show-versions *nom_du_paquet*

####

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

####

------
Réseau
------

SSH
===

Activer la connections ssh
--------------------------

    :Liens_Web:
              * https://coagul.org/drupal/article/installation-et-utilisation-ssh-sous-linux
            
    :: 
    
        sudo aptitude install openssh-client openssh-server

Désactiver la demande de mot de passe de la commande sudo au travers du ssh
---------------------------------------------------------------------------

    #. Ajouter l'utilisateur au fichiers sudoers
    
        * Ouvrir le fichier /etc/sudoers
        * Ajouter A LA FIN DU FICHIER l'utilisateur sous la forme : ::

            [nom_d'utilisateur] ALL=(ALL) NOPASSWD: ALL
            
            ex :
            polter ALL=(ALL) NOPASSWD: ALL
            
    #. Modifier le fichier /etc/ssh//sshd_config

        * Repérer et commenter la ligne : ::
        
            #PermitRootLogin prohibit-password
            
        * Ajouter juste après : ::
        
            PermitRootLogin yes

####

Pour pouvoir se connecter en RDP sur un poste Linux
===================================================

    :Liens_Web:
            * https://www.maketecheasier.com/enabling-remote-desktop-access-on-raspberry-pi/
            * https://doc.ubuntu-fr.org/xrdp

    ::
    
            sudo apt-get install xrdp

####

Pour faire du XForwarding
=========================

    :Liens WEB:
            * http://frans-web.com/x11-forwarding-en-ssh-via-putty.html
                # Guide pas à pas pour la mise en place du Xforwarding (N.B: utilise un serveur X virtuel)

            * https://doc.ubuntu-fr.org/tutoriel/xforwarding
                # Autre tuto utilisant un serveur X virtuel

            * https://www.it-connect.fr/chapitres/deport-daffichage-avec-ssh-x11-forwarding/
                # Guide simplifier utilisant le serveur X11

    #. Activation coté serveur (linux distant)

        Dans le fichier **/etc/ssh/sshd_config**, s'assurer que les 2 paramètres suivant sont bon: ::

            X11Forwarding yes
            X11DisplayOffset 10

        **N.B**: Si le serveur distant n'a pas de serveur graphique, utiliser la méthode proposée
             sur le `wiki ubuntu <https://doc.ubuntu-fr.org/tutoriel/xforwarding>`_.

    #. Mise en place coté client (Windows)

        #. Installation du serveur X vidéo sur le client

            Télécharger et installer `xming <https://sourceforge.net/projects/xming/files/latest/download>`_

    #. Activer le mode X11 forwarding dans Putty ::
        
        Connection
            \_SSH
                \_X11   --> Enable X11 forwarding

    #. Ouvrir une application graphique distante

        Ajouter une esperluette à la suite de la commande. ::

            ex:
            xterm&

            ou firefox&

####

VNCserver
=========

    :Liens_Web:
            * https://www.digitalocean.com/community/tutorials/how-to-install-and-configure-vnc-on-ubuntu-18-04
                # Installation et mise en place du serveur VNC depuis la console linux

            * https://youtu.be/jnpWYko4FNo
                # Modification du port d'écoute (defaut: 5901)

####

Pour mettre une IP fixe sur une interfaces réseau
=================================================

:Liens Web:
            * http://www.cyberciti.biz/tips/howto-ubuntu-linux-convert-dhcp-network-configuration-to-static-ip-configuration.html

            * https://inetdoc.developpez.com/tutoriels/linux/configurer-interface-reseau-ethernet/?utm_source=dlvr.it&utm_medium=twitter
                # Tuto complet sur la configuration des interfaces réseau

    Ouvrir le fichiers de configuration des interfaces :
    ::
            
        sudo nano /etc/network/interfaces

    Remplacer :
    ::
    
        iface eth0 inet dhcp

        par:
        
        iface eth0 inet static
        address 172.16.32.254
        netmask 255.255.255.0
        network 172.16.32.0 (optionel)
        gateway 172.16.32.1 (optionel)

                    
    Redémarrer le réseau
    ::
    
        /etc/init.d/networking restart

####

Pour active le WIFI
===================

:liens Web:
           * https://wiki.debian.org/fr/WiFi/HowToUse

    Ouvrir le fichiers de configuration des interfaces :
    ::
    
            sudo nano/etc/network/interfaces

    Remplacer :
    ::
    
        iface wlan0 inet manual
        
        par :             
        
        iface wlan0 inet dhcp
        
    Redémarrer les interfaces réseau
    ::
    
            ifdown -a && ifup -a

####

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
                    
####

Créer un dossier partagé avec samba
===================================

:Liens_Web:
            * https://help.ubuntu.com/community/How%20to%20Create%20a%20Network%20Share%20Via%20Samba%20Via%20CLI%20%28Command-line%20interface/Linux%20Terminal%29%20-%20Uncomplicated%2C%20Simple%20and%20Brief%20Way%21

    #. Installation de samba
        ::

            sudo apt-get update
            sudo apt-get install samba

    #. Création du mot de passe pour l'utilisateur

        Samba gère les mot de passe dans un espace de stockage différent du reste du système. ::

            sudo smbpasswd -a <user_name>

            ex:
            sudo smbpasswd -a pi

    #. Création du dossier à partager

        Par commodité, ce dossier est défini dans le dossier utilisateur (~) directement. ::

            sudo mkdir ~/share

    #. Attribution des droits sur le dossier pour l'utilisateur et pour le groupe de l'utilisateur
        ::

            sudo chown <user_name> /dossier/partagé
            sudo chown :<user_name> /dossier/partagé

            ex:
            sudo chown pi ~/share
            sudo chown :pi ~/share

    #. Modification du fichier 'smb.conf'
        #. Création d'une copie du fichier (par sécurité) ::

            sudo cp /etc/samba/smb.conf ~
                # cette copie se trouve dans '/home/<user>/'

        #. Édition de smb.conf ::

            sudo vim /etc/samba/smb.conf

        #. Ajout, à la fin du fichier, des informations sur le dossier partagé
                ::
                    
                    [<Nom_du_dossier_partage>]
                    path = /home/<user_name>/<folder_name>
                    valid users = <user_name>
                    read only = no

                    # N.B : Pour autoriser un groupe à la place d'un utilisateur:
                    valid users = @<group_name>

                    ex:
                    ...
                    valid users = @volab

            :/!\\Attention/!\\:
                        * Le bloc commençant par **[<folder_name>]** doit être séparer du code
                          existant par au moins une ligne vide (hors commentaire)a

                        * Un espace doit entouré chaque signe '='. ex: ' = '

    #. Redémarrage du service samba ::

        sudo service smbd restart

    #. Accès au dossier partagé 
           
        #. Depuis Windows ::

            \\IP_Distante\share
            ou
            \\hostname\share

            ex:
            \\192.168.1.31\share
            \\pi_crachTest\share

Monter un répertoire distant
----------------------------

    :Liens_Web:
                https://doc.ubuntu-fr.org/tutoriel/monterpartagewindows
                    # exemple d'utilisation en manuel et en automatique

    #. Création du répertoire de montage

        N.B: c'est le répertoire qui va accueillir le répertoire distant.
        ::

            sudo mkdir /media/<nom_du_nouveau_repertoire>

            ex:
            sudo mkdir /media/volab

    #. Création d'un fichier "credentials"

        #. Créer le fichier dans le répertoire 'root' ::

            sudo vim /root/.smbcreds

        #. Renseigner les identifiants de l'utilisateur distant ::

            username=<Nom_d'utilisateur>
            password=<mot_de_passe>
            domaine=>domaine>       # Facultatif

Mode Manuel
^^^^^^^^^^^
    #. Montage ::

        sudo mount -t cifs -o username=utilisateur_ubuntu,rw,iocharset=utf8,file_mode=0777,dir_mode=0777 //<adressIP_serveurFichier>/<repertoireSource> /media/<partage>

    **N.B**: il est conseiller de tester le montage à la main avant de monter le lecteur 
    automatiquement au démarrage.

    #. Démontage ::

        umount /media/<partage>

Mode Automatique
^^^^^^^^^^^^^^^^
    #. Copier le fichier 'fstab' ::

        sudo cp /etc/fstab /etc/fstab_sauvegarde

    #. Editer 'fstab'

        Ajouter le nouveau partage à la fin du fichier ::

            //<adresse_distante>/<partage>   /media/<partage> cifs credentials=/root/.smbcreds,iocharset=utf8   0   0

    #. Redémarrage et vérification

        * Redémarrer le serveur et vérifier que les données du partage distant sont bien présente.

        * Faire un test de lecture / écriture pour s'assurer que les permissions son correctement
          accordés.

####

Télécharger un fichier en ligne de commande (wget)
==================================================

:Liens_Web:
            * https://doc.ubuntu-fr.org/wget
            
    ::
    
        ex :
        wget https://github.com/docker-library/mongo/blob/2e3e1bdbb31389c8bc8d43f5a3cc439134b7956b/3.6/Dockerfile
        
####

--------
Weblinks
--------
            
.. target-notes::