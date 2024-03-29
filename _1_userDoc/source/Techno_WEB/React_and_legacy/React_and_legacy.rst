==============
React & Legacy
==============

.. index::
   single: Frontend
   single: Web; Frontend

.. contents::
    :backlinks: top

.. toctree::
   :maxdepth: 2

   JSX/JSX
   React/React
   Native/Native

####

------------
Présentation
------------

:Liens_Web:
        * `Site officiel React`_

            * https://reactjs.org/docs/cdn-links.html
                # Doc officiel permettant le téléchargement des liens CDN à inserer dans
                  la page HTML

.. _`Site officiel React`: https://fr.reactjs.org/docs/getting-started.html

React est une bibliothèque Javascript, utilisée pour créer des composants utilisé dans l'IHM. Dans
le modèle MVC, React correspond à la **Vue**.

Pour créer une application avec React, on va créer des composants (des classes ou des fonctions)
qui seront ensuite assemblé pour former l'application finale. Les composants React sont
réutilisables.

**React utilise un DOM virtuel**

Lors de l'utilisation de bibliothèques telles que JQuery nous manipulons directement les éléments
HTML de la page, c'est à dire le DOM. React ne manipule pas le DOM directement, mais une copie
interne de celui-ci (appellé DOM Virtuel), et produit les modifications d'affichage uniquement
lorsque cela s'avère nécessaire et seulement sur les élément ayant été modifié. Cela permet de ne
pas avoir à recharger la page après chaque action puisque seule quelques éléments à la foie sont mis
a jour.

**React Native** (une variante de React) permet de créer des application IPhone ou Android.

React affiche sont propre html au travers du **JSX** (JavaScript Extended). 

On s'interdit donc d'écrire du html dans le ficher ".html" à
l'éxecption du code minimum et des balises <div> qui accueilleront le html de React.

React est composé de 2 bibliothèques JavaScript à inserer dans la page HTML :

    * **React** : Correspond à React lui même qui permet de créer des composant d'affichage
      réutilisable.

    * **ReactDOM** : Extention permettant d'effectuer le rendu, dans une page HTML, les composants
      créer avec React.

Attention, les deux bibliothèques sont fournie en version **"development"** et en version
**"production"**.

Le code minimale d'une page est donc :

.. code:: html
   :number-lines:
   :force:

    <!DOCTYPE html>
    <html>
        <head>
            <meta charset="utf-8">

            <!-- CDN React - Development -->
            <script crossorigin src="https://unpkg.com/react@16/umd/react.development.js"></script>
            <script crossorigin src="https://unpkg.com/react-dom@16/umd/react-dom.development.js"></script>

            <!-- CDN React - Production -->
            <!-- <script crossorigin src="https://unpkg.com/react@16/umd/react.production.min.js"></script> -->
            <!-- <script crossorigin src="https://unpkg.com/react-dom@16/umd/react-dom.production.min.js"></script> -->
        </head>

        <body>
            <div id="app"></div>
        </body>

        <script>
            // code React ICI.
            // ou inclusion d'un module (Ne pas oublier type="module" dans la balise <script>)
        </script>
    </html>

####

--------
Weblinks
--------

.. target-notes::