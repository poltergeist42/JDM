
======================
Arborescence du projet
======================

.. contents::
   :depth: 3
   :backlinks: top

####

------------------------
Détail de l'arborescence
------------------------

Pour aider à la compréhension de mon organisation, voici un bref descriptif de l'arborescence de se projet. Cette arborescence est à reproduire si vous récupérez ce dépôt depuis GitHub. ::

    JDM                     # Dossier racine du projet (non versionner)
    |
    +--project              # (branch master) contient l'ensemble du projet en lui même
    |   |
    |   \--_1_userDoc       # Contiens toute la documentation relative au projet
    |      |
    |      \--source        # Dossier réunissant les sources utilisées par Sphinx
    |
    \--webDoc               # Dossier racine de la documentation qui doit être publiée
        |
        \--html             # (branch gh-pages) C'est dans se dossier que Sphinx vat 
                            # générer la documentation à publié sur internet

N.B : Tous les dossiers se terminant par "_v" sont vides. Ils ne remonterons donc pas sur les dépôt 
distants.

####

--------
Weblinks
--------

.. target-notes::