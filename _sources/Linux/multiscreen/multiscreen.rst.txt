=============================
Multi-Screen terminal Windows
=============================

.. contents::
    :depth: 3
    :backlinks: top

####


----
tmux
----

:Liens_Web:
    * `tmux - Wiki Officiel`_
    * `How to Use tmux on Linux`_

.. _`How to Use tmux on Linux`: https://www.howtogeek.com/671422/how-to-use-tmux-on-linux-and-why-its-better-than-screen/
.. _`tmux - Wiki Officiel`: https://github.com/tmux/tmux/wiki

Tmux est plus simple et plus ergonomic que Screen. Il permet d'ouvrir plusieur fenêtre dans une
seule fenêtre de terminal. Il permet égallement de sinder l'écran en plusieur sous fenêtre.

Memento de commandes Tmux
-------------------------

  .. image:: ./images/memento.png
        :width: 520 px
        :align: center


####

------
Screen
------

Installation de screen
----------------------
    ::

        sudo apt-get install screen
                
Lancer l'application "screen"
-----------------------------
    ::

        screen
                
Memento des commandes Screen
----------------------------

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

####

--------
Weblinks
--------

.. target-notes::