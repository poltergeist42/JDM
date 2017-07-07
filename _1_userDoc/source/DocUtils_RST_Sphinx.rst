===========================================
DocUtils ; reStructuredText (.rst) ; Sphinx
===========================================

DocUtils
========

:Liens WEB:
            * http://docutils.sourceforge.net/
            
------------------------------------------------------------------------------------------

reStructuredText (.rst)
=======================

:Liens WEB:
        * https://fr.wikipedia.org/wiki/ReStructuredText
            # (Definission Wikipedia)

        * https://aful.org/wikis/interop/ReStructuredText
            # Exemple et definission en francais

        * https://mg.pov.lt/restview/
            # api en python permettant de convertir dynamiquement
            les fichiers ".rst" en page Web
            
        * https://github.com/steenhulthin/reStructuredText_NPP            
            # Pour ajouter la syntaxe "reStructuredText" à notePad++
            
        * http://docutils.sourceforge.net/docs/user/rst/quickref.html
            # Un petit guide de reférence

------------------------------------------------------------------------------------------

Sphinx
======

:Liens WEB:
        * http://www.sphinx-doc.org/en/stable/tutorial.html
        
        * https://developer.ridgerun.com/wiki/index.php/How_to_generate_sphinx_documentation_for_python_code_running_in_an_embedded_system
            # un petit cookbook sur la configuration
    
Installer Sphinx
----------------
    ::
    
        pip install sphinx
        
Démarrage et initialisation rapide
----------------------------------
    ::
    
        sphinx-quickstart
        
------------------------------------------------------------------------------------------

Rédiger et publier de la doc avec Sphinx sur GitHub-pages
=========================================================


:Liens WEB :
        * https://daler.github.io/sphinxdoc-test/includeme.html
        
Préparation de l'arborescence
-----------------------------

    #. Création de 2 sous-dossier à la racine du projet ::
    
        fakeLib
            project
            webDoc
            
      **N.B** : 'arboProject' inclue la création de ses 2 dossiers
      
    #. Lier le dépôt local (Git) au dépot distant (GitHub) ::
    
        git remote add origin https://github.com/[votre_nom_sous_github]/[votre_depot_github]
        git push -u origin master
        
    #. Initialiser Sphinx
        - Ce placer dans le dossier **_1_userDoc** et ouvrir une invite de commande
        - Exécuter la commande : :: 
            
            sphinx-quickstart
            
        - Il faut accepter la plupart des choix par défaut sauf pour 4 d'entre eux : ::
       
            Separate source and build directories (y/n) [n]:y
            Project language [en]: fr
            autodoc: automatically insert docstrings from modules (y/n) [n]: y
            githubpages: create .nojekyll file to publish the document on GitHub pages (y/n) [n]: y
        
    #. Configurer **'conf.py'**
    
        - Repérez les 3 lignes : ::
       
            # import os
            # import sys
            # sys.path.insert(0, os.path.abspath('.'))
             
        - Remplacez les par : ::
        
            import os
            import sys
            sys.path.insert(0, os.path.abspath('../../'))
            
        - Puis la ligne : ::
        
            exclude_patterns = []
            
        - A remplacer par : ::
        
            exclude_patterns = ['_build', 'Thumbs.db', '.DS_Store']
            
    #. Configurer **'Makefile'**
    
        - Repérez les 2 lignes : ::
        
            SOURCEDIR = source
            BUILDDIR = build
 
        - Remplacez les par : ::
        
            SOURCEDIR = .
            # Attention, il y a un point après le égal. Cela signifie : "répertoire courant"
            
            BUILDDIR = ../../webDoc
            
    #. Configurer **'Make.bat'**
 
        - Rechercher la ligne : ::
        
            set BUILDDIR=build
 
        - A remplacer par : ::
            
            set BUILDDIR= ../../webDoc
            
    #. Faire un commit et le pousser dans le dépôt distant ::
    
        git add .
        git commit -m "install et conf de Sphinx"
        git push -–all
        
    #. Création de la **branch 'gh-pages'**
    
        - Copier l'url du dépôt distant
        - Cloner le dépôt distant dans 'webDoc\html' et se déplacer dans se dossier ::
        
            git clone [url_copiée_depuis_GitHub] html
            # Attention, html est en minuscule.

            cd html
            
        - Création de la branch local 'gh-pages' ::
        
            git branch gh-pages
        
        - Création d'un lien symbolic entre notre nouvelle branch et une branch homonymes
          dans notre dépoôt distant puis on bascule automatiquement sur cette nouvelle branch ::
          
            git symbolic-ref HEAD refs/heads/gh-pages
            
        - Suppression de l'indexation existante de notre nouvelle branch ::
        
            del .git\index
            
        - on nettoye le contenue de notre nouvelle branch pour ne pas refaire un commit
          sur les éléments de la branch principale ::
          
            git clean --fdx
            
    #. Préparation des éléments à intégrer dans notre documentation
    
        :Rappel:        
                - L'ordre dans lequel nous renseignons les fichiers, correspond à 
                  l'ordre dans lequel ils seront afficher sous GitHub.
                  
                - le fichier "index.rst" ne prend pas en charge les chemin relatif
                
        #. Création du fichier **'includeMe.rst'**
            Créer, dans le même dossier que le fichier 'index.rst', le fichier
            'includeMe.rst'.
        
            - Resigner le fichier de la façon suivante : ::
            
                ======================
                README_[nom_du_projet]
                ======================

                .. include:: ../../README.rst
                
            - Ajouter l'entrée **'includeMe'** dans **'index.rst'**
            
        #. Extraction de la documentation depuis les docString du code
            Créer, dans le même dossier que le fichier 'index.rst', un fichier ayant un
            nom significatif qui permete de se référer au code : ::
            
                ex :
                fakeLib
                
            - Renseigner se nouveau fichier sous la forme : ::
            
                fakeLib
                =======

                .. automodule:: _3_software.fakeLib
                   :members:
               
               # Ne pas oublier les 3 éspaces devant ':members:'
               
           - Ajouter l'entrée **'fakeLib'** dans **'index.rst'**
           
        #. Génération de la doc et MAJ de la branch **master** en local et distant : ::
       
            make html
            # si tous se passe bien, on obtien le message suivant :
            # "Build finished. The HTML pages are in ../../webDoc\html."
            cd ..
            git add .
            git commit -m "blabla"
            git push orgin master
            # on pousse la branch 'master' sur le dépôt distant
            
        #. MAJ de la branch **gh-pages** en local et en distant : ::
        
            cd ..\..
            cd webDoc\html
            git branch
            # on vérifie que l'on est bien sur la branch 'gh-pages'
            git add .
            git commit -m "MAJ de la doc"
            git push origin gh-pages
            # on pousse la branch 'gh-pages' sur le dépôt distant
            
        #. Accéder à la documentation publiée sur GitHub :
            Nous pouvons à présent consulter notre jolie documentation en ligne à 
            l'adresse : https://<utilisateur_Gihub>.github.io/fakeLib/ 
            
            example : ::
            
                https://poltergeist42.github.io/fakeLib/ 
            
