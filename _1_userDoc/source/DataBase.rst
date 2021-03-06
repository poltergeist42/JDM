========
DataBase
========

.. index::
   single: DataBase

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

    CRUD
        :Liens_WEB:     `Wikipedia : CRUD`_
        
        .. _`Wikipedia : CRUD`: https://fr.wikipedia.org/wiki/CRUD

        CRUD est un acronyme réutnissant l'ensemble des actions réalisables sur une base de données

            * **C** reate : créer

            * **R** ead : lire

            * **U** pdate : mettre à jour
            
            * **D** elete : supprimer

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

.. index::
   single: PostGreSQL
   single: DataBase; PostGreSQL

----------
PostGreSQL 
----------

:Liens_WEB:
    * `Page de documentation officiel`_

    * `site de la communauté francophone`_

    * `Doc (FR)`_

.. _`Page de documentation officiel`: https://www.postgresql.org/docs/
.. _`site de la communauté francophone`: https://www.postgresql.fr/
.. _`Doc (FR)`: https://docs.postgresql.fr/10/

Installation
============

Sous Windows
------------

:Liens_WEB:     `PostGreSQL téléchargement`_ (toutes les versions et tous les environnements)

.. _`PostGreSQL téléchargement`: https://www.postgresql.org/download/

Télécharger l'install automatique et ce laisser guider. Lorsque l'installation est terminée, il faut
ajouter les 2 chemins suivants au 'PATH' dans les Variables d'environnement.

.. code-block:: shell
   :linenos:
   :force:

    "C:\Program Files\PostgreSQL\10\bin"
    "C:\Program Files\PostgreSQL\10\lib"
        # 'C:\Program Files\' est à adapté en fonction de m'emplacement de 'PostgreSQL'

####

.. index::
   single: Redis
   single: DataBase; Redis

-----
Redis
-----

:Liens_WEB:
    * `Wikipedia : REDIS`_

    * `site officiel`_

    * `Un guide pour l'installation de Redis sous Windows10`_ (avec le Bash Ubuntu)

    * `Un résumé des commandes Redis`_

.. _`Wikipedia : REDIS`: https://fr.wikipedia.org/wiki/Redis
.. _`site officiel`: https://redis.io/
.. _`Un guide pour l'installation de Redis sous Windows10`: https://medium.com/@furkanpur/installation-redis-on-windows-10-13fbb055be7c
.. _`Un résumé des commandes Redis`: https://developer.mozilla.org/en-US/docs/Mozilla/Redis_Tips

Installation
============

Redis n'est officiellement pas supporter par Windows. L'installation se fait donc uniquement en
version Linux. 

L'installation sous Windows10 est tout de même possible depuis le Bash Ubuntu intégrer (activer
le mode développeur). L'utilisation d'un container (docker) est également possible.

Install Linux
-------------

.. code-block:: shell
   :linenos:
   :force:

    ## Téléchargement des dépendances
    sudo apt-get install build-essential
    sudo apt-get install tcl8.5

    ## Télchargement et décompression du paquet
    wget http://download.redis.io/releases/redis-4.0.2.tar.gz
    # --> verifier si une version plus récente n'existe pas

    tar xzf redis-4.0.2.tar.gz
    cd redis-4.0.2

    ## Compilation des sources
    sudo make distclean
    sudo make –j

    ## Test des éléments compilés avant l'installation
    sudo make test -j

    ## Installation du serveur
    sudo make install -j
    cd utils
    sudo ./install_server.sh
    # --> Accepter tous les choix par défaut

Démarrer le serveur
-------------------

    #. En mode manuelle :

        .. code-block:: JavaScript
           :linenos:
           :force:

            # Démarrer le service
            sudo service redis_6379 start

            # Rédémarrer le service
            sudo service redis_6379 restart

            # Arréter le service
            sudo service redis_6379 stop

    #. Démarrer le service automatiquement :

        .. code-block:: shell
           :linenos:
           :force:

            sudo update-rc.d redis_6379 defaults

Lancer le CLI
-------------

.. code-block:: shell
   :linenos:
   :force:

    redis-cli

Utilisation avec Python
-----------------------

:Liens_Web:     `Doc de la lib`_

.. _`Doc de la lib`: https://github.com/andymccurdy/redis-py

    #. Installation :

        .. code-block:: python
           :linenos:
           :force:

            sudo pip install redis

    # Exemple d'utilisation :

        .. code-block:: python
           :linenos:
           :force:

            >>> import redis
            >>> r = redis.StrictRedis(host='localhost', port=6379, db=0)
            >>> r.set('foo', 'bar')
            True
            >>> r.get('foo')
            'bar'

--------
Weblinks
--------

.. target-notes::