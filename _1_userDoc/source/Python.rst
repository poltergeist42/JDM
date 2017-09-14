======
PYTHON
======

:Liens_Web:
            * http://python.jpvweb.com/python/mesrecettespython/doku.php?id=Sommaire
                # (fr) de nombreux exemple et explication sur des utilisation spécifique
                # de fonctionnalité python
                
------------------------------------------------------------------------------------------

Ensemble de commande utiles
===========================

:Liens_Web:
            * https://python.developpez.com/faq/?page=Generalites

------------------------------------------------------------------------------------------

Obtenir de l'aide sur une class ou une méthode  (python)
========================================================

    Dans la console Python, saisir  : ::
    
            help("nom_de_la_class")

------------------------------------------------------------------------------------------

Lignes de code à insérer au debut de chaque script sous Linux
=============================================================

::

#!/usr/bin/env python3
# -*- coding: utf-8 -*-

**N.B :** copier ces lignes entièrement sans oublier le "#" devant.

------------------------------------------------------------------------------------------

os library
==========

:Liens Web:
            * http://python.developpez.com/faq/?page=Repertoire
                # résumer des commandes pour le traitement des répertoires
                
            * https://docs.python.org/3.4/library/os.html
                # doc officiel de la librairie
                
Traitement des répertoires
--------------------------

        #. Connaître le répertoire de travail ::
        
            import os
                # on commence par importer la bibliothèque 'os'
            os.getcwd()
                
        #. Redéfinir le répertoire courant ::
        
            import os
            os.chdir("mon_rep/de/travail")
                # meme sous Windows, il faut remplacer les "\" dans le chemin de
                destination par des "/"
                
                ex : os.chdir("C:/mntJeanCloud/Perso/LAB/Pierre/python/projet/appliActivity")
                
        #. Savoir si un chemin représente un répertoire ? ::
        
            os.path.isdir(path)
                # renvoi True si path désigne un répertoire existant
                
        #. Créer un répertoire ::
        
            os.mkdir(path, mode=0777)
                # créé un répertoire le plus à droite dans path
                
            os.makedirs(path, mode=0777)
                # crée tous les répertoires de path n'existant pas
                
        #. Supprimer un répertoire ::
        
            os.rmdir(path)
                # supprime le répertoire path si celui-ci est vide
                
        #. Supprimer un fichiers ::
        
            os.remove([nom_du_fichier])
                
                
        #. Renommer/déplacer un répertoire
        
            ::
        
                os.rename(src, dst)
                    # permet de renommer le répertoire src en le répertoire dst,
                    # tous les répertoire parent de dst doivent cependant déjà exister,
                    # une erreur étant sinon retournée.
                    
                os.renames(src, dst)
                    # permet de renommer le répertoire src en dst tout en créant si
                    # nécessaire les répertoires parent du répertoire de destination.
                
            **N.B** : Si le répertoire de destination se trouve sur le même système
            de fichiers, vous pouvez utiliser aussi bien les fonctions **os.rename**,
            **os.renames** que **shutil.move** sinon **préférez shutil.move**,
            les 2 autres fonctions pouvant échouer à leur tâche.
        
        #. Connaître la taille d'un répertoire
        
        Pour connaître la taille d'un répertoire, il suffit de le parcourir
        son arborescence en ajoutant la taille de chaque fichier rencontré. ::
        
            import os.path  
      
            def sizedirectory(path):  
                size = 0  
                for root, dirs, files in os.walk(path):  
                    for fic in files:  
                        size += os.path.getsize(os.path.join(root, fic)) 
                return size 
              
            print( sizedirectory([path_=_mon_chemin_de_dossier]))

------------------------------------------------------------------------------------------

shutil library
==============

:Liens Web:
            * https://docs.python.org/3.4/library/shutil.html
                # Documentation officielle de la lib.
                
Traitement des répertoires
--------------------------

        #. Supprimer un répertoire non vide ::
        
            shutil.rmtree(path)
        
        #. Renommer/déplacer un répertoire ::
        
            shutil.move(src, dst)
                # renomme exactement comme os.renames le répertoire src en dst si
                # le répertoire de destination est sur le même système de fichiers.
                # Autrement elle copie simplement src sur dst puis efface src.


------------------------------------------------------------------------------------------

psutil (process and system utilities)
=====================================

Pour surveiller différent process machine ( CPU, RAM, Network, etc)

:Liens_Web:
            * https://code.google.com/archive/p/psutil/wikis/Documentation.wiki
                # doc officielle
                
            * https://pypi.python.org/pypi/psutil
                # doc officielle (mais une autre)
                
            * https://github.com/giampaolo/psutil
                # Source github

------------------------------------------------------------------------------------------
                
pip (Python installing packages)
================================

:Liens web:
            * http://deusyss.developpez.com/tutoriels/RaspberryPi/PythonEtLeGpio/
            * http://www.inspyration.org/tutoriels/utiliser-pip
            * http://sametmax.com/votre-python-aime-les-pip/
                # ce liens montre des exemples d'utilisation de pip

Installation de PIP
-------------------

    #. Récupération et installation du paquet ::
    
        wget https://bootstrap.pypa.io/get-pip.py
            # recuperation du script d'installation
            
        python get-pip.py
            # se placer dans le répertoire d'installation et lancer le script
            # une élévation est peut être nécessaire
                    
    #. Installation depuis apt-get ::
    
        sudo apt-get install python3-pip
            # pip sera installer dans le répertoire suivant :
            # /usr/bin/pip3
                
                    
Utilisation de PIP
------------------

    La commande pip s’exécute directement dans le shell
    
    #. Exécuter pip pour python3 dans un environnement Linux ::
    
        pip-3.2 [une_commande]
                ou
        pip3 [une commande]
    
    #. obtenir la liste des options ::
    
        pip help
            # fonctionne aussi avec pip tout seul
                    
    #. chercher un paquet ::
    
        pip search [nom_du_paquet_rechercher]
            # on peut rechercher plusieurs termes en les séparent par des espaces
            # ex : pip search py3 numpy
            # attention, la recherche est également faite sur
            # les définissions des paquets
                    
    #. installer un paquet ::
    
        pip install [nom_du_paquet_a_installer]

------------------------------------------------------------------------------------------

Les environnements virtuels Python : virtualenv et virtualenvwrapper (version Linux)
====================================================================================

:Liens Web:
            * http://sametmax.com/les-environnement-virtuels-python-virtualenv-et-virtualenvwrapper/

installation des environnements virtuels
---------------------------------------

    #.  Installation de virtualenv et virtualenvwrapper
    
    N.B : il est préférable de les installer en sudo et non en root (su) ::
        
        sudo pip install virtualenv
        sudo pip install virtualenvwrapper

configuration des environnements virtuels
----------------------------------------

    #. Créer un dossier pour les environnements virtuels
    
        * Se placer dans le répertoire de l'utilisateur (/home/pi)
        * Créer un dossier pour les environnements virtuels
        
    ::
                
            mkdir virtualenv
                
    #.   Editer le fichier .bashrc ::
    
            sudo nano .bashrc
                
    #.   renseigner le fichier .bashrc
    
        * Se placer à la fin du fichier et saisir : ::
            
            # virtualenvwrapper
            
            export WORKON_HOME=~/virtualenv
                # si le dossier n'a pas été créer au même endroit ou avec le même
                # nom, modifier la ligne précédente en conséquence
                
            mkdir -p $WORKON_HOME
            source  /usr/local/bin/virtualenvwrapper.sh
                # si virtualenvwrapper.sh n'est pas installer au même endroit,
                # adapter le chemin d'accès au fichier
                    
Utilisation environnements virtuels
-----------------------------------

    #. Création d'un nouvel environnements virtuel ::
        
        mkvirtualenv [nom_de_l_environnement] -p /usr/bin/python3.2
            # ex : mkvirtualenv env1 -P /usr/bin/python3.2
            
            # un dossier du nom de votre environnement virtuel est alors créer
            # dans le dossier virtualenv créer en section 2.1
            
            # l'option "-p usr/bin/python3.2" permet de configurer environnements
            # virtuel pour python3. par défaut sur Rpi, c'est python2 qui est 
            # utilisé
                
    #. Activation / désactivation de l’environnent
        Pour être utilisé, un environnement doit être activé : ::
                    
            workon [nom_de_l_environnement]
                    # ex : workon env1
                    
        A la fin de son utilisation, ou pour passer sur un autre environnement, il faut
        le désactiver : ::
        
            deactivate
                # c'est tout !
                # Attention, ce n'est pas deSactivate,
                # mais bien deactivate sans "S"
                
    #. supprimer un environnement ::
    
        rmvirtualenv [nom_de_l_environnement]
            # ex : rmvirtualenv env1
            # le dossier de l’environnement sera également supprimer

------------------------------------------------------------------------------------------

Un shell Python qui fait de l'auto complétion
=============================================

    * ipython
    * ipython3 (pour python3)

------------------------------------------------------------------------------------------

convertir un string en bytes
============================
::
 
    b = bytes(mystring, 'utf-8')
                    
------------------------------------------------------------------------------------------
                    
Connaître l'adresse mémoire d'un objet
======================================
::

    a = 'a'
    id(a)
        # on récupère l'adresse au format décimal
    >>> 45748752
    
    hex( id(a) )
        # récupère l'adresse et on la convertit directement au format hexadécimal
        
    >>> '0x2ba1210'
                    
------------------------------------------------------------------------------------------

Affectation, copy et deepcopy
=============================

    #. Affectation :
        L'affectation ne créer pas un nouvel objet. Elle se contente de pointer sur la
        même adresse en mémoire ::
        
            a = 1
            b = a
            
            a = b = 1
            # a et b ont la même adresse
            >>> hex( id(a) )
            '0x5ec5e370'
            >>> hex( id(b) )
            '0x5ec5e370'
            
    #. copy
        La copy permet de créer un nouvel objet qui pointe sur l'adresse du premier objet 
        tant que la valeur du second n'a pas été modifier ::
        
            >>> import copy
            >>> a = 1
            >>> b = copy.copy( a )
            >>> hex( id(a) )
            '0x5ec5e370'
            >>> hex( id(b) )
            '0x5ec5e370'
            >>> a
            1
            >>> b
            1
            >>> b = 2
            >>> a
            1
            >>> b
            2
            >>> hex( id(a) )
            '0x5ec5e370'
            >>> hex( id(b) )
            '0x5ec5e380'
            
        Attention la copy d'une liste crée un nouvel objet mais les adresse des données
        pointée par la liste reste les mêmes, donc la modification d'une valeur dans
        la liste B modifiera aussi la valeur de la liste A ::
        
            >>> a = [1, 2, 3]
            >>> b = copy.copy(a)
            >>> a
            [1, 2, 3]
            >>> b
            [1, 2, 3]
            >>> hex( id(a) )
            '0x593d78'
            >>> hex( id(b) )
            '0x2f81300'
            >>> hex( id(a[0]))
            '0x5ec5e370'
            >>> hex( id(b[0]))
            '0x5ec5e370'
            
        On parle de shallow copy
            
    #. deepcopy
        Le deepcopy permet de faire une copie "en profondeur", c'est à dire une copie
        complète y compris le contenu des données itérables ::
        
            >>> a
            [1, 2, 3]
            >>> b = copy.deepcopy(a)
            >>> b
            [1, 2, 3]
            >>> hex( id(a) )
            '0x593d78'
            >>> hex( id(b) )
            '0x593800'
        

------------------------------------------------------------------------------------------

faire un exécutable à partir d'un script
========================================

:les softs:
           * py2exe
           * cx_Freeze

La procédure d'utilisation :

:Liens WEB:
            * http://python.developpez.com/faq/?page=Py2exe     
                # tuto pour py2exe
                                                
            * https://www.youtube.com/watch?v=k3VoLjGA6jI
                # video EN sur py2exe
                                                
            * https://pypi.python.org/pypi/py2exe/0.9.2.0/
                # py2exe (soft + install)
                    
            * https://pypi.python.org/pypi?:action=display&name=cx_Freeze&version=4.3.4
                # cx_Freeze (soft)
                
            * http://python.jpvweb.com/python/mesrecettespython/doku.php?id=cx_freeze
                # cookBook CX_Freeze (fr)
    
------------------------------------------------------------------------------------------

créer un setup.py (installable avec pip) et mettre sa bibliothèque en ligne sur pypi
====================================================================================

:Liens_Web:
            * http://sametmax.com/creer-un-setup-py-et-mettre-sa-bibliotheque-python-en-ligne-sur-pypi/
                # Un cook book (fr)

------------------------------------------------------------------------------------------

Fichiers de configuration (.ini)
================================

:Liens WEB:  
            * http://stackoverflow.com/questions/8884188/how-to-read-and-write-ini-file-with-python
               # exemple util pour comprendre le fonctionnement                                              
            * http://www.marclebrun.be/wiki/doku.php?id=python:fichier_de_configuration_configparser
               # Exemple en français (python2)
            * http://www.developpez.net/forums/blogs/208887-tyrtamos/b23/simplifier-gestion-fichiers-ini-python/
               # Autre exemple (pytohn3) en français
            * https://docs.python.org/3.4/library/configparser.html
               # Doc officiel (EN)

------------------------------------------------------------------------------------------

Format JSON
===========

:Liens WEB:
            * http://sdz.tdct.org/sdz/serialisez-vos-objets-au-format-json.html
                # utiliser json avec python, les bases et en français
            * http://deusyss.developpez.com/tutoriels/Python/les-modules-de-configuration/
            * https://docs.python.org/3.4/library/json.html
                # la doc Python 3.4 (en)
            * https://stackoverflow.com/questions/12309269/how-do-i-write-json-data-to-a-file-in-python
                # La fonction postée par JRCS le 24/01/2017 est intéressante
                
            #. Exemple d'utilisation intéressant : ::
            
                from json import dump, load
                from time import sleep
                from random import random

                def json_file(path, data = None, delay = 0.1):
                    while True:
                        try:
                            if data == None:
                                with open(path, "r", encoding = "utf-8") as f:
                                    return load(f)
                            else:
                                with open(path, "w", encoding = "utf-8") as f:
                                    return dump(data, f, indent=4, sort_keys=True)
                        except:
                            sleep(random()*delay) # concurrency
                
------------------------------------------------------------------------------------------

web framework
=============

Bottle
------

:Liens Web:
            * http://bottlepy.org/docs/dev/index.html
                # Doc officielle
                
Bottle is a fast, simple and lightweight WSGI micro web-framework for Python.


Flask
-----

:Liens Web:
            * http://blog.miguelgrinberg.com/post/the-flask-mega-tutorial-now-with-python-3-support
                # tuto complet (en)
            * https://phollow.fr/2012/08/demarrer-la-creation-site-python-flask/
                # un exemple
            * http://flask.pocoo.org/docs/0.11/
                # Doc officielle
            * http://flask.pocoo.org/docs/0.11/quickstart/
                # le QuickStart de la doc officielle
            * http://flask.pocoo.org/docs/0.11/tutorial/#tutorial
                # tuto de la doc officeille
            
Flask is a micro webdevelopment framework for Python.

------------------------------------------------------------------------------------------

Les décorateurs
===============

:Liens Web:
            * http://gillesfabio.com/blog/2010/12/16/python-et-les-decorateurs/
                # Exemple + explications en fr
            * http://sametmax.com/comprendre-les-decorateurs-python-pas-a-pas-partie-1/
            * http://sametmax.com/comprendre-les-decorateur-python-pas-a-pas-partie-2/
                # une explication plus pousser, partie 1 et 2 (Sam & Max)
            * http://python.jpvweb.com/python/mesrecettespython/doku.php?id=decorateurs_modeles
                # (fr) plus facile à comprendre que Sam & Max
                
            exemple d'utilisation : ::
            
                >>> def decorateur(fonct) :
                ...     """ fonction décorateur permettant de donnée le temps d’exécution d'une fonction """
                ...     @functools.wraps( fonct )
                ...     def appelFonc( *args, **kwargs ) :
                ...             t = time.time()
                ...             tache = fonct( *args, **kwargs )
                ...             print(f"temps d’exécution : {time.time()-t}")
                ...             return tache
                ...     return appelFonc
                ...
                >>>
                >>> @decorateur
                ... def f(a, b, c) :
                ...     """ affiche le contenue et le type des variables passées en argument """
                ...     print( f"{a} - {type(a)}")
                ...     print( f"{b} - {type(b)}")
                ...     print( f"{c} - {type(c)}")
                ...
                >>> f('a', 1, c=f)
                a - <class 'str'>
                1 - <class 'int'>
                <function f at 0x000001F6E7792268> - <class 'function'>
                temps d'execution : 0.00653386116027832
                
------------------------------------------------------------------------------------------

Tester un type attendu
======================

    #. Pour Test si une variable ou une instance et bien du type attendu : ::
        
        isinstance( [variable_a_traiter], [type_attendu] )
        
        ex :
        
        >>> a = [1, 2, 3]
        >>> isinstance( a, list )
        True
            
------------------------------------------------------------------------------------------

Packing et UnPacking (utilisation de : '*args' et '**kwargs')
=============================================================

:Liens Web:
            * http://deusyss.developpez.com/tutoriels/Python/args_kwargs/
                # complet en fr
            * http://sametmax.com/operateur-splat-ou-etoile-en-python/
                
**N.B :** on parle de l'opérateur **'splat'** lorsque l'on parle de l’astérisque **'*'**
                
    #. "*args"
    
        **'*args'** permet de passer, à une fonctions, des arguments en nombres et de
        types inconnue puis converti l'ensemble en tuple. Dans le prototype d'une
        fonction, cet argument est utilisé comme "positional argument".
        ex : ::
        
            >>> def f(*args) :
            ...     print( args )
            ...     for i in range( len(args) ) :
            ...             print( "{} - {}".format(args[i], type(args[i])))
            ...
            >>> f(1, 'a', True)
            (1, 'a', True)
            1 - <class 'int'>
            a - <class 'str'>
            True - <class 'bool'>
            
    #. "**kwargs"
    
        **'*kwargs'** permet de passer, à une fonctions, des arguments en nombres et de
        types inconnue puis converti l'ensemble en dictionnaire. Dans le prototype d'une
        fonction, cet argument est utilisé pour les argument par défaut.
        ex : ::
        
            >>> def fd(**kwargs) :
            ...     print( kwargs )
            ...
            >>> fd(a=1, b=2, c=3)
            {'c': 3, 'a': 1, 'b': 2}
            
**N.B :** Les termes **"args"** et **"kwargse"** sont des conventions et peuvent être
remplacés par un nom plus parlant mais se n'est pas conseillé.

------------------------------------------------------------------------------------------

Passer des paramètres à un programme avec argparse
==================================================

:Liens Web:
    https://openclassrooms.com/courses/apprenez-a-programmer-en-python/un-peu-de-programmation-systeme
        # une bonne introductions sur la gestion des flux entrant et sortant ainsi que
          sur argparse
          
    https://docs.python.org/3.4/library/argparse.html
        # La doc officielle
        
    https://docs.python.org/3.4/howto/argparse.html
        # Un tuto tire de la doc officielle
        
    http://www.developpez.net/forums/d1477855/autres-langages/python-zope/general-python/marche-argparse/
        # Voir le post de 'tyrtamos' du 27/10/2014 à 16h40
        
    #. Obtenir de l'aide sur les options de notre code
    
        Même si on ne met pas l'option '-h' ou "- -help", cette options est implémentée par
        défaut dès lors que l'on crée un parser avec argparse. Cette options vas lister et
        détailler nos propre options : ::
        
            python code.py --help
            usage: code.py [-h]

            optional arguments:
              -h, --help  show this help message and exit
              
    #. Elements de bases ::
    
        import argparse 

        parser = argparse.ArgumentParser()
            # Création de l'instance

        args = parser.parse_args()
            # Récupérer les arguments
        
    #. ajouter des arguments a parser ::
    
        parser.add_argument([listes_des_options_separees_par_des_virgules])

    #. positional arguments
    
       Les 'positional arguments' sont des arguments obligatoires lors de l'appel 
       du script. ils sont déclaré entre guillemets (ou simples cotes) et sans tiret. 
       Ils n'ont pas non plus un appel long et un appel court.
       
        ex : ::
       
            parser.add_argument("x", type=int, help="le nombre à mettre au carré")
            
    #. optional arguments
    
        les 'optional arguments' sont des argument facultatifs. Ils sont déclare entre 
        guillemets (ou simples cotes) avec tiret. Les appels court sont composes 
        d'un tiret et d'une lettre. Les appels long sont composes d'un double tiret et
        d'un nom significatif. Les 2 appels peuvent être soit déclare ensemble ou déclarer
        seuls (l'un ou l'autre)
        
        **N.B :** même si il n'y a pas de d'argument optionnel de déclaré, il y en a 
              toujours au moins un puisque le help (-h ou --help) est ajouter
              automatiquement.
              
        ex : ::
        
            parser.add_argument("-v", "--verbose", action="store_true", help="augmente la verbosité")
            
    #. l'exemple tire du help( "argparse" ) ::
    
        The following is a simple usage example that sums integers from the
        command-line and writes the result to a file::

            parser = argparse.ArgumentParser(
                description='sum the integers at the command line')
            parser.add_argument(
                'integers', metavar='int', nargs='+', type=int,
                help='an integer to be summed')
            parser.add_argument(
                '--log', default=sys.stdout, type=argparse.FileType('w'),
                help='the file where the sum should be written')
            args = parser.parse_args()
            args.log.write('%s' % sum(args.integers))
            args.log.close()

------------------------------------------------------------------------------------------

Les context managers et le mot clé 'with' en Python
===================================================

:Liens Web:
    http://sametmax.com/les-context-managers-et-le-mot-cle-with-en-python/
        # Article de présentation et d'utilisation sur les context managers
        
------------------------------------------------------------------------------------------
        
Connaître le nombre de CPU d'un système
=======================================

::

    os.cpu_count()
    
------------------------------------------------------------------------------------------
    
logging Library
===============

:Liens Web:
            * http://sametmax.com/ecrire-des-logs-en-python/
                # L'explication qui vas bien
            
            * https://docs.python.org/3.4/library/logging.html
                # La doc officielle
                
:Description:
            Cette Lib permet de faire du log sur des éléments.
            
------------------------------------------------------------------------------------------

hashlib Library
===============

:Liens Web:
            * http://sametmax.com/md5-en-bash-php-python-et-javascript/
                # un petit exemple vite fait
                
            * https://docs.python.org/3.4/library/hashlib.html
                # la doc de la lib
                
------------------------------------------------------------------------------------------

Utilisation de l'underscore (_)
===============================

:Liens Web:
            * http://sametmax.com/a-propos-des-attributs-prefixes-de-deux-underscores/

Publique, Protégé et Privé
--------------------------

Bien qu'il n'y ai pas de notion "protégé" ou "privé" en python il y a des conventions qui
permettent d'introduire ces notions dans les interpréteurs

    #. Publique
    
        C'est l'affectation classique.  Cette affectation sera visible dans l'API (dir()
        help()) ::
        
            maVariablePublique = 1
            
    #. Protégé
    
        On préfix notre objet (attribut ou méthode) avec un simple underscore (_). L'objet
        n’apparaîtra pas dans l'API mais sera utilisable de l'extérieur si on l'appel
        spécifiquement ::
        
            _maVaribleProtegee = 2
            
    #. Privé
    
        On préfix notre objet avec un double underscore (__). Il n’apparaîtra pas dans
        l'API et renverra un "AttributError" si on l'appel spécifiquement ::
        
            __maVariablePrivee = 3
            
Exemple d'utilisation : ::

    >>> class C(object) :
    ...     pub     = 1
    ...     _prot   = 2
    ...     __priv  = 3
    ...     def getProt(self) :
    ...             return self._prot
    ...     def getPriv(self) :
    ...             return self.__priv
    ...
    >>> test = C()
    >>> help(test)
    Help on C in module __main__ object:

    class C(builtins.object)
     |  Methods defined here:
     |
     |  getPriv(self)
     |
     |  getProt(self)
     |
     |  ----------------------------------------------------------------------
     |  Data descriptors defined here:
     |
     |  __dict__
     |      dictionary for instance variables (if defined)
     |
     |  __weakref__
     |      list of weak references to the object (if defined)
     |
     |  ----------------------------------------------------------------------
     |  Data and other attributes defined here:
     |
     |  pub = 1

    >>> test._prot
    2
    >>> test.__priv
    Traceback (most recent call last):
      File "<stdin>", line 1, in <module>
    AttributeError: 'C' object has no attribute '__priv'
    >>> test.getPriv()
    3
    
------------------------------------------------------------------------------------------

Connaître l'os de travail
=========================

::

    ex Win :
    >>> import os
    >>> os.name
    'nt'
    
    ex Mac / Linux :
    >>> import os
    >>> os.name
    'posix'
    
------------------------------------------------------------------------------------------

matplotlib
==========

:Liens_Web:
            * http://www.science-emergence.com/Articles/Tutoriel-Matplotlib/
                # petite introduction (fr)
                
            * http://matplotlib.org/index.html
                # le site officiel
                
            * https://matplotlib.org/users/tutorials.html
                # tuto du site officiel
                
    