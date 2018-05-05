======
Django
======

:Liens_WEB:
            * https://docs.djangoproject.com/fr/1.10/ref/
                # Référence de Django (fr)
                
            * https://docs.djangoproject.com/fr/1.10/intro/
                # Tutoriel de prise en main / découverte
                
            * https://docs.djangoproject.com/fr/1.10/howto/
                # Guides pratiques
                
            * https://www.youtube.com/watch?v=yDv5FIAeyoY
                # Vidéo tutoriel de 08h00 sur Django 1.11

            * http://www.marinamele.com/2014/03/document-your-django-projects.html
                # Pour utiliser Sphinx avec django

            * https://docs.djangoproject.com/en/dev/internals/contributing/writing-documentation/
                # Documenter un projet Django avec Sphinx (Doc officiel Django)

            * https://www.supinfo.com/articles/single/5779-bien-debuter-avec-django-docker
                # Création d'un Container Django

            * https://docs.docker.com/compose/django/
                # Création d'un container Django (Doc officiel Docker)

------------------------------------------------------------------------------------------

Démarrer un nouveau projet
==========================

    #. Créer l’environnement virtuel
    
        - Créer un dossier avec un nom significatif : ::
        
            ex : env_[nom_du_projet]
            
        - Ce placer dans le répertoire de destination et lancer la création
          de l’environnement virtuel : ::
          
            cd env_[nom_du_projet]
            
            virtualenv --system-site-packages .
                # Le point en fin de ligne représente le répertoire courant
                
    #. Créer un projet Django
    
        - Créer un dossier significatif
        - Lancer l’environnement virtuel avant de créer le projet Django
            + Exécuter le script d'activation : ::
            
                .\Scripts\activate.bat
                
        - Ce placer dans le répertoire de destination et lancer la création
          du projet Django(site principal) : ::
          
            cd [nom_du_projet]
            
            django-admin startproject [nom_du_projet] .
                # Le point en fin de ligne représente le répertoire courant
                # Un dossier du [nom_du_projet] sera créer dans le répertoire courant
                
    #. Configurer le fichier "settings.py"
    
        - Editer le fichier "settings.py" situé dans le dossier "./[nom_du_projet]/"
        - Modifier les lignes : ::
        
            LANGUAGE_CODE = 'en-us'
            TIME_ZONE = 'UTC'
            
          par : ::
          
            LANGUAGE_CODE = 'fr-fr'
            TIME_ZONE = 'Europe/Paris'
            
        - Ajouter après la ligne "STATIC_URL = '/static/'" la ligne : ::
        
            STATIC_ROOT = os.path.join(BASE_DIR, 'static')
            
    #. Créer la base de donnée (pour une DB SQLite)
    
        - Se placer au même niveau que le fichiers "manage.py"
        - Effectuer la première migration : ::
        
            manage.py migrate

                
Démarrer une nouvelle APP
-------------------------

    - Se placer au même niveau que le fichiers "manage.py" et exécuter la commande manage : ::
    
        manage.py startapp [votre_application]
            # Un dossier [votre_application] sera créer dans le répertoire courant
    

------------------------------------------------------------------------------------------

Principes de fonctionnement
===========================

Django travail sur le principe du MVC (Model, Vue, Controler). L'organisation dans Django
se présente sous la forme : Model, Vue, Template.

La correspondance avec le MVC est la suivante :

    #. Model (Django : Model) :
    
        - **models.py** : C'est le script qui permet la création des tables
          dans la base de données. 
          
          Par analogie avec la POO
            + La base de donné est l'objet
            + Les tables (définies comme des class dans "models.py")
              sont des instances de l'objet
            + Les champs (définies comme des attribut de class dans "models.py")
              sont des attributs de l'instances
            
    #. Vue (Django : Template) :
        
        - Tous les fichiers en ".html" dans ./templates
        - Les feuilles de styles (".css") dans ./static
        - **urls.py** : sert de liaison avec views.py. Ce ficher généré les urls à la volée,
          par l'interprétation d'expression régulière (RegEx)
          
    #. Controler (Django : Vue)
    
        - **views.py** : Permet de faire le liens entre le Model et la Vue. Interprètes
          les formulaires HTML et interagit avec la base de données
        

------------------------------------------------------------------------------------------

Rappel des commandes de base
============================

:Liens_WEB:
            * https://docs.djangoproject.com/fr/1.10/intro/tutorial01/


    #. Le serveur de développement
        ::
    
            manage.py runserver
            
        **N.B** : Le port par défaut est le 8000
        
        #. Démarrage du serveur sur un autre port ::
        
            manage.py runserver 8080
            
        #. Démarrer le serveur en écoutant sur une autre IP ::
        
            manage.py runserver 0.0.0.0:8000
            

            
Types de champ les plus courant (models.py)
===========================================

:Liens_Web: * https://docs.djangoproject.com/fr/1.10/ref/models/fields/#field-types
                # Liste complète depuis la doc officiel et en fr

    * models.CharField - Cela nous permet de définir un champ texte avec un nombre limité de caractères.
    * models.TextField - Cela nous permet de définir un champ texte sans limite de caractères. Parfait pour le contenu d'un blog post !
    * models.DateTimeField - Définit que le champ en question est une date ou une heure.
    * models.ForeignKey - C'est un lien vers un autre modèle.

