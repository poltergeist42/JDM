=====
React
=====

.. index::
   single: React
   single: Frontend; React
   single: JavaScript; React
   single: MERN; React
   single: Web; React

.. contents::
    :depth: 3
    :backlinks: top


.. toctree::
   :maxdepth: 2

   Components/Components
   Props/Props
   States/States
   Hooks/Hooks
   ReactRouterDOM/ReactRouterDOM
   BugFix/BugFix

####

---------------
Getting started
---------------

:Liens_Web:
    * `From Scratch - Apprendre React de zéro en 2022`_ : Vidéo FR montrant les bases (Pages,
       Composants, Srops, State, Hooks, Router, Navbar, etc ...)

    * `Package create-react-app`_

.. _`From Scratch - Apprendre React de zéro en 2022`: https://www.youtube.com/watch?v=f0X1Tl8aHtA
.. _`Package create-react-app`: https://github.com/facebook/create-react-app

**Create React App** est un paquet qui permet de créer l'arborescence et d'installer toutes les
dépendances nécéssaires.

Ce paquet doit être installer globallement.

    .. code:: shell
        :number-lines:
        :force:

        npm install -g create-react-app     # le "-g" permet d'effectuer l'installation de façon
                                            # global. Cette étape n'est à effectuer qu'une seule fois.


*Utilisation* :

L'utilisation se fait depuis un terminale. La commande va créer un répertoire à partir du nom
fournit en arguement. Ce nom n'étant pas attache au projet React lui même, il peut être modifié
ultérieurement.

    .. code:: shell
        :number-lines:
        :force:

        npx create-react-app [my-app]       # Attention, les noms des projets doivent être écris en
                                            # minuscule uniquement.
        cd [my-app]
        npm start


*Variante* : 
Sur les version moderne de "npm" et "Create-react-app" il n'est plus nécéssaire de
lancer "Create-react-app" depuis "npx".

    .. code:: shell
        :number-lines:
        :force:

        create-react-app [my-app]       # Attention, les noms des projets doivent être écris en
                                        # minuscule uniquement.
        cd [my-app]
        npm start




Versionning et récupération de projet
=====================================

Lorsqu'un projet react est créer avec create-react-app, un "git" est également initialisé. React
étant en frontend, il peut être préférable de le supprimer pour en créer un plus haut dans
l'arborescence et ainsi englober le frontend et le backend . 

.. code:: shell

    ~/myProject
        |
        \--> .git
        |
        \--> frontend # React
        |
        \--> backend # Node-Express + Mongo

Create-react-app génére également un fichier ".gitignore" qui exclue le dossier "node_modules". Ce
fichier est à conserver. Il est même intéressant de créer un fichier ".dockerignore" qui exclue lui
aussi le dossier "node_modules".

Le dossiers "node_modules" contient toutes les dépendances de React. Ces dépendances sont listées
dans le fichiers "package.json".

Si le projet est récupérer d'un dépot distant comme Github par exemple il faut alors installer les
dépendances du projet.

.. code:: shell
   :number-lines:
   :force:

    cd [my-app]
    npm install     #lecture du fichier "package.json" pour identifier les dépendances à installer

####

--------------------------------
Exemple d'organisation de projet
--------------------------------

    .. code::

        Public
            |
            \
             --> Index.html

        SRC
            |
            --> Composants
            |
            --> CSS
            |
            --> Pages
            |
            --> App.js

    * Les composants sont isolés et appellés depuis les Pages.
      Il existe deux type de composants.
        + Les composants Statyques. le contenu de ces éléments n'est jamais modifié. C'est éléments
          sont souvent partagé entre plusieurs page (exemple : Navbar ou Footer).
        + Les composant dynamiques. Le contenu et le comportement de ces éléments est modifié en
          fonction des props qui lui sont passées.

    * Les Pages exploitent les composants et les CSS. Ces éléments sont également construit sous la
      forme d'un composant. Ces éléments sont statiques. Ils concentre differents composants. Les
      pages permettent de créer des sections permettant de traité des sujets différents (Ex: Accueil,
      formulaire et liste détaillée).

    * Les CSS sont conccentrée à 1 seul emplacement. Toutes les CSS sont importée depuis une feuille
      de style.

    **N.B** : Les feuilles de styles bootstrap sont gérée depuis un emplacement propre à Bootstrap.

    .. code:: CSS

        # Excemple d'import d'une CSS dans "App.css"

        @import './home.css';

Bonnes pratiques
================

Lorsque l'on crée un nouveau projet, il est pratique de créer les pages en premier. Il sera ensuite
plus simple de procéder au routage à l'aide de "React-Router-DOM".

Les pages doivent, dans un premier temps, être le plus simple possible. Elles seront complétée par
la suite avec leur contenu définitif.

    .. code:: JavaScript
        :number-lines:
        :force:

        // Titre du document : Home.js
        import React from 'react'

        const Home = () => {
            return (
                <h1>Accueil</h1>
            )
        }

        export default Home


####

------------------------------------------------
Accès et traitement des données (Props et State)
------------------------------------------------

La bonne pratique pour la gestion des donées est qu'elles ne soient récoltées et manipuler que depuis
le composant racine. Générallement "App.js".

Il revient donc à ce composant racine d'intéroger la base le serveur pour obtenir les informations
de la base de données et de les partagées composant enfants au travers des Props. 

C'est également  à lui de traiter les données remontées par les composant enfant au travers des
fonctions callback passée en tant que Props pour ensuite mettre à jour les états (State) et ensuite
les redistribuer. 

####

--------
Weblinks
--------

.. target-notes::