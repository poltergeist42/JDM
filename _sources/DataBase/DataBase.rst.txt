========
DataBase
========

.. index::
   single: DataBase

.. toctree::
   :titlesonly:
   :maxdepth: 2

   PostGreSQL/PostGreSQL
   Redis/Redis

.. contents::
   :backlinks: top

:Liens_WEB:
    * `Wikipedia : base de données`_
    * `Base de données relationnelle`_
    * `NoSQL`_
    * `SQL vs noSQL`_

.. _`Wikipedia : base de données`: https://fr.wikipedia.org/wiki/Base_de_donn%C3%A9es
.. _`Base de données relationnelle`: https://fr.wikipedia.org/wiki/Base_de_donn%C3%A9es_relationnelle
.. _`NoSQL`: https://fr.wikipedia.org/wiki/NoSQL
.. _`SQL vs noSQL`: http://www.sourceamax.com/sql-vs-nosql-quelles-differences-pour-quels-projets/

Une base de données permet rassembler et de stocker des données sous forme de tables pour les bases
de données relationnels (de type SQL) et sous forme de collection pour les bases de données
destructurées (de type NoSQL).

Dans le model MVC (Model Vue Controler), les bases de données représente le **Model**.

Il existe 2 philosophie dans les bases des données : Les bases de données relationnelles
dites : **SQL** et les bases de données destructurées dites **NoSQL**.

Ces 2 philosophies se différencies par leur approches.

Ce qu’il faut retenir c’est que les bases de données SQL peuvent valider vos données et vos mises à
jour (définition de contraintes), mais elles les rendent du coup très strictes. Les bases de
données NoSQL sont plus flexibles mais ne valident pas les données : il en revient au développeur
d’ajouter des contrôles dans la logique du programme car la base de données elle-même n’empêchera
pas les erreurs.

Pour choisir une technologie plutôt qu'une autre on peut s'appuyer sur les éléments suivant :

Pour les projets dont :

    * La structure de données relatives aux logiques métier peuvent être identifiées à l’avance
    * L’intégrité des données (native dans le SGBD) est essentielle
    * Le caractère transactionnel est fortement présent (eCommerce)

SQL semble plus adapté.

Pour les projets dont :

    * L’organisation de données est indépendante, indéterminée et évolutive
    * L’organisation demande un forte agilité et gérant beaucoup de données structurées,
      semi-structurées, non structurées et polymorphes

    * Les besoins de performance et d’évolutivité (load balancing) sont impératives

noSQL semble être une solution.

.. glossary::

    MERISE
        :Liens_WEB:     `présentation de la méthode MERISE`_

        .. _`présentation de la méthode MERISE`: https://www.commentcamarche.net/contents/655-merise-initiation-a-la-conception-de-systemes-d-information

        MERISE est une méthode de conception, de développement et de réalisation de projets
        informatiques. Le but de cette méthode est d'arriver à concevoir un système d'information.
        La méthode MERISE est basée sur la séparation des données et des traitements à effectuer en
        plusieurs modèles conceptuels et physiques.

        La séparation des données et des traitements assure une longévité au modèle. En effet,
        l'agencement des données n'a pas à être souvent remanié, tandis que les traitements le sont
        plus fréquemment.
        
        Cette méthode est donc parfaitement adaptée pour définir les modèles de base de données
        relationnelles.

####


--------
Weblinks
--------

.. target-notes::