================
React-Router-DOM
================

.. index::
   single: ReactRouterDOM
   single: React; ReactRouterDOM

.. contents::
    :depth: 3
    :backlinks: top

####

:Liens_Web:
    * `gérer la navigation programmatique`_

    * `faire un redirect avec le composant react-router-dom après une requête POST`_

    * `Quick Start`_ : semble être la doc officiel

.. _`gérer la navigation programmatique`: https://www.journaldunet.fr/web-tech/developpement/1441259-comment-gerer-la-navigation-programmatique-avec-react-router/
.. _`faire un redirect avec le composant react-router-dom après une requête POST`: https://www.journaldunet.fr/web-tech/developpement/1441289-comment-faire-un-redirect-avec-le-composant-react-router-dom-apres-une-requete-post/
.. _`Quick Start`: https://reacttraining.com/react-router/web/guides/quick-start

React-routeur-dom est un paquet qui permet de rediriger vers une nouvelle url et donc de naviguer entre les différentes pages
en gardant l'esrpie "monopage" de React.

Cette librairie est utilisée depuis le composoant racine, génrallement le composant "App.js".

.. warning::
    A chaque changement de composant ce dernier est recharger dans le DOM. Il est donc important de
    **percisté les données** avec le localstorage ou une base de donnés. Dans le cas contraite
    toutes les données seront perdu puisque le composant sera chargé à son état initial.

####

--------
Weblinks
--------

.. target-notes::