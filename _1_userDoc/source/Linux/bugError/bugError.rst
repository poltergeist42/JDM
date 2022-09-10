==========================================
Bug, Maintenance et traitemant des Erreurs
==========================================

.. contents::
    :depth: 3
    :backlinks: top

####

    Concentration des des information sur les problèmes rencontré et sur les solutions ou
    contournements utilisés.

####

----------------------------------------
Disparition des applications dans le GUI
----------------------------------------

:Liens_Web:
    * `Ubuntu Software not loading properly`_

.. _`Ubuntu Software not loading properly`: https://askubuntu.com/questions/1238069/ubuntu-software-not-loading-properly

Détail du problème
==================

Après un redémarrage, toutes les applications ont disparu. Les accès réseau restent tout de même
fonctionnel.

Solution et correction
======================

Ce problème et lier au gestionnaire d'application qui ne se charge pas correctement. Il faut donc
tuer le process et le relancer. Si cela ne fonctionne pas il peut être nécessaire de le réinstaller.

    * Tuer le process

        .. code:: shell

            # snap-store est le gestionnaire d'application Ubuntu
            # Le process devrait se relancer automatiquement. Si ce n'est pas le cas, faire un Reboot
            killall snap-store


    * Faire un refresh de Gnome-Software

        Si Gnome-Software est déja installer, il est possible de faire un refresh avant de le
        réinstaller.

        .. code:: shell

            gnome-software refresh


    * Installer **Gnome-Software**

        Gnome-software n'est plus installer par défaut à partir de la version 20.04 d'Ubuntu. Dans
        mon cas il a été nécessaire de l'installer. Si il est déjà installer, il faut d'abbord le 
        redémarrer.

        .. code:: shell

            sudo apt update
            sudo apt purge gnome-software
            sudo apt install gnome-software
            # Pour moi cela a suffit à corriger mon problème

####

--------
Weblinks
--------

.. target-notes::