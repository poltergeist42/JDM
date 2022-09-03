========================
Raspberry Pi as a router
========================

.. contents::
    :backlinks: top
    :depth: 3

####

Objectif
========

L'objectif est de transformer le Raspberry Pi en router. La carte wifi doit se connecter à un point
d'accès mobile tel q'un téléphone ou un router 4G / 5G. Le trafic est ensuite routé vers la carte
Ethernet. 

Un serveur DHCP est également configuré sur la carte Ethernet.

Schéma 
------

    .. image:: ./images/schema.svg
        :width: 520 px
        :align: center

####

-------------------------------------
Configuration des points d'accès wifi
-------------------------------------

:Liens_Web:
    * `Setting up Raspberry Pi Wi-Fi`_

.. _`Setting up Raspberry Pi Wi-Fi`:https://pimylifeup.com/setting-up-raspberry-pi-wifi/

.. warning::
    Attention, il est important de respecter la casse du SSID (majuscule / minuscule). De plus,
    un SSID ne peux pas contenir d'espace.

L'ajout de SSID peut s'effectuer de 2 façons diférentes :

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


[WIP]

####

------------
Serveur DHCP
------------

[WIP]

####

--------------------
Serveur d'impression
--------------------

:Liens_Web:
    * `Comment Installer une Imprimante sur Raspberry Pi (CUPS)`_

.. _`Comment Installer une Imprimante sur Raspberry Pi (CUPS)`:https://raspberrytips.fr/installer-imprimante-raspberry-pi/

Ici aucune dificulté. Il suffit de suivre un tuto installation et de configuration de CUPS.

####

--------
Weblinks
--------

.. target-notes::