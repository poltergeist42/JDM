========
VIM (VI)
========

:liens Web:
            * http://www.vim.org/download.php
            * https://vimebook.com/fr/download/d54e189e-3a6b-4705-86b0-270cec5d5003/vim-pour-les-humains.pdf
            * https://vim-adventures.com/
            * http://www.dansmongrenier.com/informatique_memento_vi.html 
                # Mémento des commandes et actions VI

####

Présentation
============

Vim a 4 modes principaux :

    +-----------+-------------------+----------------------------------------------------------+
    | Modes     | Touche(s) d'accès | Description                                              |
    +===========+===================+==========================================================+
    | Normales  | * [esc]           | - C'est le mode de base. il permet :                     |
    |           |                   |                                                          |
    |           |                   |   * D'accéder aux autres modes                           |
    |           |                   |   * De naviguer dans le fichier                          |
    +-----------+-------------------+----------------------------------------------------------+
    | Commandes | * [esc] --> [:]   | Permet de lancer les commandes                           |
    +-----------+-------------------+----------------------------------------------------------+
    | Visuel    | * [esc] --> [v]   | Permet d'effectuer des sélections                        |
    +-----------+-------------------+----------------------------------------------------------+
    | Insertion | * [esc] --> [i]   | * [i] insérer du texte a l'emplacement du curseur        |
    |           | * [esc] --> [a]   | * [a] insérer du texte après le curseur                  |
    |           | * [esc] --> [o]   | * [o] insérer du texte sur la ligne du dessous           |
    |           | * [esc] --> [I]   | * [I] insérer du texte en début de ligne                 |
    |           | * [esc] --> [A]   | * [A] insérer du texte en fin de ligne                   |
    |           | * [esc] --> [O]   | * [O] Insérer du texte sur la ligne du dessus            |
    +-----------+-------------------+----------------------------------------------------------+

####

Configuration et extension
==========================

Il y a 2 type de configuration :

    :Configuration permanente:      En renseignant le fichier **'.vimrc'**. Les options
                                    seront appliquée sur tous les documents

    :Configuration isolée:          En saisissant les options de configuration en mode
                                    commande. Les options ne seront appliquées que sur le 
                                    document actif pendant toute la durée d'utilisation du fichier

####

Liste des commandes et fonctions utiles
=======================================

    #. Caractères cachés

        #. Afficher masquer les caractères cachés

            :Liens_Web:
                        * http://vimdoc.sourceforge.net/htmldoc/options.html#'list'
                            # /!\\ : #'list' fait parti de l'url

            ::

                ##Afficher les carctères cachés
                set list

                ## Masquer les carctères cachés
                set list!

        #. Configurer les caractères cachés

            :Liens_Web:
                        * http://vimdoc.sourceforge.net/htmldoc/options.html#'listchars'
                            # /!\\ : #'listchars' fait parti de l'url

            ::

                ex:
                set listchars=space:·,tab:>-


    #. Correcteur orthographique

        :Liens_Web:
                    * https://vim-fr.org/index.php/Correction_orthographique

        Le correcteur orthographique nécessite que les langues désirées soit présentes dans
        le dossier "%programFiles(x86)%\Vim\vim80\spell\"

            * Activer la correction orthographique ::

                :setlocal spell spelllang=fr

            * Désactiver la correction orthographique ::

                :setlocal spell!

            * liste des commandes / actions disponibles pour le correcteur

                +------+----------------------------------------------------------------+
                | z=   | sur un mot souligné affiche une liste de corrections possibles |
                +------+----------------------------------------------------------------+
                | zg   | rajoute un mot dans le dictionnaire                            |
                +------+----------------------------------------------------------------+
                | zug  | pour annuler l'ajout au dictionnaire                           |
                +------+----------------------------------------------------------------+
                | ]s   | pour aller au prochain mot mal orthographié                    |
                +------+----------------------------------------------------------------+
                | \[s  | pour le précédent                                              |
                +------+----------------------------------------------------------------+

