======
States
======

.. index::
   single: States
   single: React; States

.. contents::
    :depth: 3
    :backlinks: top

####

:Liens_Web:
    * `React JS — Understanding State`_

.. _`React JS — Understanding State`: https://codeburst.io/react-js-understanding-state-e875911e921c

React applique une règle stricte :

    **"Tout composant React doit agir comme une fonction pure vis-a-vis de ses props"**.

Les fonctions composants ne pouvant manipuler que des props, on les utilisent lorsque notre
composant ne modifie pas sont état. On parle de **Composant Stateless**.

Lorsqu'un composant doit modifier son état, on utilise une classe (ou des Hooks dans le cas d'une 
fonction).

.. code:: JavaScript
   :number-lines:
   :force:

    const famille = {
        membre1: {
            nom: 'Pierre,
            age: 42,
            type: 'humain'
        },
        membre2: {
            nom: 'Tartine'
            age: 8,
            type: 'chat'
        }
    }

    class App extends Component {
        // 'state = { famille }' en version destructuration
        // 'state = { famille : famille }' en version normal
        state = { famille }
        render() {
            const {titre} = this.props
            const { famille } = this.state
            return(
                <div>
                    <h1>{titre}</h1>
                    <Membre nom={famille.membre1.nom} />
                    <Membre nom={famille.membre2.nom} />
                </div>
            )
        }
    }

####

--------
Weblinks
--------

.. target-notes::