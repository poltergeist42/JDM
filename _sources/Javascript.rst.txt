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

Les commentaires sont les mêmes qu'en C : 

    .. code:: javascript

        // Commentaire simple

        /*
            Commentaires
            sur plusieurs
            lignes
        */

Intéraction avec l'utilisateur
------------------------------

    #. affichage d'un message à l'écran

    .. code:: javascript

        alert()
        //ex:
        var myVar = "un message super important";
        alert(myVar);

    #. Entrée utilisateur

        .. code:: javascript

            prompt()
            //ex:
            var entreeClavier = prompt("tapez du text ici : ");

    #. Confirmation conditionnel

        .. code:: javascript

            confirm()
            //ex:
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

    #. Connaitre le type d'une variables
    
        .. code:: javascript

            typeof
            //ex:
            var myVar = 2;
            alert(typeof myVar);

    #. Conversion de TYPE

        #. String --> Number

            .. code:: javascript

                parseInt()
                //ex:
                var myStr, myNumber;
                myStr = "1234";
                myNumber = parseInt(myStr);

        #. Number --> String

            .. code:: javascript

                //ex:
                var myNumber, myStr;
                myNumber = 1234;
                myStr = myNumber + '';

                //ex: (version simplifiee)
                var myVar = 12;
                myVar += '';
                alert(typeof myVar);

Détails syntaxique
==================

Concatener les strings
----------------------

Il y a 2 méthodes permettant de concaténer les chaines de caractères :

    #. Additionner les string

        .. code:: javascript

            var str1 = "aa"
            var str2 = "zz"
            var str12 = "STR1 : " + str1 + " STR2 : " + str2
            //"STR1 : aa STR2 : zz"

    #.  Modifier les chaines directement

        Pour pouvoir modifier les chaines directement, il remplacer les simples cotes < ' ... ' >
        ou les doubles cotes <" ... "> par des accent graves (altGR + 7) < \` ... \` >

        .. code:: javascript

            var str1 = "aa"
            var str_GR7 = `str1 : ${str1}`

Déclaration des variables
-------------------------

    * Constantes

        Les constantes sont définies avec le préfix "const".

        .. code:: javascript

            const var_constante = "cc";
            var_constante = "nn"
            //TypeError: invalid assignment to const `var_constante`


    * var

        "var" permet de définir une variable locale. Si la valeur de cette variable est modifiée
        en dehors de la portée de sa déclaration, la valeur initale sera modifiée / écrasée. 

            .. code:: javascript

                var nom = "aa";
                console.log("Avant le bloc : " + nom);      //nom == "aa"
                if (true){
                    var nom = "zz";
                    console.log("Dans le bloc : " + nom);   //nom == "zz"
                }
                console.log("Après le bloc : " + nom);      //nom == "zz"

​
    * let

        "let" permet de définir une variable locale. Si la valeur de cette variable est modifiée
        en dehors de la portée de sa déclaration, la valeur initiale ne sera pas modifiée.

            .. code:: javascript

                let nom = "aa";
                console.log("Avant le bloc : " + nom);      //nom == "aa"
                if (true){
                    let nom = "zz";
                    console.log("Dans le bloc : " + nom);   //nom == "zz"
                }
                console.log("Après le bloc : " + nom);      //nom == "aa"


Les fonctions
-------------

    #. Fonctions simples

        .. code:: javascript

            // Déclaration
            function myFunct(myArg1, myArg2){
                // un super code ...
                }

            // appel
            myFunct()

            /* Variante */
            var myFunct(myArg1, myArg2) => {
                //un super code ...
                }
            // Le mot clef "function" est suprimé, alors que la flèche " => " est insérée entre
            // les parenthèses et les accolades

            //si la finction n'a pas d'argument
            var myFunct = () => {
                //un super code ...
                }

    #. Fonctions anonymes

        .. code:: javascript

            // déclaration
            function (myArg){
                // un super code ...
                }

    #. Exécution immédiate d'une fonction, sans appel préalable

        .. code:: javascript

            (function (myArg){
                // super code ...
                })();

            /* Cette syntaxe permet d'executer du code isolé
            sans appel préallable d'une 
            fonction. La fonction anonyme est exécutée automatiquement (et immédiatement)
            */


Opérateur < ... > (spread)
--------------------------

L'opérateur spread ( ... ) permet d'éclater les propriété d'un objet. Ces propriété sont alors
intégrable par d'autres objet.

exemple : Création dans "personne2", d'une copie de "personne"

    .. code:: javascript

        var personne = {
            nom : "aa",
            prenom : "zz"};

        var ville = "ee";

    #. Sans l'opérateur spread

        .. code:: javascript

            var personne2 = {
                personne,
                ville};

        ::

            personne2;
            {…}
                personne: Object { nom: "aa", prenom: "zz"}
                ville: "ee"

    #. Avec l'opérateur spread

        .. code:: javascript

            var personne2 = {
                ...personne,
                ville};

        ::

            personne2;
            {…}
                nom: "aa"
                prenom: "zz"
                ville: "ee"

Dans le premier cas, on constate que l'objet "personne" est maintenant une propriété de "personne2".
Dans le second cas, seules les propriété de "personne" ont été ajoutée à "personne2".