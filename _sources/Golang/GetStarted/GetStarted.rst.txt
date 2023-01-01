===========
Get Started
===========

.. contents::
    :depth: 3
    :backlinks: top

####

------------------
Installation de Go
------------------

:Liens_Web:
    * `Downloads`_
    * `Download and install`_

.. _`Downloads`: https://go.dev/dl/
.. _`Download and install`: https://go.dev/doc/install

Après le téléchargement du binnaire, il faut supprimer les version existantes avant de décompresser
l'archive dans le dossier "/usr/local"

    .. code:: shell
        :number-lines:
        :force:

         rm -rf /usr/local/go && tar -C /usr/local -xzf go1.19.4.linux-amd64.tar.gz

Une fois l'archive décompressé, il faut l'ajouter au PATH local en ajoutant une entré dans
"$HOME/.profile". Attention si le shell et différent de bash, l'entrée sera à ajouter dans fichier
différent. Ex: pour ZSH "$HOME/.zshrc".


    .. code:: shell
        :number-lines:
        :force:

        export PATH=$PATH:/usr/local/go/bin

--------------------------------------
Création d'un nouveau module (Package)
--------------------------------------

Un module peut aussi bien être un programme complet qu'une librairie qui sera utilisée par d'autre
module.

N.B : Pour u programme, il faut également créer le fichier "main.go"

    .. code:: shell
        :number-lines:
        :force:

        # Se placer dans le dossier de déstination
        cd monSupperModule

        # Initialiser le module
        # go mod init [nom_du_package]
        go mod init monSupperModule

Structure minimum d'une application
===================================

    .. code:: go
        :number-lines:
        :force:

        // Tous les fichiers ".go" doivent appartenir à un package
        package main

        // Import des package ou bibliothèque extérieur
        import "fmt" 

        // Déclaration de la fonction principale.
        func main() {
            fmt.Println("Todo: add some features")
        }


####

--------
Weblinks
--------

.. target-notes::