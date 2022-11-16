========
Fragment
========

.. index::
   single: Fragment
   single: React; Fragment

.. contents::
    :depth: 3
    :backlinks: top

####

Il n'est pas possible d'effectuer un rendu de plus d'un composant à la fois. Pour palier à se
problème, il est possible d'utiliser le composant "Fragment". Ce composant est importé depuis
"React".

    .. code:: Javascript
        :number-lines:
        :force:

        import {Fragment} from 'react';

        const Numbers = () => {
            return (
                <Fragment>
                    <Module1/>
                    <Module2/>
                </Fragment>
            )
        }

Il est possible d'utiliser la forme courte "<> ... </>". Il ne sera alors plus nécessaire de faire
l'import depuis 'react'.

    .. code:: Javascript

        const Numbers = () => {
            return (
                <>
                    <Module1/>
                    <Module2/>
                </>
            )
        }

####

--------
Weblinks
--------

.. target-notes::