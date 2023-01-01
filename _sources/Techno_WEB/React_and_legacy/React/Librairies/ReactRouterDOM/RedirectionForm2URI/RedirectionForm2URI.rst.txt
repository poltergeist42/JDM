====================================================
Redirection vers une Page React depuis un formulaire
====================================================

.. index::
   single: Redirection vers page
   single: React; Redirection vers page

.. contents::
    :depth: 3
    :backlinks: top

####

-----------------------------------
onSubmit : redirection vers une URL
-----------------------------------

La redirection se fait en 2 étapes :

    #. Redirection vers une page et transmission du state lors de la soumiision d'un formulaire.

    #. Traitement du state depuis la nouvelle page.

Ces 2 opérations se font à l'aide de 2 hooks de la librairie "react-router-dom".

    * useNavigate() 

    * useLocation()

useNavigate()
=============

:Liens_Web:
        * `useNavigate`_

.. _`useNavigate`: https://reactrouter.com/en/6.4.4/hooks/use-navigate


useNavigate() permet de naviguer vers une route qui a été définie à la racine de l'application
(générallement app.js).

Ce hook prend 2 argument. Le premier est à la route à utiliser pour la redirection. Le second, qui
est facultatif, est le state que doit récupérer la page de destination.

    .. code:: JavaScript

        // ...
        
        // Syntax d'utilisation de useNavigate()
        // useNavigate("path", {state: {...SomeData})

        // import du hook depuis la librairie
        import { useNavigate } from 'react-router-dom'

        const form2submit = () => {
            
            const navigation = useNavigate()

            const handleSubmit = (event) => {
            event.preventDefault()
            // ...
            navigation("/list", {state: {...someState})
            }

        // ...
        }


useLocation()
==============

:Liens_Web:
    * `useLocation`_

.. _`useLocation`: https://reactrouter.com/en/6.4.4/hooks/use-location

useLocaltion permet de récupérer l'état qui à été passé au composant actuel à l'aide de useNavigate.

    .. code:: JavaScript

        import { useLocation } from 'react-router-dom'

        const List = (props) => {
          const location = useLocation()
          const {state1 , state2 } = location.state

          return (
            <>
                <h1>Un super titre {state1}</h1>
                <p>un super paragraphe {state2}</p>
            </>
          )
        }



####

--------
Weblinks
--------

.. target-notes::