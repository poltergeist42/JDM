======
Docker
======

Installation
============

:Liens_Web:
            * https://docs.docker.com/v17.09/engine/installation/linux/docker-ce/ubuntu/#set-up-the-repository
                # Install Docker pour ubuntu
                
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
        
    #. Executer le script ::
    
        sudo sh ./dockerinstall.sh
        
    #. Intégrer l'utilisateur au groupe docker ::
    
        sudo usermod -aG docker pierre

------------------------------------------------------------------------------------------
                
Obtenir la list des images/containers présents sur le poste
=========================================================== 
    ::
    
        sudo docker image ls
        
------------------------------------------------------------------------------------------
        
Lancer une image/container
==========================

    #. En mode intéractif ::
    
        sudo docker -it [nom_du_container]
        
    #. En mode intéractif avec accès au bash ::

        sudo docker -it [nom_du_container] bash
        
------------------------------------------------------------------------------------------
     
Sortir d'un container (mode iterractif)
=======================================
    ::
    
        CTRL-d (control-d)
     