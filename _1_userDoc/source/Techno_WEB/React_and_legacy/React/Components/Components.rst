=========
Composant
=========

.. index::
   single: Composants
   single: React; Composants

.. contents::
    :depth: 3
    :backlinks: top

.. toctree::
   :maxdepth: 2

   Fragment/Fragment
   Navbar/Navbar

####

----------------------
Les types de component
----------------------

Il existe 2 types de composants. Les fonctions (appellées **fonctions composants**) et les classes.

Une **fonction composant** est une fonction Javascript qui n'accepte qu'un seul argument appellé
**props** qui signifie "propriétés". Il peut ne pas y avoir de props. Ce composant doit
obligatoirement retourner quelque chose 

    .. code:: JavaScript
       :number-lines:
       :force:

        // fonction composant
        import React from 'react'

        function Welcome(props){
            return <h1>Bonjour, {props.name} </h1>;
            }
        }

On peut également utiliser une classe ES6 pour définir un composant.

    .. code:: JavaScript
       :number-lines:
       :force:

        // class
        import React from 'react'

        class Welcome extends React.Component{
            render() {
                return <h1>Bonjour, {this.props.name}</h1>;
            }
        }

        // Alternative : import de React.Component à l'aide du destructuring
        import React, { Component } from 'react'

        class Welcome extends Component {
            render() {
                return <h1>Bonjour, {this.props.name}</h1>;
            }
        }


Ces 2 composants (la fonction et la classe) sont équivalents.

Une classe doit systématiquement avor une méthode **"render(){return(<code JSX/>)}"** c'est cette
méthode qui modifie le DOM virtuel.

Une fonction doit, systématiquement avoir un "return".

Choix d'un composant ? Fonction : Classe
========================================

Depuis la version 16.8.0 de React et l'introduction des hooks, l'utilisation des
Fonctions composants est privilégiée par rapport aux Classes. 

La philisophie de React est d'avoir des composants le plus simples possible pour pouvoir les
réutiliser plus facillement. Les fonctions sont donc à privilégier le plus souvent possible. 

Convention de nommage des Composants
====================================

Pour permettre à JSX d'identifier et d'interpréter les composants que nous créons, ils faut que la
première lettre du composant soit en majuscule.

####

--------------------------------------------------
Rendu d’un composant : Comment lier React au DOM ?
--------------------------------------------------

Pour lier une application au DOM, il faut utiliser le package ReactDOM et la fonction render avec
en paramètres, le composant racine de l'application et le noeud du DOM auquel il sera attaché.

    .. code:: JavaScript
       :number-lines:
       :force:

        ReactDOM.render(
            <MonApplication />,
            docment.getElementById('root')
        );

Les éléments peuvent soit représenter un éléments du DOM :

    .. code:: JavaScript
       :number-lines:
       :force:

        const element = <div />;

soit représenter un élément définis par l'utilisateur :

    .. code:: JavaScript
       :number-lines:
       :force:

        const element = <Welcome name="Sara"/>;

Lorsque React rencontre un élément représentant un composant défini par l’utilisateur, il transmet
les attributs JSX à ce composant sous la forme d’un objet unique. Nous appelons cet objet **"props"**.

**Le rendu** se fait en appellant **ReactDOM.render()**.

    .. code:: JavaScript
       :number-lines:
       :force:

        function Welcome(props){
            return <h1>Bonjour, {props.name}</h1>;
        }

        const element = <Welcome name="Sara"/>;
        ReactDOM.render(
            element,
            document.getElementById('root')
        );

Détail du déroulement de l'exemple précedent :

    #. On appelle **ReactDOM.render()** avec l’élément créer par <Welcome name='Sara'/>.

    #. React appelle le composant Welcome avec comme props {name: 'Sara'}.

    #. Notre composant Welcome retourne un élément <h1>Bonjour, Sara</h1> pour résultat.

    #. React DOM met à jour efficacement le DOM pour correspondre à <h1>Bonjour, Sara</h1>.

Parcourrir un tableau et l'afficher sous forme de liste
=======================================================

    .. code:: JavaScript
       :number-lines:
       :force:

        {/* JavaScript Object */}
        var d= {elm1: "Je s'appelle Groot !",
                elm2: "Je s'appelle Pierre !",
                eml3: "Je s'appelle atarte"}

        {/* Creation of an array from keys of the "d" object */}
        var dKeys = Object.keys(d)
        console.log("dKey : ", dKeys)

        {/* Browsing the "dkeys" array with the map function. The map function use a callback function. 
        Each item (dkey) is given as the unique key ID : ("item", "unique key")=>{...} */}
        var ul = React.createElement("ul", null, dKeys.map(
                                    (dKey, dkey)=>{
                                        return (
                                            React.createElement("li", null, d[dKey])
                                            )
                                        }
                                    )
                                )
        console.log(ul)
        {/* the "ul"  function is given to the render */}
        ReactDOM.render(ul, document.getElementById("app"))

####

------------------------------------------------------------
Amélioration sémantique du HTML dans le rendu des composants
------------------------------------------------------------

:Liens_Web:
    * `A little semantic HTML trick for React components`_
    * `Les éléments sémantiques HTML5`_

.. _`A little semantic HTML trick for React components`: https://queen.raae.codes/emails/2022-10-10-semantic-react/
.. _`Les éléments sémantiques HTML5`: https://fr.w3docs.com/apprendre-html/les-elements-semantiques-html5.html

Les éléments sémantiques sont une des innovations significatives en HTML5. Avant leur apparition,
toutes les balises des pages Web étaient créées à l'aide des éléments <div>, auxquels étaient
attribués des identificateurs (id) ou des classes (class). Pour placer des panneaux latéraux, des
en-têtes, des pieds de page, des éléments de navigation et d'autres blocs de construction, des blocs
div avec les valeurs appropriées (par exemple, div = "footer") ont été utilisés.

HTML5 introduit de nouveaux éléments sémantiques pour la structuration, le regroupement du contenu
et le balisage du contenu du texte. Ils décrivent clairement quel contenu ils ont (il y avait
<div id = "footer">, devenu <footer>).

La SEO ainsi que les moteurs de recherches moderne s'appuient en autre sur ces éléments sémantique
pour le reférencement des page WEB.

L'utilisation des composant réutilisable dans React à tendence à nous pousser à ne créer que des div,
nous privant ainsi d'une partie de la souplesse ammenée avec le HTML5.

Il est interessant de prendre un peu de temps pour permettre aux composant de pouvoir définir
dynamiquement c'est balises interne.

    .. code:: Javascript
        :number-lines:
        :force:

        // File: card.js
        import React from "react";

        export function Card(props) {
            // 1️⃣ Destructure element and children from props
            const { element, children } = props;

            // 2️⃣ Capitalise element to make it valid jsx
            let Element = element;

            // 3️⃣ Make "div" the default choice
            if (!element) {
                Element = "div";
            }

        return <Element>{children}</Element>;
        }

L'utilisation se fera alors de la façon suivante :

    .. code:: JavaScript
        :number-lines:
        :force:

        // File: exmaple.js
        import React from "react";
        import { Card } from "./card";

        export function Example() {
        return (
            <article>
            <p>An introduction</p>

            <Card element="aside">
                Something related to the article but a little outside of the normal
                flow.
            </Card>

            <p>More content...</p>

            <Card element="p">A paragraph with different styling...</Card>

            <p>More content...</p>
            </article>
        );
        }

####

-----------------------
Extraire des composants
-----------------------

En règle générale, les nouvelles applications React ont un seul composant **App** à la racine.
C'est l'équivalent d'une fonction *main()*. Pour faciliter la maintenance et la portabilité des
éléments, il est conseiller d'avoir un composant **App** le plus simple possible. Pour cela, on
doit isoler, chaque fois que c'est possible, les éléments en composants plus petits (et monotache).

    .. code:: JavaScript
       :number-lines:
       :force:

        function Comment(props) {
            return (
                <div className="Comment">
                    <div className="UserInfo">
                        <img className="Avatar"
                            src={props.author.avatarUrl}
                            alt={props.author.name}
                        />
                        <div className="UserInfo-name">
                            {props.author.name}
                        </div>
                    </div>
                    <div className="Comment-text">
                        {props.name}
                    </div>
                    <div className="Comment-date">
                        {formatDate(props.date)}
                    </div>
                </div>
            );
        }

Si on définit séparément les composant **Avatar** et **UserInfo**, on pourra alors simplifier le
composant **Comment** :

    .. code:: JavaScript
       :number-lines:
       :force:

        // Composant "Avatar"
        function Avatar(props) {
            return (
                <img className="Avatar"
                src={props.user.avatarUrl}
                alt={props.user.name}
                />
            );
        }

        // Composant "UserInfo"
        function UserInfo(props) {
            return (
                <div className="UserInfo">
                    <Avatar user={props.user} />
                    <div className="UserInfo-name">
                        {props.user.name}
                    </div>
                </div>
            );
        }

        // composant "Comment"
        function Comment(props) {
            return (
                <div className="Comment">
                    <UserInfo user={props.author} />
                    <div className="Comment-text">
                        {props.text}
                    </div>
                    <div className="Comment-date">
                        {formatDate(props.date)}
                    </div>
                </div>
            );
        }

####

--------------------------------
Convertir une fonction en classe
--------------------------------

Il est possible de convertir une fonction en classe en quelques étapes:

    #. Créez une classe, avec le même nom, qui étend React.Component (ou simplement Component si on
       l'a importer en destructuring {component}).

    #. Ajoutez-y une méthode vide appelée render().

    #. Déplacez le corps de la fonction dans la méthode render().

    #. Remplacez props par this.props dans le corps de la méthode render(). la méthode render n'a
       q'un seul élément : 'return' suivie d'un bloc JSX entouré de parenthèses.

    #. Supprimez la déclaration désormais vide de la fonction.

    .. code:: JavaScript
       :number-lines:
       :force:

        //Fonction Clock
        function Clock(props) {
            return (
                <div>
                <h1>Bonjour, monde !</h1>
                <h2>Il est {props.date.toLocaleTimeString()}.</h2>
                </div>
            );
        }

        //Classe Clock après transformation
        class Clock extends React.Component {
            render() {
                return (
                <div>
                    <h1>Bonjour, monde !</h1>
                    <h2>Il est {this.props.date.toLocaleTimeString()}.</h2>
                </div>
                );
            }
        }

####

--------
Weblinks
--------

.. target-notes::