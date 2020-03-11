========
DataBase
========

PostGreSQL 
==========

:Liens_WEB:
            * https://www.postgresql.org/docs/
                # Page de documentation officiel

            * https://www.postgresql.fr/
                # site de la communauté francophone

            * https://docs.postgresql.fr/10/
                # Doc (FR)

Installation
------------

Sous Windows
++++++++++++

:Liens_WEB:
            * https://www.postgresql.org/download/
                # Page de téléchargement (toutes les versions et tous les environnements)

Télécharger l'install automatique et ce laisser guider. Lorsque l'installation est terminée, il faut
ajouter les 2 chemins suivants au 'PATH' dans les Variables d'environnement. ::

    "C:\Program Files\PostgreSQL\10\bin"
    "C:\Program Files\PostgreSQL\10\lib"
        # 'C:\Program Files\' est à adapté en fonction de m'emplacement de 'PostgreSQL'

####

Redis
=====

:Liens_WEB:
        * https://fr.wikipedia.org/wiki/Redis
          # Une définition de Redis

        * https://redis.io/
          # site officiel

        * https://medium.com/@furkanpur/installation-redis-on-windows-10-13fbb055be7c
          # Un guide pour l'installation de Redis sous Windows10 (avec le Bash Ubuntu)

        * https://developer.mozilla.org/en-US/docs/Mozilla/Redis_Tips
          # Un résumé des commandes Redis

Installation
------------

Redis n'est officiellement pas supporter par Windows. L'installation se fait donc uniquement en
version Linux. 

L'installation sous Windows10 est tout de même possible depuis le Bash Ubuntu intégrer (activer
le mode développeur). Lu'tilisation d'un container (docker) est également possible.

Install Linux
+++++++++++++

::

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
+++++++++++++++++++

    #. En mode manuelle ::

        # Démarrer le service
        sudo service redis_6379 start

        # Rédémarrer le service
        sudo service redis_6379 restart

        # Arréter le service
        sudo service redis_6379 stop

    #. Démarrer le service automatiquement ::

        sudo update-rc.d redis_6379 defaults

Lancer le CLI
+++++++++++++

::

    redis-cli

Utilisation avec Python
+++++++++++++++++++++++

:Liens_Web:
        * https://github.com/andymccurdy/redis-py
          # Doc de la lib

    #. Installation ::

        sudo pip install redis

    # Exemple d'utilisation ::

        >>> import redis
        >>> r = redis.StrictRedis(host='localhost', port=6379, db=0)
        >>> r.set('foo', 'bar')
        True
        >>> r.get('foo')
        'bar'


