==============================
Props (Short for "Properties")
==============================

.. index::
   single: Props
   single: React; Props

.. contents::
    :depth: 3
    :backlinks: top

####

:Liens_Web:
    * `What is 'props' and how to use it in React ?`_

.. _`What is 'props' and how to use it in React ?`: https://itnext.io/what-is-props-and-how-to-use-it-in-react-da307f500da0

.. glossary::

    Props
        'Props' est un mot clef spécial en React qui représente les **propriétées**. Il est **utilisé pour**
        **transmettre des données (propriétés) d'un composant à un autre.**

        Les propriétés ne sont transmisent que dans un sens : du composant parent vers le composant
        enfant. On parle de **'uni-directionnal flow'**. Les data transmisent par les props sont en
        lectures seules. Cela signifie que **les data ne doivent pas être changées par le composant**
        **enfant**. Si une données doit changer d'état ou de valeur, il faut passer une fonction 
        "callback" en tant que props. Ce callback sera lui capable de faire évoluer les **states**.

Utilisation des Props
=====================

Il faut se rappeler que les props sont des arguments passés aux composants. Ces arguements sont
fournis par le composant parent et passés aux composants enfants.

On peut résumer l'utilisation des props en 3 étapes:

    #. On définie un attribut et sa valeur (Data) sous la forme d'un Objet 
       JavaScript (Dictionnaire) : {Attribut: Value}.

    #. On passe cet attribue à un composant enfant en utilisant 'props'.

    #. On effectue le rendu de la data du props.

Les props sont en lecture seule 
================================

Une fonction est dite "pure" si elle ne tente pas de modifier ses entrées et retourne toujours le
même résultat avec les même entrées.

.. code:: JavaScript
   :number-lines:
   :force:

    // Une fonction pure (qui ne modifie pas ces propres entrées)
    function sum(a, b) {
        return a + b;
    }

    // Une fonction impure (qui modifie ces propres entrées)
    function withdraw(account, amout) {
        account.total -= amount;
    }

####

--------
Weblinks
--------

.. target-notes::