=========================
JSX (JavaScript eXtended)
=========================

.. index::
   single: JSX
   single: JavaScript; JSX
   single: React; JSX
   single: WEB; JSX

.. contents::
    :depth: 3
    :backlinks: top

####

:Liens_Web:
    * `Les bases du JSX`_
    * `Introduction à JSX`_
    * `JSX dans le détail`_

.. _`Les bases du JSX`: https://www.apprendre-react.fr/tutorial/debutant/jsx/
.. _`Introduction à JSX`: https://fr.reactjs.org/docs/introducing-jsx.html
.. _`JSX dans le détail`: https://fr.reactjs.org/docs/jsx-in-depth.html

------------------
Definission de JSX
------------------

Le JSX est l'encapsulation d'un pseudo HTML dans du Javascript. cela permet donc de simplifier
l'écriture. C'est ce que l'on appel du *"sucre syntaxique"*.

On écris le html directement dans le code JavaScript, ce qui nous permet d'y inclure directement
des composants React.

.. code-block:: JavaScript
   :linenos:
   :force:

    //Expression en JSX
    const element = (
        <h1 className="greeting">
            Je s'appel Groot !
        </h1>
    );

    //Expression en REACT
    const element = React.createlement(
        'h1',
        {className: 'greeting'},
        'Je s'appelle Groot !'
    );

Ces deux expressions sont équivlente.

Il est possible d'ajouter des commentaire dans une expression JSX. Les commentaire s'écrivent
comme pour le JavaScript mais entourés d'accolades.

.. code-block:: JavaScript
   :linenos:
   :force:

    const element = (
        <h1>
            {/* un super commentaire bien pertinent */}
            Je s'appelle Groot !
        </h1>
    );

####

-------------------------------------
Interpréter le JSX dans un navigateur
-------------------------------------

Le JSX n'est pas nativement interpréter par les navigateurs. Pour interpréter le JSX dans le
navigateur, il faut le prévoir dans le HTML en ajoutant une la bibliothèque **"Babel"** au moyen de
la balise *<src="...">*. Il faut également inclure l'attribut *type="text/babel"* dans la balise
script contenant le JSX.

.. code-block:: html
   :linenos:
   :emphasize-lines: 10, 17
   :force:

    <!DOCTYPE html>
    <html>
        <head>
            <meta charset="utf-8">
            <!-- CDN React - Development -->
            <script crossorigin src="https://unpkg.com/react@16/umd/react.development.js"></script>
            <script crossorigin src="https://unpkg.com/react-dom@16/umd/react-dom.development.js"></script>

            <!-- imort de Babel (Dev uniquement) -->
            <script src="https://unpkg.com/babel-standalone@6/babel.min.js"></script>
        </head>
        <body>
            <div id="app"></div>
        </body>

        <!-- Balise 'script' avec l'option 'text/babel -->
        <script type="text/babel">
            const element = (
                <h1>
                    Je s'appel Groot !
                </h1>
            );
            ReactDOM.render(element, document.getElementById("app"));
        </script>
    </html>

.. warning::

    L'inclusion de Babel pour interpréter le JSX ralentie le programme. En effet, cela ajoute une
    étape de traduction supplémentaire au processus. 
    
    L'inclusion de Babel est donc a reserver à la phase de **Developpement**. En phase de
    **production** on utilisera d'autres outils tel que **Webpack** pour créer un package.

####

------------------
Details syntaxique
------------------

    * Le mot clef **'class'** habituellement utilisé dans le html ne peut pas être utilisé en JSX
      car c'est égallement un mot clef utilisé en Javascript. Dans les expressions JSX, ce mot clef
      est remplacé par **"className"**.

    * Les mots clefs composés (séparé par "_") utilisés en CSS sont systématiquement remplacé par
      le formatage en **lowerCamelCase**

    * JSX (et donc React) considère les composants commençant par des lettres minuscules comme des
      balises :term:`DOM`. Par exemple, <div /> représente une balise HTML div, mais <Welcome />
      représente un composant, et exige que l’identifiant Welcome existe dans la portée courante.

    * Toutes les balises auto-fermantes doivent être fermées avec "/" avant le ">"

        .. code-block:: html
           :linenos:
           :emphasize-lines: 1, 4
           :force:

            <!-- Balise auto-fermantes en HTML -->
            <input type="text">

            <!-- Balise auto-fermantes en JSX -->
            <input type="text" />

    * Le JSX n'accepte de retourner qu'un seule élément parent à la fois

        .. code-block:: html
           :linenos:
           :force:

            // Code en erreur
            import React, { Component } from 'react'

            class App extends Component {
                render() {
                    return (
                        {/* Premier composant parent */}
                        <div>
                            <h1>Je s'appelle Groot !<h1/>
                        <div/>

                        {/* Second composant parent (Interdit !) */}
                        <h2>Je s'appelle Pierre<h2/>
                    )
                }

            export default App

     Pour eviter ce problème, on import "Fragment" depuis React et on entoure le JSX d'une balise
     "<Fragment></Fragment>"

        .. code-block:: html
           :linenos:
           :force:

            // Code valide
            import React, { Component, Fragment } from 'react'

            class App extends Component {
                render() {
                    return (
                        <Fragment>
                            {/* Premier composant parent */}
                            <div>
                                <h1>Je s'appelle Groot !<h1/>
                            <div/>

                            {/* Second composant parent (Interdit !) */}
                            <h2>Je s'appelle Pierre<h2/>
                        </Fragment>
                    )
                }

            export default App

####

--------
Weblinks
--------

.. target-notes::