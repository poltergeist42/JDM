================
GIT (versinning)
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
        
    #. Pour créer une nouvelle branch
        ::
            
            git branch [nom de la branch]
    
    #. Pour sélectionner et se déplacer sur une branche
        ::
        
            git checkout [nom de la branch]
        
    #. Pour importer des fichiers depuis une autre branch.
        ::
            
            git chekout [branch] [fichier cible]

------------------------------------------------------------------------------------------

appliquer le contenu d'une branch dans la branch courante (faire un merge)
==========================================================================
    
    #. Se placer sur la branche de destination
        ::
        
            git checkout [branch cible]
                # ex : git checkout master
        
    #. lancer la commande "merge" en prenant comme argument la branch a appliquer
        ::
            git merge [branch_a_appliquer]
                # ex : git merge dev
                    
------------------------------------------------------------------------------------------

supprimer des éléments
======================
 
    #. supprimer un fichier du repository (de l'index, mais pas du dossier de travail)
       
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
        
        git stash [nom]
            
    #. Obtenir la list des stash ::
        
        git stash list
            
    #. Libérer l'instantané, et le supprimer ::
        
        git pop [id du stash (commit) ou son nom]
            
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

    #. annuler le dernier commit ::
        
        git revert HEAD
            
    #. remplacer le dernier commit par le présent ::
    
        git commit --ammend

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
            
    #. Pour récupérer une branch distante dans un dépôt local ::
            
            git checkout -b [nom_de_la_branch_local] [emplacement_de_la_branch_distante]/[branch_distante]
                # ex : git checkout -b dev origin/dev
            
    #. Pour mettre à jour une branch locale depuis depuis une branch distante ::
    
            git pull -a [depot_distant] [branch_locale]
                # ex : git pull -a origin dev
            