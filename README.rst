================
Journal de manip
================

   :Autheur:            `Poltergeist42 <https://github.com/poltergeist42>`_
   :Projet:             JDM
   :dépôt GitHub:       https://github.com/poltergeist42/JDM
   :documentation:      https://poltergeist42.github.io/JDM/
   :Licence:            CC BY-NC-SA 4.0
   :Liens:              https://creativecommons.org/licenses/by-nc-sa/4.0/ 

------------------------------------------------------------------------------------------

Déscription
===========

Le Journal De Manip (JDM) est un ensemble d'information, d'astuce et d'expérience pour les 
quelles il m'a semblé nécessaire de prendre des notes

Arborescence du projet
======================

Pour aider à la compréhension de mon organisation, voici un bref déscrptif de l'arborescence de se projet. Cette arborescence est à reproduire si vous récupérez ce dépôt depuis GitHub. ::

    FAKELIB                 # Dossier racine du projet (non versionner)
    |
    +--project              # (branch master) contient l'ensemble du projet en lui même
    |   |
    |   \--_1_userDoc       # Contien toute la documentation relative au projet
    |      |
    |      \--source       # Dossier réunissant les sources utilisées par Sphinx
    |
    \--webDoc               # Dossier racine de la documentation qui doit être publiée
        |
        \--html             # (branch gh-pages) C'est dans se dosier que Sphinx vat 
                            # générer la documentation à publié sur internet