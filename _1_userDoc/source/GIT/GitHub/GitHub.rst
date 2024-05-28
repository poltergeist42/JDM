======
Github
======

.. index::
   single: Github
   single: Git; Github

.. contents::
    :depth: 3
    :backlinks: top

####

    .. note:: 
        
        **Liens Web**
        

        * `Git-pour-les-nuls-recuperer_une_branche_distante`_
    
.. _`Git-pour-les-nuls-recuperer_une_branche_distante`: http://guillaumevincent.com/2012/12/23/Git-pour-les-nuls-recuperer_une_branche_distante.html


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

####

--------
Weblinks
--------

.. target-notes::