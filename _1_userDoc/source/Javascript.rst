==========
JavaScript
==========

:Liens_Web:
            * https://openclassrooms.com/fr/courses/1916641-dynamisez-vos-sites-web-avec-javascript
              # Cours (fr) pour l'apprentissage du langage

            * https://developer.mozilla.org/fr/docs/Web/JavaScript/Reference
              # Doc + tuto (fr)

            * https://jsfiddle.net/
              #pour tester du code JS
              
####

Liste des commandes de bases
============================

Commentaires
------------

Les commentaires sont les mêmes qu'en C : ::

    // Commentaire simple

    /*
        Commentaires
        sur plusieurs
        lignes
    */

Intéraction avec l'utilisateur
------------------------------

    #. affichage d'un message à l'écran ::

        alert()

        ex:
        var myVar = "un message super important";
        alert(myVar);

    #. Entrée utilisateur ::

        prompt()
        
        ex:
        var entreeClavier = prompt("tapez du text ici : ");

    #. Confirmation conditionnel ::

        confirm()

        ex:
        if (confirm('Voulez-vous exécuter le code JavaScript de cette page ?')) {
            alert('Le code a bien été exécuté !');
            }
        /* un Popup doit s'ouvrir et demander de confirmer ([OK]) ou pas ([Annuler])
           la valeur retournée est alors un booléin (true ou false) */

Type
----

    #. Les 3 types de bases

           * **number** : Ce type contient tous les types numériques ( entier et décimaux)

           * string

           * boolean

    #. Connaitre le type d'une variables ::

        typeof

        ex:
        var myVar = 2;
        alert(typeof myVar);

    #. Conversion de TYPE

        #. String --> Number ::

            parseInt()

            ex:
            var myStr, myNumber;
            myStr = "1234";
            myNumber = parseInt(myStr);

        #. Number --> String ::

            ex:
            var myNumber, myStr;
            myNumber = 1234;
            myStr = myNumber + '';

            ex: (version simplifiee)
            var myVar = 12;
            myVar += '';
            alert(typeof myVar);

Détails syntaxique
==================

Les fonctions
-------------

    #. Fonctions simples ::

        // Déclaration
        function myFunct(myArg1, myArg2){
                    // un super code
                    }

        // appel
        myFunct()

    #. Fonctions anonymes ::

        // déclaration
        function (myArg){
                    // un super code
                    }

    #. Exécution immédiate d'une fonction, sans appel préalable ::

        (function (myArg){
                    // super code ...
                    })();

        /* Cette syntaxe permet d'executer du code isolé
           sans appel préallable d'une 
           fonction. La fonction anonyme est exécutée automatiquement (et immédiatement)
        */