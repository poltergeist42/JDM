======
Docker
======

Installation
============

:Liens_Web:
            * https://docs.docker.com/v17.09/engine/installation/linux/docker-ce/ubuntu/#set-up-the-repository
                # Install Docker pour ubuntu

            * https://xataz.developpez.com/tutoriels/utilisation-docker/#LI
                # Tuto FR (mieux que le livre 'Docker' des éditions ENI

            * https://docs.docker.com/
                # Documentation officielle

            * https://docs.docker.com/get-started/
                # La page de démarrage / prise en main dans la doc officielle

            * https://www.wanadev.fr/23-tuto-docker-comprendre-docker-partie1/
                # Tuto (introduction) en 3 partie (FR)

            * https://docs.docker.com/engine/reference/commandline/cli/
                # référence CLI


                
Installation manuelle
---------------------
    
    #. MAJ et installation des paquets nécessaires ::
    
        $ sudo apt-get update
        
        $ sudo apt-get install \
            apt-transport-https \
            ca-certificates \
            curl \
            software-properties-common
            
    #. Récupérer la clef GPG de docker ::
    
        $ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
        
    #. Vérifier que l'empreinte de la clef est la bonne ::
    
        $ sudo apt-key fingerprint 0EBFCD88

        --> pub   4096R/0EBFCD88 2017-02-22
        -->       Key fingerprint = 9DC8 5822 9FC7 DD38 854A  E2D8 8D81 803C 0EBF CD88
        --> uid                  Docker Release (CE deb) <docker@docker.com>
        --> sub   4096R/F273FCD8 2017-02-22
        
    #. Installer docker ::
    
        $ sudo apt-get update
        $ sudo apt-get install docker-ce
        
    #. Tester si docker fonctionne ::
    
        $ sudo docker run hello-world

Version facile / Automatique
----------------------------

    #. Télécharger le script d'installation automatique ::
    
        wget -O dockerinstall.sh https://get.docker.com
        
    #. Exécuter le script ::
    
        sudo sh ./dockerinstall.sh
        
    #. Intégrer l'utilisateur au groupe docker ::
    
        sudo usermod -aG docker pierre

Installation sous Windows
-------------------------

:Liens_Web:
            * https://download.docker.com/win/stable/DockerToolbox.exe
                # Ce soft installe virtualBox et une mini VM (boot2docker)

####

Obtenir de l'aide sur une commande
==================================
    ::

        docker [nom_de_la_commanded] --help
        
        ex :
        
        docker rm --help
        
        > Usage:  docker rmi [OPTIONS] IMAGE [IMAGE...]
        >
        > Remove one or more images
        >
        > Options:
        >  -f, --force      Force removal of the image
        >      --no-prune   Do not delete untagged parents

####

Diférence entre une **Image** et un **Container**
=================================================

    * Une image est l'équivalent d'un iso ou d'une VM servant de modèle.
      L'image est en Lecture seule.
    
    * Un Container est une instance dérivée de l'image. Les modifications apportées au
      Container n'entrainent pas de modification sur l'image.
      
    N.B : il est possible de générer une nouvelle image à partir d'un Containers.

####

Images
======

:Liens_Web:
            * https://hub.docker.com/
                # pour trouver des images et consulter ses informations
                
Trouver une image depuis la console
-----------------------------------
    ::
    
        docker search [options] [image_recherche]
        
        ex1 :
        docker search --stars=100 ubuntu
            # l'option '--stars=100' permet d'apliquer un filtre pour n'afficher les
            # images ayant obtenu un score (attribué par la communauté) de 100 minium
            
        ex2 :
        docker search --stars=100 django
        
Récupérer une Image depuis la console
-------------------------------------
    ::
    
        docker pull [OPTIONS] NAME[:TAG|@DIGEST]
        
        ex :
        docker pull ubuntu:latest
            # le tag 'latest' permet de ne récupérer que le dernier commit de l'image et
            # non pas le dépôt complet
            
Suprimer une Image
------------------
    ::
    
        docker rmi [OPTIONS] IMAGE [IMAGE...]

Obtenir la list des images présents sur le poste
------------------------------------------------
    ::
    
        docker image ls [OPTIONS] [REPOSITORY[:TAG]]
        
        ou
        
        docker images [OPTIONS] [REPOSITORY[:TAG]]
        
Créer une nouvelle image à partir d'un container
------------------------------------------------
    ::
    
        Usage:  docker commit [OPTIONS] CONTAINER [REPOSITORY[:TAG]]
        
        Soit :  docker commit [Options] [Nom_du_container] [depot/Nom_del'image]
        
        ex :
         docker commit -m "image Ubuntu avec MongoDB" myMongoDB poltergeist42/mongodb

Définir un Repository et un TAG sur une image
---------------------------------------------
    ::

        $ docker tag --help

            Usage:  docker tag SOURCE_IMAGE[:TAG] TARGET_IMAGE[:TAG]

            Create a tag TARGET_IMAGE that refers to SOURCE_IMAGE

        Ex:
        docker tag friendlyhello poltergeist42/get-started:part1
        # friendlyhello --> SOURCE_IMAGE
        # TARGET_IMAGE :
        #   poltergeist42   --> UserName
        #   get-started     --> Repository
        #   part1           --> TAG

Les information qui compose le TARGET_IMAGE permettrons de faire un push sur dockerHub

Faire un push sur dockerHub
---------------------------

Pour faire un push sur dockerHub, il faut d'abord s'authentifier :
    ::

        docker login
        
On peut ensuite faire un push en précisant

    * le nom d'utilisateur
    * le dépôt distant
    * le TAG
      ::

        Ex:
        docker push poltergeist42/get-started:part1

Pour terminer, on peut arrêter l'authentification :
    ::

        docker logout

####

Containers
==========

Obtenir la liste des Containers
-------------------------------
    ::

        docker ps -a
        
Supprimer un ou plusieurs Containers
------------------------------------

    #. Supprimer un ou plusieurs Containers
        ::
        
            docker rm [OPTIONS] CONTAINER [CONTAINER...]
            
            ex :
            docker rm infallible_haibt
            
            N.B : Plussieurs Containers peuvent être supprimer d'un seul coup. Il Suffit
            d'indiquer les noms des Containers en le séparant par des virgules.
            
    #. Supprimer tous les Containers d'un seul coup
        ::
        
            docker rm `docker ps -aq`
                # attention, le caractère [`] s'obtient avec 
                # la combinaison de touche [AltGR]-[7]
                
####
        
Lancer/initialiser un Container
===============================

**N.B** : pour connaitre toutes les options disponible avec la commande 'run' il faut lancer l'aide
        ::

            docker run --help

    #. En mode interactif ::
    
        sudo docker run -it [nom_de_l'image]
        
    #. En mode interactif avec accès au bash ::

        sudo docker run -it [nom_de_l'image] bash
        
    #. Sur un port différent ::
    
        sudo docker run -p 88:80 [nom_de_l'image]
        
        # Pour attaquer un serveur Web lancer depuis un container, il faut saisir l'IP de
        # la machine hote suivie du port translater
        
        ex :
        http://192.168.1.32:88
       
    #. En mode détacher (en tache de fond, dans un process non bloquant)
    
        sudo docker run -d [nom_de_l'image]
        
    #. Donner un nom spécifique au container pendant son initialisation ::
    
        docker run --name [nom_du_container] [nom_de_l'image]
        
        ex :
        
        docker run -d -p 88:80  --name galette amapdesquatsaisons/galette
        
    #. Arrêter un container ::
    
        sudo docker stop [nom_du_container]
        
    #. Démarrer un container ::
    
        sudo docker start [nom_du_container]
        
    #. Redémarrer un container ::
    
        sudo docker restart [nom_du_container]
        
####
     
Sortir d'un container (mode iterractif)
=======================================
    ::
    
        CTRL-d (control-d)
     


