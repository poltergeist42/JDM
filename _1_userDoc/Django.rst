======
Django
======

:Liens Web:
            * https://docs.djangoproject.com/fr/1.10/ref/
                # Référence de Django (fr)
                
            * https://docs.djangoproject.com/fr/1.10/intro/
                # Tutoriel de prise en main / découverte
                
            * https://docs.djangoproject.com/fr/1.10/howto/
                # Guides pratiques


Rappel des commandes de base
============================

:Liens Web:
            * https://docs.djangoproject.com/fr/1.10/intro/tutorial01/

    #. Création d’un projet ::
    
        django-admin startproject mysite
        # Cela va créer un répertoire mysite dans le répertoire courant
        
    #. Le serveur de développement
        ::
    
            python manage.py runserver
            
        **N.B** : Le port par défaut est le 8000
        
        #. Démarrage du serveur sur un autre port ::
        
            python manage.py runserver 8080
            
        #. Démarrer le serveur en écoutant sur une autre IP ::
        
            python manage.py runserver 0.0.0.0:8000
            
    #. Création d'une application
        
        Pour créer votre application, assurez-vous d’être dans le même répertoire que manage.py ::
        
            python manage.py startapp [votre_application]
            
Types de champ les plus courant (models.py)
===========================================

    * models.CharField - Cela nous permet de définir un champ texte avec un nombre limité de caractères.
    * models.TextField - Cela nous permet de définir un champ texte sans limite de caractères. Parfait pour le contenu d'un blog post !
    * models.DateTimeField - Définit que le champ en question est une date ou une heure.
    * models.ForeignKey - C'est un lien vers un autre modèle.

    
    