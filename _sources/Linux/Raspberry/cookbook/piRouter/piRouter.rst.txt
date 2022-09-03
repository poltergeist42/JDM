========================
Raspberry Pi as a router
========================

.. contents::
    :backlinks: top
    :depth: 3

####

--------
Objectif
--------

L'objectif est de transformer le Raspberry Pi en router. La carte wifi doit se connecter à un point
d'accès mobile tel q'un téléphone ou un router 4G / 5G. Le trafic est ensuite routé vers la carte
Ethernet. 

Un serveur DHCP est également configuré sur la carte Ethernet.

Schéma 
======

    .. image:: ./images/schema.svg
        :width: 520 px
        :align: center

####

-------------------------------------
Configuration des points d'accès wifi
-------------------------------------

:Liens_Web:
    * `Setting up Raspberry Pi Wi-Fi`_

.. _`Setting up Raspberry Pi Wi-Fi`: https://pimylifeup.com/setting-up-raspberry-pi-wifi/

.. warning::
    Attention, il est important de respecter la casse du SSID (majuscule / minuscule). De plus,
    un SSID ne peux pas contenir d'espace.

L'ajout de SSID peut s'effectuer de 2 façons diférentes.

Configuration à l'aide de l'outil **"Raspi-config"**
====================================================

 Naviguer dans les menus pour configurer le SSID du wifi

    #.
        .. code:: shell

           sudo raspi-config

    #.
        .. image:: ./images/raspiConf1.png
            :width: 520 px
            :align: center

    #.
        .. image:: ./images/raspiConf2.png
            :width: 520 px
            :align: center

    #.
        .. image:: ./images/raspiConf3.png
            :width: 520 px
            :align: center

    #.
        .. image:: ./images/raspiConf4.png
            :width: 520 px
            :align: center

Configuration manuelle
======================

Il est possible de configurer les point d'accès directement depuis le fichier de configuration.

    #. Editer le fichier "wpa_supplcant"
        .. code:: shell

            cd /etc/wpa_supplicant/
            sudo vi wpa_supplicant.conf

    #. Ajouter les informations Wifi (SSID + Password) à la fin du fichier
        .. code:: shell

            network={
            ssid="The SSID of your network (eg. Network name)"
            psk="Your Wifi Password"
            }

####

-------
Routeur
-------

:Liens_Web:
    * `wlan0 to eth0 bridge`_

.. _`wlan0 to eth0 bridge`: https://forums.raspberrypi.com/viewtopic.php?t=247584

Configuration d'une IP statique sur eth0
========================================

    #. Editer le fichier dhcpcd.conf

       .. code:: shell

          sudo vim /etc/dhcpcd.conf

    #. Définir l'adresse IP fixe et les DNS

       Ici, il n'est pas nécessaire de renseigner la passerelle car puisqu'il n'y en à qu'une (wlan0),
       elle est utilisée par défault.

       La définission des DNS est facultative. Par défault, les DNS sont fournis par l'ISP.

        
       .. code:: shell

          interface eth0
          static ip_address=192.168.1.254/24
          static domain_name_servers=1.1.1.1 9.9.9.9

    #. Redémarrer le Pi

       .. code:: shell

          sudo reboot

    #. Editer le fichier de configuration du Kernel

       .. code:: shell

          sudo /etc/sysctl.conf
    
    #. Activer l'option router dans le Kernel

       .. code:: shell

          # Uncomment the next line to enable packet forwarding for IPv4
          net.ipv4.ip_forward=1

    #. Installation d'Iptable

       .. code:: shell
          
          sudo apt-get update
          sudo apt-get install iptables-persistent

    #. Ajout du fichier "rules.v4" au group de l'utilisateur

       .. code:: shell
          
          sudo chgrp pi /etc/iptables/rules.v*
          sudo chmod 664 /etc/iptables/rules.v*

    #. Création d'une table persistante

       .. code:: shell

          sudo iptables -t nat -A POSTROUTING -o wlan0 -j MASQUERADE
          sudo iptables-save >/etc/iptables/rules.v4

####

------------
Serveur DHCP
------------

:Liens_Web:
    * `How to Use Raspberry Pi as a DHCP Server`_

.. _`How to Use Raspberry Pi as a DHCP Server`: https://raspberrytips.com/dhcp-server-on-raspberry-pi/

    #. Installation de dnsmasq

       .. code:: shell

          sudo apt install dnsmasq

    #. Editer le fichier de configuration de dnsmasq

       .. code:: shell
          
          sudo vim dnsmasq.conf

    #. Ajouter la configuration du DHCP en fin de fichier

       .. warning::

          Vérifier que les options et exemples déjà renseignés ne sont pas en conflit avec les
          informations ajoutées.

       .. code::

           # TP : 220814
           # Configuration manuelle du DHCP
           interface=eth0
           bind-dynamic
           domain-needed
           bogus-priv
           dhcp-range=192.168.1.50,192.168.1.80,255.255.255.0,12h

        
       .. image:: ./images/dnsmasq.png
           :width: 520 px
           :align: center

    #. Redémarrer le service dnsmasq

       .. code:: shell

          sudo service dnsmasq restart

####

------
Webmin
------

:Liens_Web:
    * `Install Webmin`_

.. _`Install Webmin`: https://raspberrytips.com/install-webmin-raspberry-pi/

    #. Editer le fichier source.list

       .. code:: shell
        
           sudo vim /etc/apt/sources.list

    #. Ajouter le dépôt à la fin du fichier

       .. code:: shell

          deb https://download.webmin.com/download/repository sarge contrib

    #. Installation de la clef GPG

       .. code:: shell

          wget http://www.webmin.com/jcameron-key.asc
          sudo apt-key add jcameron-key.asc

    #. Installation de webmin

       .. code:: shell

          sudo apt update
          sudo apt install webmin

    #. Accéder à webmin depuis une page web

       .. code:: html

          https://IP_ADDRESS:10000

       * Le port part défaut est le TCP 10000

       * Les identifiants sont les identifiants de l'utilisateurs sur le Pi

####

--------------------
Serveur d'impression
--------------------

:Liens_Web:
    * `Comment Installer une Imprimante sur Raspberry Pi (CUPS)`_

.. _`Comment Installer une Imprimante sur Raspberry Pi (CUPS)`: https://raspberrytips.fr/installer-imprimante-raspberry-pi/

Ici aucune dificulté. Il suffit de suivre un tuto installation et de configuration de CUPS.

####

--------
Weblinks
--------

.. target-notes::