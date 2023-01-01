====================================
Utilisateurs, Groupes et Permissions
====================================

.. contents::
    :depth: 3
    :backlinks: top

####

------------
Utilisateurs
------------

activer l'utilisateur root
==========================

    .. warning::
        
        Attention il est recomander de ne pas activer le compte root. 

    .. code:: shell
    
        # Cette command réinitialise le mot de passe de l'utilisateur root et l'active si nécessaire.
        sudo passwd root

Faire une élévation valable toute la durée de la session
========================================================

    .. warning::
        
        Attention il est recomander de ne pas activer le compte root. 

    .. code:: shell

        # N.B : Le prompt devrais passer en root@[nom_de_machine]
        sudo -s


Créer un nouvel utilisateur
===========================

    :Liens_Web:
                * `adduser command`_ 
                
.. _`adduser command`: https://doc.ubuntu-fr.org/adduser#adduser

    .. code:: shell

        # sudo adduser <nom_du_nouvel_utilisateur>
        sudo adduser volab

    N.B: Lorsqu'on crée un nouvel utilisateur, un groupe du même nom est également créer.


Ajouter un utilisateur à un groupe
==================================

    .. code:: shell

        # sudo adduser <nom_de_l'utilisateur> <nom_du_groupe>
        sudo adduser root volab

    N.B: Lorsqu'on crée un nouvel utilisateur, un groupe du même nom est également créer.


Changer le mot de passe d'un utilisateur
========================================
    
    .. code:: shell

        # sudo passwd [username]
        sudo passwd root


####

-------
Groupes
-------

:Liens_Web:
            * `How to List Groups in Linux`_

.. _`How to List Groups in Linux`: https://linuxize.com/post/how-to-list-groups-in-linux/

Créer un nouveau groupe
=======================

    .. code:: shell

        # sudo addgroup <nom_du_group>
        sudo addgroup volab


Afficher les groupes d'un utilisateur
=====================================

    .. code:: shell

        # groups <nom_d'utilisateur>
        groups polter
        # >> polter : polter adm cdrom sudo dip plugdev


Afficher les membres d'un groupe
================================

    .. code:: shell

        # getent group <nom_du_group>
        getent group volab


Afficher les membres d'un groupes (commande alternantive)
---------------------------------------------------------

    .. code:: shell

        # grep <nom_du_groupe> /etc/group
        grep volab /etc/group

Afficher la liste de tous les groupes
=====================================

    .. code:: shell

        getent group


Afficher la liste de tous les groupes (commande alternantive)
-------------------------------------------------------------

    .. code:: shell

        cat /etc/group


Ajouter un utilisateur à un groupes
===================================

    .. code:: shell

        # sudo usermod -aG [nom_du_groupe] [nom_de_l'utilisateur]
        usermod -aG docker polter


####

-----------------------
ACL (Propriétaire, RWX)
-----------------------

:Liens_Web:
            * `propriétés et permissions`_ : Explication simple sur la gestion de permissions

.. _`propriétés et permissions`: https://doc.ubuntu-fr.org/permissions


Connaitre tous les droits et autorisation sur des fichiers et des répertoires
=============================================================================
           
    .. code:: shell

        ls -al
            
Changer le propriétaire d'un dossier (ownership)
================================================

    .. code:: shell
    
        # chown root:[nom_d'utilisateur] [nom_du_dossier]/
            
        chown root:volab echanges/
                

Mettre les droits sur un dossier
================================

    .. warning::
        
        Il est déconseillé de mettre les droits 777 car cela donne tous les droits à tous le
        monde. 

    .. image:: ./images/filesPermissions.png
        :width: 520 px
        :align: center


Pour rendre un fichier Exécutable
=================================

    .. code::

        # chmod a+x [nomDuFichier]

####

--------
Weblinks
--------

.. target-notes::