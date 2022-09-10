===================
Hardware Management
===================

.. contents::
    :depth: 3
    :backlinks: top

####

----------------
Gestion Matériel
----------------

Info / Gestion CPU
==================

:Liens_Web:
            * https://www.tecmint.com/check-linux-cpu-information/
                # 9 Commandes pour la gestion du CPU

Connaître la liste des matériel usb
===================================
    ::

        lsusb

####

Connaître l’espace disque utilise et celui disponible
=====================================================
    ::

        df -h
                    
####

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

Connaître la liste des ports série
----------------------------------
    ::
    
        ls /dev/tty*
            # La commande retourne généralement plus de 50 tty.
              Cependant, les tty associés au port USB disposent d'une nomenclature différente.
              Ils contiennent habituellement USB ou ACM (Abstract Control Model)
                        
Interroger le journal sur les ports série
-----------------------------------------
    ::

        dmesg | grep tty
            # Information plus complète qu'avec l'instruction précédente

####

--------
Weblinks
--------

.. target-notes::