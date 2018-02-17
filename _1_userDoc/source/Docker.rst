======
Docker
======

:Liens_Web:
            * https://docs.docker.com/v17.09/engine/installation/linux/docker-ce/ubuntu/#set-up-the-repository
                # Install Docker pour ubuntu
                
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
     