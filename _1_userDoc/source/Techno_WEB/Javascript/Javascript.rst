==========
JavaScript
==========

.. index::
   single: JavaScript
   pair: WEB; JavaScript

.. contents::
   :backlinks: top
   :depth: 3

:Liens_Web:
            * `Cours (FR) pour l'apprentissage du langage`_ : Le cours d'openclassrooms

            * `Doc + tuto (FR)`_ : Info sur le MDN de Mozzilla

            * Pour tester du code HTML, CSS et JS : `JSFiddle`_ ou `codepen.io`_

            * `JavaScript Standard Style`_ : une convention de syntaxe à utiliser pour écrire du
              JavaScript

.. _`Cours (FR) pour l'apprentissage du langage`: https://openclassrooms.com/fr/courses/1916641-dynamisez-vos-sites-web-avec-javascript
.. _`Doc + tuto (FR)`: https://developer.mozilla.org/fr/docs/Web/JavaScript/Reference
.. _`JSFiddle`: https://jsfiddle.net/
.. _`codepen.io`: https://codepen.io/
.. _`JavaScript Standard Style`: https://standarjs.com
              
####

------------
Présentation
------------

JavaScript est un language interpréter conçu pour s'éxecuter coté client, c'est à dire directement
coté navigateur.

Tout comme avec le CSS, il est possible de placer le code JavaScript directement dans la page HTML
ou dans un fichier séparé qui sera ensuite appeller depuis le HTML.

Il était anciennement conseiller de faire l'appelle au fichier JS dans le "head" du fichier puisque
c'est dans cette section que son regrouper toutes les meta-données de la page WEB. Cependant le 
chargement d'un fichier HTML étant séquentiel, il est conseiller de placer les scripts JS en bas de
page (juste avant "</html>") pour ne pas ralentir le chargement des autres éléments.


.. code:: html
   :number-lines:
   :force:

    <!-- JS directely loadded in the HTML page -->
    <html>
        <head>
            <!-- MetaDATA -->
        </head>
        <body>
            <!-- some cool stuff -->
        </body>
        <script>
            console.log("Je s'appelle Groot !");
        </script>
    </html>

    <!-- JS loadded from a seprated file -->
    <html>
        <head>
            <!-- MetaDATA -->
        </head>
        <body>
            <!-- some cool stuff -->
        </body>
        <script type="text/javascript" src="myScript.js"></script>
    </html>

Liste des commandes de bases
============================

Commentaires
------------

Les commentaires sont les mêmes qu'en C : 

.. code:: JavaScript
   :number-lines:
   :force:

    // Commentaire simple

    /*
        Commentaires
        sur plusieurs
        lignes
    */

Interaction avec l'utilisateur
------------------------------

    #. affichage d'un message à l'écran

    .. code:: JavaScript
       :number-lines:
       :force:

        alert();
        //ex:
        var myVar = "un message super important";
        alert(myVar);

    #. Entrée utilisateur

    .. code:: JavaScript
       :number-lines:
       :force:

        prompt();
        //ex:
        var entreeClavier = prompt("tapez du texte ici : ");

    #. Confirmation conditionnelle

    .. code:: JavaScript
       :number-lines:
       :force:

        confirm();
        //ex:
        if (confirm('Voulez-vous exécuter le code JavaScript de cette page ?')) {
            alert('Le code a bien été exécuté !');
            }
        /* un Popup doit s'ouvrir et demander de confirmer ([OK]) ou pas ([Annuler])
        la valeur retournée est alors un booléin (true ou false) */

    #. Affichage dans la console

    .. code:: JavaScript
       :number-lines:
       :force:

       console.log("Je s'appelle Groot !");

Type
----

    #. Les 3 types de bases

           * **number** : Ce type contient tous les types numériques ( entier et décimaux)

           * string

           * Boolean

    #. Connaitre le type d’une variable
    
    .. code:: JavaScript
       :number-lines:
       :force:

        typeof
        //ex:
        var myVar = 2;
        alert(typeof myVar);

    #. Conversion de TYPE

        #. String --> Number

        .. code:: JavaScript
           :number-lines:
           :force:

            parseInt()
            //ex:
            var myStr, myNumber;
            myStr = "1234";
            myNumber = parseInt(myStr);

        #. Number --> String

        .. code:: JavaScript
           :number-lines:
           :force:

            //ex:
            var myNumber, myStr;
            myNumber = 1234;
            myStr = myNumber + '';

            //ex: (version simplifiée)
            var myVar = 12;
            myVar += '';
            alert(typeof myVar);

Opérateur
---------

    #. Opérateur d'égalité : "==" et "==="

    .. code:: JavaScript
       :number-lines:
       :force:

        var a = 1;
        var b = 1;
        var c = "1";

        //"=="  --> contenu égale à
        console.log(a == b);    // true
        console.log(a==c);      // true

        //"===" --> contenu et type égale à
        console.log(a === b);   // true
        console.log(a===c);     // false

    #. Opérateur ternaire

    .. code:: JavaScript
       :number-lines:
       :force:

        /* a ? [instruction 1] : [instruction 2]

            si a est vrai 
                [instruction 1]
            sinon
                [instruction 2]
        */
        // ex :
        var a = 1;
        var myVar = a ? console.log("'a' est vrai") : console.log("'a' est faux");     // "'a' est vrai"

        var a = 0;
        var myVar = a ? console.log("'a' est vrai") : console.log("'a' est faux");     // "'a' est faux"


Détails syntaxiques
===================

Concaténer les strings
----------------------

Il y a 2 méthodes permettant de concaténer les chaines de caractères :

    #. Additionner les strings

    .. code:: JavaScript
       :number-lines:
       :force:

        var str1 = "aa"
        var str2 = "zz"
        var str12 = "STR1 : " + str1 + " STR2 : " + str2
        //"STR1 : aa STR2 : zz"

    #.  Modifier les chaines directement

        Pour pouvoir modifier les chaines directement, il remplacer les simples cotes < ' ... ' >
        ou les doubles cotes <" ... "> par des accent graves (altGR + 7) < \` ... \` >

        .. code:: JavaScript
           :number-lines:
           :force:

            var str1 = "aa"
            var str_GR7 = `str1 : ${str1}`

Déclaration des variables
-------------------------

    * Constantes

        Les constantes sont définies avec le préfix "const".

        .. code:: JavaScript
           :number-lines:
           :force:

            const var_constante = "cc";
            var_constante = "nn"
            //TypeError: invalid assignment to const `var_constante`

    * var

        "var" permet de définir une variable locale. Si la valeur de cette variable est modifiée
        en dehors de la portée de sa déclaration, la valeur initale sera modifiée / écrasée. 

        .. code:: JavaScript
           :number-lines:
           :force:

            var nom = "aa";
            console.log("Avant le bloc : " + nom);      //nom == "aa"
            if (true){
                var nom = "zz";
                console.log("Dans le bloc : " + nom);   //nom == "zz"
            }
            console.log("Après le bloc : " + nom);      //nom == "zz"

    * let

        "let" permet de définir une variable locale. Si la valeur de cette variable est modifiée
        en dehors de la portée de sa déclaration, la valeur initiale ne sera pas modifiée.

        .. code:: JavaScript
           :number-lines:
           :force:

            let nom = "aa";
            console.log("Avant le bloc : " + nom);      //nom == "aa"
            if (true){
                let nom = "zz";
                console.log("Dans le bloc : " + nom);   //nom == "zz"
            }
            console.log("Après le bloc : " + nom);      //nom == "aa"


Les objets JSON (Object)
------------------------

Les objets JSON sont l'équivalent des dictionnaires en python. On peux utiliser toute la syntaxe
JSON.

.. code:: JavaScript
   :number-lines:
   :force:

    { id : "id1" }

Extraire les clés (keys) pour les classé dans un tableau
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^


.. code:: JavaScript
   :number-lines:
   :force:

    var myObject = { 
        id1 : "id1",
        id2: "id2" 
        }

    var keyFromObject = Object.keys( myObject )     //keyFromObject === ["id1", "id2"]

Quand utiliser '[]' ou '.' pour accéder à une clef
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

On utilise '[]' dans le cas d'une itération lorsque le nom du membre n'est pas connue. A l'inverse,
on utilise '.' pour un appel direct, lorsque le nom du membre est connu

.. code:: JavaScript
   :number-lines:
   :force:

    d={'a':1, 'b':2, 'c':3}             //d     --> Object { a: 1, b: 2, c: 3 }
    const d_str = Object.keys(d)        //d_str --> Array(3) [ "a", "b", "c" ]

    d_str.forEach(
        item =>{
            console.log(d[item])
        }
    )                                   //1
                                        //2
                                        //3

    d.a                                 //1
    d.b                                 //2
    d.c                                 //3

Les fonctions
-------------

    #. Fonctions simples

    .. code:: JavaScript
       :number-lines:
       :force:

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

        //si la fonction n'a pas d'argument
        var myFunct = () => {
            //un super code ...
            }

    #. Fonctions anonymes

    .. code:: JavaScript
       :number-lines:
       :force:

        // déclaration
        function (myArg){
            // un super code ...
        }

    #. Exécution immédiate d'une fonction, sans appel préalable

    .. code:: JavaScript
       :number-lines:
       :force:

        (function (myArg){
            // super code ...
        })();

        /* Cette syntaxe permet d'exécuter du code isolé
        sans appel préalable d'une 
        fonction. La fonction anonyme est exécutée automatiquement (et immédiatement)
        */

Opérateur < ... > (spread)
--------------------------

L'opérateur spread ( ... ) permet d'éclater les propriétés d'un objet. Ces propriétés sont alors
intégrable par d'autres objet.

exemple : Création dans "personne2", d'une copie de "personne"

    .. code:: JavaScript
       :number-lines:
       :force:

        var personne = {
            nom : "aa",
            prenom : "zz"};

            var ville = "ee";

    #. Sans l'opérateur spread

    .. code:: JavaScript
       :number-lines:
       :force:

        var personne2 = {
            personne,
            ville};


        personne2;
        {…}
            personne: Object { nom: "aa", prenom: "zz"}
            ville: "ee"

    #. Avec l'opérateur spread

    .. code:: JavaScript
       :number-lines:
       :force:

        var personne2 = {
            ...personne,
            ville};

        personne2;
        {…}
            nom: "aa"
            prenom: "zz"
            ville: "ee"

Dans le premier cas, on constate que l'objet "personne" est maintenant une propriété de "personne2".
Dans le second cas, seules les propriétés de "personne" ont été ajoutée à "personne2".

Opérateur de comparaison "short-circuit"
----------------------------------------

Il existe un opérateur de comparaison qui retourne une expression seulement si la condition est
vraie, contrairement à l'opérateur ternaire qui retourne une expression dans tous les cas.

Cet opérateur est sous utilise le "ET" logique : &&

    .. code:: JavaScript
       :number-lines:
       :force:

        let isTrue = true
        let someExpression = "isTrue est vrai"

        isTrue && someExpression        // --> "isTrue est vrai"

        isTrue = false
        isTrue && someExpression        // --> flase

        //cette syntaxe est équivalente à :
        if (isTrue){
            someExpression
            }

Ça fonctionne parce qu’en JavaScript, true && expression est toujours évalué à expression,
et false && expression est toujours évalué à false.

La décomposition (destructuring)
--------------------------------

:Liens_Web:

    * `Affecter par décomposistion (MDN)`_

.. _`Affecter par décomposistion (MDN)`: https://developer.mozilla.org/fr/docs/Web/JavaScript/Reference/Op%C3%A9rateurs/Affecter_par_d%C3%A9composition

**L'affectation par décomposition (destructuring en anglais)** est une expression JavaScript qui
permet d'extraire (unpack en anglais) des données d'un tableau ou d'un objet grâce à une syntaxe
dont la forme ressemble à la structure du tableau ou de l'objet.

Ces expression peuvent être utilisée pour l'affectation de valeur à une varriable, décomposer un
objet JavaScript (un Dictionnaire) ou de décomposer les propriétés d'un objet. C'est égelement la
forme utilisée pour n'importer que certaines classes d'une librairie et ainsi éviter de la chargé
complétement.

.. code:: JavaScript
   :number-lines:
   :force:

    /* Affectation */
    var a, b, rest
    //Affectation simple
    [a, b] = [1, 2]                     //a===1, b===2

    //Afectation avec un 'reste' grace à l'opérateur 'spread'
    [a, b, ...rest] = [1, 2, 3, 4, 5]   //a===1, b===2, rest = [3, 4, 5]

    /* Décomposer un objet */
    //Décomposition simple
    var o = {p: 42, q: true};
    var {p, q} = o;                     //p===42, q===true

    //Décomposition sans affectation
    var a, b;
    ({a, b} = {a:1, b:2});              //Les parenthèses ( ... ) utilisées autour de l'instruction
                                        //sont nécessaires pour que la partie gauche soit bien
                                        //interprétée comme un objet littéral et non comme un bloc.
                                        //Il est également nécessaire d'avoir un point-virgule 
                                        //avant les parenthèses de l'instruction car sinon, ces
                                        //parenthèses peuvent être interprétées comme un appel
                                        //de fonction.

    //affectation avec un nom différent
    var o = {p: 42, q: true};
    var {p: toto, q: truc} = o;         //toto===42, truc===true

    //Décomposer les propriétés d'objets passés en arguments
    var user = {
        id: 42,
        displayName: "jbiche",
        fullName: {
            firstName: "Jean",
            lastName: "Biche"
        } 
    };

    function userId({id}) {
        return id;
    }

    function whois({displayName: displayName, fullName: {firstName: name}}){
        console.log(displayName + " est " + name);
    }

    console.log("userId: " + userId(user)); w// "userId: 42"
        whois(user); // "jbiche est Jean"

                                        //Cela permet d'accéder directement à id, displayName et
                                        //firstName depuis l'objet user

Les classes
-----------

La Création d'une classe se fait avec le mot clef : **class**. La création d'une instance se fait
avec le mot clef : **new**.

.. code:: JavaScript
   :number-lines:
   :force:

    class Personne{
        //...
    }

    personne = new Personne();

La définission d'attribut de classe se fait dans une méthode **"construtor()"**. Cette méthode est
appellée automatiquement à la création d'une instance de la classe. C'est l'équivalent de la
méthode **"__init__()"** en Python. La définition d'attribut ou l'appel d'une méthode depuis une
autre méthode de la classe doit être précéder de **"this"**. c'est l'équivalent de **"self"**
en Python.

.. code:: JavaScript
   :number-lines:
   :force:

    class Personne{
        constructor(nom, prenom){
            this.nom = nom;
            this.prenom = prenom;
        }
    }

Héritage de classe
^^^^^^^^^^^^^^^^^^

L'héritage d'une classe se fait par lajout du terme **"extends" suivie du nom de la calsse mère**
dans la déclaration de classe. Il faut égallement appeller la méthode **"super()"** dans la méthode
**"constructor()"** de la classe fille.

.. code:: JavaScript
   :number-lines:
   :force:

    class Homme extends Personne{
        constructor(nom, prenom){
            super(nom, prenom);     //Equivalent de Personne.constructor(nom, prenom)
            this.sexe = "H";
        }

        log(){
            console.log(`nom : ${this.nom}, prenom : ${this.prenom}`);
        }
    }

    var personne = new Homme("Bond", "James");
    personne.log();

super()
+++++++

:Liens_Web:
    * `super() : MDN web docs`_

.. _`super() : MDN web docs`: https://developer.mozilla.org/fr/docs/Web/JavaScript/Reference/Op%C3%A9rateurs/super

Le mot-clé super est utilisé afin d'appeler ou d'accéder à des fonctions définies sur l'objet
parent.

Lorsqu'il est utilisé dans un constructeur, le mot-clé super est utilisé seul et doit apparaître
avant le mot-clé this. Ce mot-clé peut également être utilisé afin d'appeler des fonctions sur un
objet parent.

Import / Inclusion de module
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Un module représente un fichier qui doit être importer dans un autre fichier. Il est possible, mais
déconseiller, de faire import de ces modules directement dans le fichier HTML. Cette approche
impose de connaitre à l'avance toutes les dépendances et donc nous oblige à inserer tous les
fichiers dans l'ordre. De plus le fichier HTML est alors surchargé ce qui peux le rendre difficile
à maintenir.

.. code:: html
   :number-lines:
   :force:


    <!DOCTYPE html>
    <html>
        <head>
            <meta charset="utf-8">
        </head>

        <body>
        </body>

        <!-- Inclusion des modules externes -->
        <script src="./personne.js"></script>
        <script src="./homme.js"></script>
        <script>
            var personne = new Homme("Bond", "James");
            personne.log();
        </script></script>>
    </html>

Pour éviter ces problèmes, il faut créer des modules en choisissant les éléments à exposer à l'Aide
du termes **"export"**. Le ficher deveint un module à ce moment là. Il est possible d'exporter
plusieurs éléments en les séparant par des virgules.

.. code:: JavaScript
   :number-lines:
   :force:

    //module "personne.js"
    class Personne{
        constructor(nom, prenom){
            this.nom = nom;
            this.prenom = prenom;
        }
        log(){
            console.log(`nom : ${this.nom}, prenom : ${this.prenom}`);
        }
    }

    export {Personne};

L'utilisation de ces modules se fait à l'aide de la commande **"import [...] from [...]"**.

.. code:: JavaScript
   :number-lines:
   :force:

    // Module "Homme"
    import {Personne} from "./personne.js";

    class Homme extends Personne{
        constructor(nom, prenom){
            super(nom, prenom);     //Equivalent de Personne.constructor(nom, prenom)
            this.sexe = "H";
        }

        log(){
            super.log();
            console.log("C'est un homme !");
        }
    }

    export {Homme};

IL est conseiller d'importer tous les modules dans un seul fichier.

.. code:: JavaScript
   :number-lines:
   :force:

    import {Personne} from "./personne";
    import {Homme} from "./homme";

    var personne = new Personne("Gabin", "Jean");
    personne.log();

    var personne2 = new Homme("Bond", "James");
    personne2.log();

On peux ensuite importer Ce fichier dans une balise **"script"** de type **"module"** dans le
fichier html.

.. code:: html
   :number-lines:
   :force:

    <!DOCTYPE html>
    <html>
        <head>
            <meta charset="utf-8">
        </head>

        <body>
        </body>

        <!-- Inclusion des modules externes -->
        <script type="module" src="./index.js"></Script>
    </html>

Importer du CSS
---------------

Si on importe les fichier JavaScript sans préciser l'extention, c'est l'inverse lorsque l'on doit
inserer du CSS.

.. code:: JavaScript
   :number-lines:
   :force:

    import {Personne} from "./personne"
    import styles from "./css/monSuperCSS.css"

.. glossary::

   DOM
    Le DOM (Document Object Model) est une API qui réprésente et interagit avec tous types de
    documents HTML ou XML. Le DOM est un modèle de document chargé dans le navigateur. La
    représentation du document est un arbre nodal. Chaque nœud représente une partie du document
    (par exemple, un élément, une chaîne de caractères ou un commentaire).

    Le DOM est l'une des API les plus utilisées sur le Web parce-qu'il autorise du code exécuté
    dans un navigateur à accéder et interagir avec chaque nœud dans le document. Les nœuds peuvent
    être créés, déplacés et modifiés. Des auditeurs d'évènements (event listeners) peuvent être
    ajoutés à des nœuds et déclenchés par un évènement donné.

    À l'origine, DOM n'était pas standardisé. Il ne l'a été que lorsque les navigateurs ont
    commencé à implémenter JavaScript. Le DOM qui découle de cette période initiale est parfois
    appelé DOM 0. À l'heure actuelle, le W3C édicte les spécifications de la norme DOM.

    Source : `DOM sur MDN web docs`_
    Voir aussi : `DOM sur Wikipedia`_

.. _`DOM sur MDN web docs`: https://developer.mozilla.org/fr/docs/Glossaire/DOM
.. _`DOM sur Wikipedia`: https://fr.wikipedia.org/wiki/Document_Object_Model

.. glossary::

   AJAX
    Le JavaScript et XML asynchrone (AJAX) est une pratique de programmation qui consiste à
    construire des pages web plus complexes et plus dynamiques en utilisant une technologie connue
    sous le nom de XMLHttpRequest.

    AJAX vous permet de mettre à jour simplement des parties du DOM d'une page web HTML au lieu de
    devoir recharger la page entière. AJAX vous permet également de travailler de manière
    asynchrone, c'est-à-dire que votre code continue à s'exécuter pendant que la partie de votre
    page web essaie de se recharger (par opposition à la méthode synchrone qui bloque l'exécution
    de votre code jusqu'à ce que la partie de votre page web ait fini de se recharger).

    Avec les sites web interactifs et les standards modernes du web, AJAX est progressivement
    remplacé par des fonctions dans les cadres JavaScript et l'API standard officielle Fetch API.

    Source : `AJAX sur MDN web docs`_

    Voir aussi : 

        * `AJAX sur WIKIPEDIA`_
        * `AJAX, guide pour les développeurs du WEB`_

.. _`AJAX sur MDN web docs`: https://fr.wikipedia.org/wiki/Ajax_(informatique)
.. _`AJAX sur WIKIPEDIA`: https://fr.wikipedia.org/wiki/Ajax_(informatique)
.. _`AJAX, guide pour les développeurs du WEB`: https://developer.mozilla.org/fr/docs/Web/Guide/AJAX

####

--------
Weblinks
--------

.. target-notes::