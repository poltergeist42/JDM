==============
Node & Express
==============

.. index::
   single: Node
   single: JavaScript; Node
   single: MERN; Node
   single: Node & Express
   single: Backend; Node & Express
   single: Backend; Node
   single: WEB; Node
   single: WEB; Node & Express

.. contents::
    :depth: 3
    :backlinks: top

####

-------
Node.js
-------

:Liens_Web:
    * `Nodejs dowload`_

.. _`Nodejs dowload`: https://nodejs.org/en/download/ 

Node.js (ou Node) est un runtime pour Javascript. Tout comme JRE est le runtime de JAVA. Il permet à
Javascript de s'executer en dehors d'un navigateur par exemple coté serveur.

.. glossary::

    CRUD
        :Liens_WEB:     `Wikipedia : CRUD`_
        
        .. _`Wikipedia : CRUD`: https://fr.wikipedia.org/wiki/CRUD

        CRUD est un acronyme réutnissant l'ensemble des actions réalisables sur une base de données

            * **C** reate : créer

            * **R** ead : lire

            * **U** pdate : mettre à jour
            
            * **D** elete : supprimer

####

--------------------
Package et framework
--------------------

.. index::
   single: NPM
   single: Node; NPM

NPM - Packet manager
====================

:Liens_Web:
    * `Installation et découverte de npm`_

.. _`Installation et découverte de npm`: https://www.pierre-giraud.com/npm-installation-decouverte/


.. glossary::

    NPM
        npm (Node Package Manager) est le gestionnaire de paquets officiel de Node.js. Il permet de
        télécharger et d’installer des paquets (encore appelés modules ou librairies) pour pouvoir
        les utiliser pour un projet ou au contraire de partager des paquets pour que d’autres 
        utilisateurs puissent les utiliser.

####


.. glossary::

    middleware
        Middleware are function that Express executes in the middle after incomming request and
        before the output. Middlewares might make changes to the request and response objet.

        The 'use' function registers a middleware with our Express app.
        With 'app.use(express.json())', the express.json() let's us retrieve data from a request via
        the 'body' attribute. Without this middleware, data retrieval would be much more difficult.

Express.JS
==========

Epress est un framework qui permet de simplifier la tache d'écriture du code d'un serveur WEB
(Backside). Il nous laisse définir les routes et les actions à effectuer lorsqu'une requette HTTP
arrive est qu'elle correspond à l'un des patterns que nous avons défini. les patterns utilisé dans
la comparaison avec les requèttes HTTP correspondent à une expression regulière.

Il est également possible de créer des middleware qui pourron être inserer dans le traitement entre
la requètes HTTP (en entrée) et la réponse (en sortie). Les opérations de logging et
d'authentification sont, par exemple traitées à l'aide de middleware.

Babel
=====

Installer babel en mode dévellopeur :

.. code:: shell
   :number-lines:
   :force:

    npm install --save-dev @babel/core@7 @babel/cli@7
    # le "@7" signifie que l'on force l'installation de la version 7 du package.

Babel est capable de plusieurs nombreuse convertion / transformation. Il y a cependant un package
différent pour chacunes des taches. Le package permettant de convertir le JSX en en Javascript 
est : PRESET-REACT.


####

--------
Weblinks
--------

.. target-notes::