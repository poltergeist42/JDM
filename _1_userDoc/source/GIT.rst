================
GIT (versioning)
================

Les liens utiles
================

:liens WEB:
            * https://git-scm.com/book/fr/v1/D%C3%A9marrage-rapide-%C3%80-propos-de-la-gestion-de-version
            * https://git-scm.com/book/en/v2
            * https://www.youtube.com/watch?v=rP3T0Ee6pLU&list=PLjwdMgw5TTLXuY5i7RW0QqGdW0NZntqiP
                # Chaine youtube en français sur l'utilisation de GIT
                
            * https://youtu.be/V6Zo68uQPqE
                # Cours complet un peu long mais en français en claire
                
            * https://git-scm.com/doc
                # documentation
                
            * https://www.nano-editor.org/dist/v2.2/NT/
                # nano
                
            * https://alexgirard.com/git-book/
                # 'Livre' en français
                
            * http://www.formation-lpi.com/IMG/pdf/mind-map-git.pdf
                # MindMap (memento)

------------------------------------------------------------------------------------------
                
Configurer GIT
==============

    #.  Les options de base pour la configuration
        ::
        
            git config --global user.name "votre_pseudo"
            git config --global user.email moi@email.com
                # on commence par configurer son nom (user.name)
                # puis son adresse Email (user.email)
                
            git config --global color.diff auto
            git config --global color.status auto
            git config --global color.branch auto
                # Les 3 lignes permettent de mettre le shell en couleur
                
    #. Pour vérifier la configuration
        ::
        
            git config --list
    
    #. Remplacer VI par Nano
        - `Télécharger Nano. <https://sourceforge.net/projects/nano/>`_ et l'installer
          dans "C:\Program Files (x86)"
          
        - Ajouter le chemin de Nano dans le path
        - Ouvrir une invite de commande et tapez
            ::
            
                git config --global core.editor nano.exe
    
------------------------------------------------------------------------------------------

Obtenir de l'aide
=================

    #. les commandes de bases intégrée a git
        ::
        
            git help
            git help <verbe>
            git <verbe> --help
            man git-<verbe>
        
------------------------------------------------------------------------------------------

Démarrer un dépôt Git
=====================

    #. Initialisation d'un dépôt Git dans un répertoire existant
        ::
        
            git init
            
------------------------------------------------------------------------------------------

gitignore
=========

    :Liens_Web:
            * https://fr.atlassian.com/git/tutorials/saving-changes/gitignore
                # Description de la syntaxe à utiliser pour '.gitignore'

------------------------------------------------------------------------------------------

Enregistrer des modifications dans le dépôt
===========================================

    #. Vérifier l'état des fichiers
        ::
        
            git status
        
    #. Ajouter les données 
        ::
        
            git add *
    
    #. faire un commit
        ::
        
            git commit -am "votre commentaire"
    
------------------------------------------------------------------------------------------

Créer, lister et sélectionner une branche
=========================================

    #. Pour lister une branche
        ::
        
            git branch
                # la branch ayant un asterics est la branche courante
        
    #. Pour connaitre la branch avtive
        ::

            git symbolic-ref HEAD --short
                
    #. Pour créer une nouvelle branch
        ::
            
            git branch [nom de la branch]
    
    #. Pour sélectionner et se déplacer sur une branche
        ::
        
            git checkout [nom de la branch]
        
    #. Pour importer des fichiers depuis une autre branch.
        ::
            
            git chekout [branch] [fichier cible]

    #. Pour créer une nouvelle branch et basculer directement dessus
        ::

            git checkout -B [Nom de la nouvelle branch]

    #. Pour lister les fichiers tracker : ::

            git ls-files

    #. Pour lister les fichiers non tracker : ::

            git ls-files --others

            ou en version courte :

            git ls-files -o

------------------------------------------------------------------------------------------

appliquer le contenu d'une branch dans la branch courante (faire un merge)
==========================================================================
    
    #. Se placer sur la branche de destination
        ::
        
            git checkout [branch cible]
                # ex : git checkout master
        
    #. Lancer la commande "merge" en prenant comme argument la branch a appliquer
        ::

            git merge [branch_a_appliquer]
                # ex : git merge dev

Copier seulement un fichier depuis une autre branch dans la branch courante
---------------------------------------------------------------------------

    #. Faire un chekout du ficher dans la branch courante ::

        git checkout [branch_source] [chemin/du/fichier]

        ex:
        git branch
              crash_test
              dev_jojo
            * dev_pierre
              master

        git checkout dev_jojo js/main.js
                    
------------------------------------------------------------------------------------------

supprimer des éléments
======================
 
    #. Supprimer un fichier du repository (de l'index, mais pas du dossier de travail)
       
        ::
        
            git rm --cached [nom_du_fichier]
            
    #. supprimer un dossier du repository (de l'index, mais pas du dossier de travail)
    
        - On commence par l'exclure à laide de '.gitignore' ::
            
            ## gitignore
            ## files
            ...
            ## dir
            path_to_my_folder/
            
        - on le supprime ensuite de la même façon qu'un fichier ::
        
            git rm -r --cached path_to_my_folder/
    
    
    #. supprimer tous le cache
        ::
        
            git rm -r --cached .
                # ne pas oublier le point
            
    #. réparer l'index si un fichier est supprimer du dossier de travail mais pas de l'index
        ::
        
            git reset
        
    #. supprimer une branch ::
        
            git branch -D [nom_de_la_branch]
                # l'option '-D' est l’équivalent de --delete --force

------------------------------------------------------------------------------------------

faire un "instantané" puis le libérer
=====================================

    #. faire un instantané ::
        
        git stash push
            
    #. Obtenir la list des stash ::
        
        git stash list
            
    #. Appliquer et libérer l'instantané puis le supprimer ::
        
        git stash pop [id du stash (commit) ou son nom]
            
    #. Appliquer l'instantané ::
        
        git apply [ID ou nom]
            
------------------------------------------------------------------------------------------

Réparer / annuler / remplacer
=============================

:Liens Web:
            * https://alexgirard.com/git-book/intermediaire/repair-reset-checkout-revert/
                # Explications fr

Réparer une erreur non-committée
--------------------------------

    #. Réparer une erreur non-committée ::
    
        git reset --hard HEAD

annuler / remplacer le dernier commit
-------------------------------------

    #. Annuler le dernier commit ::
        
        git revert HEAD
            
    #. remplacer le dernier commit par le présent ::
    
        git commit --ammend

Réparer un **detached HEAD**
----------------------------

l'état **detached HEAD** se produit lorsque "HEAD" fait référence à un commit et non plus à la branche elle même.

cette information est alors visible en faisant un "git branch"

    .. code:: shell

        git branch

        * (HEAD detached from 2ca07f8)
          crash_test
          dev_jojo
          dev_pierre
          master


Les étapes pour rattacher HEAD à la branche sont :

    #. Créer une branche temporaire à partir de la branch actuelle et se placer dessus.

        .. code:: shell

            git checkout -b temp

    #. mettre la branch "normalle" à jour par rapport à la branch temporaire.

        .. code:: shell

            git branch -f [nom_de_la_branche_normalile] [nom_de_la_branch_temporaire]

            ex:
            git branch -f dev_pierre temp

    #. Ce déplacer sur la branche "normalle" et supprimer la branche temporaire.

        .. code:: shell

            git checkout dev_pierre
            git branch -D temp

    #. Vérifier que l'opération c'est effectuée correctement.

        .. code:: shell

            git branch

              crash_test
              dev_jojo
            * dev_pierre
              master

------------------------------------------------------------------------------------------

Gestion dépôt distant
=====================

Un dépôt distant ne doit pas être un dossier de travail.

    #. créer un dépôt distant
        se placer dans le dossier distant
        ::
        
            git init --bare
            
    #. dépôt local
        Si il s'agit d'un nouveau projet on peut faire un clone
        ::
        
            git clone [//chemin/vers/depot/distant]
            
        Si il s'agit d'un projet existant ayant déjà un dépôt distant, on peut changer le
        chemin du dépôt distant directement en éditant le fichier "config" du dépôt local.

------------------------------------------------------------------------------------------

github
======

:Liens Web:
            http://guillaumevincent.com/2012/12/23/Git-pour-les-nuls-recuperer_une_branche_distante.html

    #. Ajouter le dépôt distant "origin" ::
        
            git remote add origin [url_de_votre_projet_sur_github]

    #. Pousser la branch locale "master" vers la branch distante "origin" ::
        
            git push -u origin master
            
    #. Mettre à jour le dépôt local depuis le dépôt distant ::
        
            git pull [nom de la branche]
                # le nom de la branch est optionnel si il n'y en a qu'une (origin)

    #. Lister les branch distantes
        * Lister les branch distantes toutes seules ::
                
                git remote
                
        * afficher l'url à la suite du nom de la branch ::
            
                git remote -v
                
    #. Modifier l'url du dépôt distant
    
        * Ouvrir le dossier ".git" que se trouve à la base du dépôt local
        * Editer le fichier "config" et modifier la ligne "URL"
        
    #. Pousser toutes branch d'un coup sur le dépôt distant ::
        
            git push --all
            
    #. Supprimer une branche distante ::
        
            git push origin :[nom_de_la_branche_distante]
                # N.B : les ':' doivent être colles au nom de la branch distante
            
    #. Obtenir la list des branch distantes (liste depuis de dépôt local) ::
        
            git branch -r
            
    #. Obtenr la list de toutes les branch ::
    
            git branch -a
            
    #. Pour mettre à jour une branch locale depuis depuis une branch distante ::
    
            git pull -a [depot_distant] [branch_locale]
                # ex : git pull -a origin dev

------------------------------------------------------------------------------------------

Importer une branch distante dans le dépôt local
================================================

    #. Synchroniser le dépôt local et le dépôt distant : ::

        git fetch

    #. Contrôler que la nouvelle branch distante est bien référencée dans le dépôt local : ::

        git branch -a

            * master
              remotes/origin/dev_Jojo   <--
              remotes/origin/master

    #. Créer et Tracker la nouvelle branch : ::

        git --track [nom_de_la_branche] [chemin_distant]

        ex:

        git --track dev_jojo remotes/origin/dev_Jojo

    #. Basculer sur la nouvelle branch : ::

        git checkout [nom_de_la_branch]

        ex:

        git checkout dev_jojo


------------------------------------------------------------------------------------------

Réparer un liens vers une branche distante
==========================================

    :Liens_Web:
            * file:///C:/Program%20Files/Git/mingw64/share/doc/git-doc/git-fetch.html
                # Manuel de la commande fetch

::

    git fetch --prune
