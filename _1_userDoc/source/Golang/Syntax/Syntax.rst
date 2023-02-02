===================
Détails syntaxiques
===================

.. index::
   single: Go Syntaxe
   single: Go; Go Syntaxe

.. contents::
    :depth: 3
    :backlinks: top

####

--------------
Aperçu globale
--------------

:Liens_Web:
    * `Apprendre X en Y minutes`_ : Ensemble de code commentée en français permettant d'avoir un
      apperçu concis de l'ensemble des éléments de syntaxe du language.

.. _`Apprendre X en Y minutes`: https://learnxinyminutes.com/docs/fr-fr/go-fr/

####

---------
Accolades
---------

La première accolade doit être positionnée sur la même que l'élément au quel elles appartiennent.

Exemple pour une fonction :

    .. code:: go
        :number-lines:
        :force:

        // Bonne Syntaxe
        func main () {
            // ...
            }

        // Mauviase Syntaxe
        func main ()
        {
            // ...
            }

####

-------
main.go
-------

Tous les projets doivent avoir un fichier "main.go". C'est le fichier principale du programme. Ce
fichier doit contenir une fonction "main()". C'est cette fonction qui est appellée lors de
l'éxécution du programme.


    .. code:: go

        // code minimum
        package main

        func main() {

        }

####

---------
Fonctions
---------

Une fonction peut être déclarée avec des prototypes plus ou moins complexes en fonction de si la
fonction reçoit des arguments, si elle retourne des arguments et si elle est lié à un struct ou à
un interface.

Forme simple
============

Cette forme ne prend pas d'argument, ne retourne rien et n'est pas liée à un autre élément.

  .. image:: ./images/simpleFunction.svg
        :width: 520 px
        :align: center

####

--------
Weblinks
--------

.. target-notes::