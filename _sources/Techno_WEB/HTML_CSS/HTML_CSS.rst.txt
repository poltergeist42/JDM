========
HTML_CSS
========

.. contents::
   :backlinks: top
   :depth: 3

:Liens_Web:
            * `Index et syntaxe du html`_

            * `pense bête html5 et CSS3`_

              
            * `Glossaire de toutes les balises html5`_
                
            * `De nombreux examples d'utilisation du **CANVAS** et HTML5`_
                
            * `Site traitant de la programmation des site WEB`_


.. _`Index et syntaxe du html`: https://html.com/attributes/img-src/
.. _`petit slide (68 pages) de présentation du CSS`: http://slideplayer.fr/slide/1694038/
.. _`Glossaire de toutes les balises html5`: http://41mag.fr/liste-des-balises-html5/balise-br-html5
.. _`De nombreux examples d'utilisation du **CANVAS** et HTML5`: http://www.phpoc.com/forum/viewforum.php?f=51
.. _`Site traitant de la programmation des site WEB`: http://putaindecode.io/fr/articles/github/pages/site-web-gratuit/

####

.. index::
   single: HTML
   single: WEB; HTML

----
HTML
----

Rappel des balises courantes en HTML
====================================

    * <h1>Titre 1</h1> - pour vos titres les plus importants
    
    * <h2>Titre 2</h2> - pour les sous-titres
    
    * <h3>Titre 3</h3> ... et ainsi de suite jusqu'à <h6>
    
    * <em>texte</em> permet de mettre l'accent sur une partie du texte
    
    * <strong>texte</strong> permet de mettre encore plus l'accent sur une partie de texte
    
    * <br /> permet d'insérer un saut de ligne (vous ne pouvez rien mettre à l'intérieur d'un élément br)
    
    * <a href="https://djangogirls.org">link</a> permet de créer un lien
    
    * <ul><li>premier item</li><li>second item</li></ul> permet de créer des listes, comme celle que nous sommes en train de faire !
    
    * <div></div> permet de créer une section au sein de la page

####

.. index::
   single: CSS
   single: WEB; CSS

---
CSS
---

:Liens_Web:

            * `petit slide (68 pages) de présentation du CSS`_
            * `Index des commandes CSS`_
            
.. _`pense bête html5 et CSS3`: http://www.html5-css3-pense-bete.fr/
.. _`Index des commandes CSS`: http://www.css-faciles.com/proprietes-css-liste-alphabetique.php

Sélecteur, pseudo-class et pseudo-elements
==========================================

:Liens_Web:
        * `Description de l'ensemble des sélecteur (et combinaison)`_

        * `Ensemble des sélecteurs CSS`_

.. _`Description de l'ensemble des sélecteur (et combinaison)`: https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Selectors
.. _`Ensemble des sélecteurs CSS`: https://emw3.com/css/

Positionnement et dimensionnement dans la fenêtre (ou dans la boite)
====================================================================

    .. image:: ./images/dimensionnement.png
        :width: 400 px
        :align: center

    * **margin** : Marge extérieur
    * **padding** : Marge intérieur
    * **height** : Hauteur
    * **width** : Largeur

Chaque dimensions peut être utilisée dans sa forme courte (dans le sens horaire) :

    .. image:: ./images/rotation_propriete.PNG
        :width: 400 px
        :align: center

    ::

        p {
            margin:[top] [right] [bottom] [left]
            }

        ex :
        p {
            margin:3px 2px 3px 2px
            }

Chaque dimensions peut aussi être utilisée dans sa forme longue avec les mot clef 
**top, right, bottom, left** :

    ::

        ex :
        p {
            margin-top:3px;
            margin-right:2px;
            margin-bottom:3px;
            margin-left:2px;
            }

Couleurs
========

    :Liens_Web:
            * https://emw3.com/colour.html
                # Calculatrice FaltColor
                
            * https://htmlcolorcodes.com/
                # site permettant d'identifier le code hexa d'une couleur. Propose aussi des tutos CSS

Le terme à recherche pour trouver les codes hexa des couleurs est : ::

    flat color

####

.. index::
    single: Bootstrap
   single: CSS; Bootstrap
   single: WEB; Bootstrap

---------
Bootstrap
---------

    :Liens_Web:
            * https://getbootstrap.com/docs/4.1/getting-started/download/
                # Utiliser la version "Compiled CSS and JS"

Utiliser Bootstrap Offline
==========================

    :Liens_Web:
            * https://www.quora.com/How-do-I-use-Bootstrap-offline
                # la réponse sur un forum

    #. Télécharger le paquet `Bootstrap <https://getbootstrap.com/docs/4.1/getting-started/download/>`_
       puis copier les dossiers "JS" et "CSS" dans le dossier du projet.

    #. Ajouter les lignes suivantes dans le "HEAD" du html (en fonction des CSS désirés) : ::

        # CSS
        <link href="css/bootstrap.css" rel="stylesheet" />
        <link href="css/bootstrap.min.css" rel="stylesheet" />
        <link href="css/bootstrap-grid.css" rel="stylesheet" />
        <link href="css/bootstrap-grid.min.css" rel="stylesheet" />
        <link href="css/bootstrap-reboot.css" rel="stylesheet" />
        <link href="css/bootstrap-reboot.min.css" rel="stylesheet" />

        # Javascript
        <script src="js/bootstrap.min.js"></script>

####

--------
Weblinks
--------

.. target-notes::