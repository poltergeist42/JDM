========================
Vocabulaire et Glossaire
========================

.. index::
   single: Golang Vocab 
   single: Go; Gloang Vocab

.. contents::
    :depth: 3
    :backlinks: top

####

------------------------
Vocabulaire et Glossaire
------------------------

:Liens_Web:
    * `Liste des packages de la bibliothèque standard`_

.. _`Liste des packages de la bibliothèque standard`: https://pkg.go.dev/std

.. glossary::

    Package
       Les packages sont utilisés pour regrouper les fonctionnalités associées. Chaque fichier de
       code doit déclarer le package auquel il est lié. Le package par défaut est "main". Il est
       associé au dossier racine du projet.

       Il est possible de définir ces propre packages. Le nom à déclarer dans tous les fichier de
       code sera alors le même que le dossier du package.

       Un package correspond à une librairie dans d'autre langage. Il est possible d'appeler des
       package externes pour enrichier la bibliothèque standard.

       Un package ce déclare au début du fichier avec le mot clef "package" suivi du nom du package.

        .. code:: go

            package main

####

--------
Weblinks
--------

.. target-notes::