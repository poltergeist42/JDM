========
VIM (VI)
========

:liens Web:
            * http://www.vim.org/download.php
            
            * https://vimebook.com/fr/download/d54e189e-3a6b-4705-86b0-270cec5d5003/vim-pour-les-humains.pdf
            
            * https://vim-adventures.com/
            
            * http://www.dansmongrenier.com/informatique_memento_vi.html 
                # Mémento des commandes et actions VI
            
            * https://urfist.unistra.fr/uploads/media/command_memento_fr.pdf
                # Autres memento (plus denses)

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

Emplacement ou créer le fichiers '.vimrc' en fonction de l'environement
-----------------------------------------------------------------------

    #. Sous Windows

        * %userprofile%\.vimrc


    #. Sous Linux

        * /home/[nom_d'utilisateur]/.vimrc

    #. Sous Mac

        * /Users/[nom_d'utilisateur]/.vimrc


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

            * Activer automatiquement la correction automatique pour un certain type de documenet

                Dans '.vimrc' : ::

                    au BufRead *.txt setlocal spell spelllang=fr
                
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

    #. Rechercher, mettre en évidence un mot ou un ensemble de mot

        #.Rechercher un mot ou une phrase

            * Se placer en mode normal

            * Saisir le caractère slash ('/') suivie du terme à rechercher ::

                [Mode_Normal]
                /[Recherche]

                ex:
                [Mode_Normal]
                /self

        #. Mettre en surbrillance le terme recherché ::

            :set hlsearch

            # pour l'arréter
            :set nohlsearch

        #. supprimer la subrillance précédente ::

            :nohlsearch

        #. faire une recherche incremental (au fur et à mesure de la frappe) ::

            # la recherche incrémental vas séléctioner la première chaine de charactère correspondante
            :set incsearch

    #. Définir le système (dos, unix ou mac) pour l'enregistrement d'un fichier

        :Liens_Web:
                    * http://www.finiderire.com/?post/2008/10/18/Conversion-rituelle-d-un-fichier-egare

        :: 
        
            set ff=x (avec x = dos, unix ou mac )

            ex:
            set ff=unix
                # conversion au format unix / Linux

            set ff=dos
                # conversion au format dos / windows

    #. Activer la souris

        ::
        
            set mouse=a

    #. Ouvrir fermer des bloc de text (folding / unfolding)

        :Liens_Web:
                    * https://unix.stackexchange.com/questions/141097/how-to-enable-and-use-code-folding-in-vim

                    * http://vimcasts.org/episodes/how-to-fold/

        #. instruction à ajourter dans '.vimrc' ::

                set foldmethod=indent   
                set foldnestmax=10
                set nofoldenable
                set foldlevel=2


        #. Liste des raccourcis en mode normal
                   
            +---------+---------------------------------+
            | command | effect                          |
            +=========+=================================+
            | zi      | switch folding on or off        |
            +---------+---------------------------------+
            | za      | toggle current fold open/closed |
            +---------+---------------------------------+
            | zc      | close current fold              |
            +---------+---------------------------------+
            | zR      | open all folds                  |
            +---------+---------------------------------+
            | zM      | close all folds                 |
            +---------+---------------------------------+
            | zv      | expand folds to reveal cursor   |
            +---------+---------------------------------+

    #. Gestion des balises (mark) dans le texte

        #. Placer une balise ::

            # mode normal
            m<a-z>

            ex:
            mb

        #. accéder à une balise ::

            # mode normal
            '(apostrophe)<lettre_de_la_balise>

            ex:
            'b

        #. Lister toutes les balises ::

            # mode normal
            :marks

        #. Repérer une balise spécifique ::

            # mode normal
            :marks <lettre_de_la_balise>

            ex:
            marks b

    #. Faire de l'auto complétion

        :Liens_Web:
                * https://linuxfr.org/forums/astucesdivers/posts/%C3%A9diteurvim-lautocompl%C3%A9tion-sous-vim

        L'auto complétion se fait en cumulant tous les buffers ouvert (1 fichier ouvert = 1 buffer)

        #. Pour descendre le cycle des propositions ::

            CTRL+n

        #. Pour remonter le cycle des propositions ::

            CTRL+p

        #. Auto complétion sur un PATH ::

            CTRL+X+F

        #. Ajouter des listes de mots

            Il est possible d'utiliser la commande **ctags** pour générer des fichiers contenant 
            des listes de tag. Il faut ensuite les intégrer / activer dans '.virmrc' ::

                set tag=<liste_de_fichiers_tag>

                # Plus d'informations dans l'aide de vim :
                :help ctag
