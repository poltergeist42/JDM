=====
Redis
=====

.. index::
   single: Redis
   single: DataBase; Redis


.. contents::
    :depth: 3
    :backlinks: top


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

.. code:: shell
   :number-lines:
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

        .. code:: JavaScript
           :number-lines:
           :force:

            # Démarrer le service
            sudo service redis_6379 start

            # Rédémarrer le service
            sudo service redis_6379 restart

            # Arréter le service
            sudo service redis_6379 stop

    #. Démarrer le service automatiquement :

        .. code:: shell
           :number-lines:
           :force:

            sudo update-rc.d redis_6379 defaults

Lancer le CLI
-------------

.. code:: shell
   :number-lines:
   :force:

    redis-cli

Utilisation avec Python
-----------------------

:Liens_Web:     `Doc de la lib`_

.. _`Doc de la lib`: https://github.com/andymccurdy/redis-py

    #. Installation :

        .. code:: python
           :number-lines:
           :force:

            sudo pip install redis

    # Exemple d'utilisation :

        .. code:: python
           :number-lines:
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