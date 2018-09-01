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
        * http://docutils.sourceforge.net/docs/ref/rst/restructuredtext.html
            # Références  officielles

        * https://fr.wikipedia.org/wiki/ReStructuredText
            # (Définition Wikipedia)

        * https://aful.org/wikis/interop/ReStructuredText
            # Exemple et définition en français

        * https://mg.pov.lt/restview/
            # api en python permettant de convertir dynamiquement
            les fichiers ".rst" en page Web
            
        * https://github.com/steenhulthin/reStructuredText_NPP            
            # Pour ajouter la syntaxe "reStructuredText" à notePad++
            
        * http://docutils.sourceforge.net/docs/user/rst/quickref.html
            # Un petit guide de référence
            
        * http://python.physique.free.fr/aide/Partie1.html
            # détail de syntaxe avancé

        * http://docutils.sourceforge.net/docs/ref/rst/directives.html
            # Explication détailler des directives (ex : images, include, etc ...)

        * http://openalea.gforge.inria.fr/doc/openalea/doc/_build/html/source/sphinx/rest_syntax.html
            # Syntaxe avancée

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

    #. Création de 2 sous dossier à la racine du projet ::
    
            fakeLib
                project
                webDoc
            
        **N.B** : 'arboProject' inclue la création de ses 2 dossiers
      
    #. Lier le dépôt local (Git) au dépôt distant (GitHub) ::
    
        git remote add origin https://github.com/[votre_nom_sous_github]/[votre_depot_github]
        git push -u origin master
        
    #. Initialiser Sphinx
        - Ce placer dans le dossier **_1_userDoc** (pensez à supprimer le suffixe "_v"
          et ouvrir une invite de commande.
          
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
            # Attention, il y a un point après le égal.
            # Cela signifie : "répertoire courant"
            
            BUILDDIR = ../../webDoc
            
    #. Configurer **'Make.bat'**
 
        - Rechercher la ligne : ::
        
            set BUILDDIR=build
 
        - A remplacer par : ::
            
            set BUILDDIR= ..\..\webDoc
            
    #. Faire un commit et le pousser dans le dépôt distant ::
    
        git add .
        git commit -m "install et conf de Sphinx"
        git push -–all
        
    #. Création de la **branch 'gh-pages'**
    
        - Copier l'url du dépôt distant
        - Se placer dans le dossier 'webDoc'
        - Cloner le dépôt distant dans 'html' et se déplacer dans se dossier ::
        
            git clone [url_copiée_depuis_GitHub] html
            # Attention, html est en minuscule.

            cd html
            
        - Création de la branch local 'gh-pages' ::
        
            git branch gh-pages
        
        - Création d'un lien symbolique entre notre nouvelle branch et une branch homonymes
          dans notre dépôt distant puis on bascule automatiquement sur cette nouvelle branch ::
          
            git symbolic-ref HEAD refs/heads/gh-pages
            
        - Suppression de l'indexation existante de notre nouvelle branch ::
        
            del .git\index
            
        - on nettoie le contenue de notre nouvelle branch pour ne pas refaire un commit
          sur les éléments de la branch principale ::
          
            git clean -fdx
            
    #. Préparation des éléments à intégrer dans notre documentation
    
        :Rappel:        
                - L'ordre dans lequel nous renseignons les fichiers, correspond à 
                  l'ordre dans lequel ils seront afficher sous GitHub.
                  
                - le fichier "index.rst" ne prend pas en charge les chemin relatif
                
        #. Création du fichier **'includeMe.rst'**
            Créer, dans le même dossier que le fichier 'index.rst', le fichier
            'includeMe.rst'.
        
            - Renseigner le fichier de la façon suivante : ::
            
                ======================
                README_[nom_du_projet]
                ======================

                .. include:: ../../README.rst
                
            - Ajouter l'entrée **'includeMe'** dans **'index.rst'**
            
        #. Extraction de la documentation depuis les docString du code
            Créer, dans le même dossier que le fichier 'index.rst', un fichier ayant un
            nom significatif qui permette de se référer au code : ::
            
                ex :
                fakeLib
                
            - Renseigner se nouveau fichier sous la forme : ::
            
                fakeLib
                =======

                .. automodule:: _3_software.fakeLib
                   :members:
               
               # Ne pas oublier les 3 espaces devant ':members:'
               
           - Ajouter l'entrée **'fakeLib'** dans **'index.rst'**
           
        #. Génération de la doc et MAJ de la branch **master** en local et distant : ::
       
            make html
            # si tous se passe bien, on obtien le message suivant :
            # "Build finished. The HTML pages are in ..\..\webDoc\html."
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
            l'adresse : https://<utilisateur_Gihub>.github.io/[nom_du_dépot]/ 
            
            Exemple : ::
            
                https://poltergeist42.github.io/fakeLib/
                
        #. Mettre à jour automatiquement la branch **'gh-pages'** et le dépôt distant
            Pour automatiser la MAJ de 'gh-pages' il faut modifier le fichier **'Makefile'**
            et **'make.bat'**.
            
            - Dans **'Makefile'**, se placer à la fin du document et ajouter les lignes
              suivantes à la fin du document : ::
        
                # reconstruction de la branch "gh-pages" et mise a jour du depot distant
                buildandcommithtml: html

                    cd $(BUILDDIR)/html; git add . ; git commit -m "rebuilt docs"; git push origin gh-pages
                    
            - Dans **'make.bat'** repérer les 2 lignes : ::
            
                %SPHINXBUILD% -M %1 %SOURCEDIR% %BUILDDIR% %SPHINXOPTS%
                goto end
                
            - Intercaler les lignes suivantes entre les 2 : ::
            
                rem reconstruction de la branch "gh-pages" et mise a jour du dépôt distant
                cd %BUILDDIR%\html
                git add .
                git commit -m "rebuilt docs"
                git push origin gh-pages

        #. Cloner un dépôt distant utilisant **'gh-pages'**
            
            - Depuis la racine du projet cloner le dépôt distant dans 2 dossiers ayant la
              même arborescence que le projet initial : ::
            
                ex :
                D:\fakeLib>
                > git clone https://github.com/poltergeist42/fakeLib.git .\project
                > git clone https://github.com/poltergeist42/fakeLib.git .\webDoc\html
                
            - Ce déplacer dans le dossier **'html'** et vérifier la branch courante. Il
              ne devrait y avoir que la branch **'master'** ::
              
                cd .\webDoc\html
                git branch
                
            - Recréer la branch locale **'gh-pages'** et l'associer avec le dépôt distant ::
            
                git checkout -b gh-pages remotes/origin/gh-pages
                
            - Une nouvelle vérification des branch locale devrait nous indiquer qu'il y a
              2 branch et que nous sommes sur la branch **'gh-pages'**

------------------------------------------------------------------------------------------

Directives
==========

    #. Insérez du code html ::

        .. raw:: html

           <br/>
           # Attention, il faut sauter une ligne entre 'raw' et le code html

    #. Insérer une image ::

        .. image:: [chemin/vers/une/image]
           :align: center

        ex:
        .. image:: ./Images/monImage.jpg
           :align: center

        # Important : les chemins doivent être renseigné avec des '/' même sous windows


------------------------------------------------------------------------------------------

Utiliser Sphinx pour traité les donnes de Doxygen
=================================================

:Liens_Web:
        * http://breathe.readthedocs.io/en/latest/
            # Breathe permet de transformer le XML générer par Doxygen en un contenu exploitable par Sphinx


------------------------------------------------------------------------------------------

Modification de thèmes dans Sphinx
==================================

:Liens_Web:
            * http://www.sphinx-doc.org/en/master/theming.html
                # Doc officiel de Sphinx concernant le changement de thèmes


Installer le pack de thèmes pour Sphinx
---------------------------------------

    ::

        pip install sphinxjp.themes.dotted
