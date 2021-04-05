========
XML_JSON
========

Format JSON
===========

Ensemble des informations sur la création et l'utilisation des fichiers JSON

:Liens_Web:
            * http://www.tutorialspoint.com/online_json_editor.htm
                # Générateur online de JSON

            * http://www.objgen.com/json?demo=true
                # Un autre générateur de JSON
            
Généralités
-----------

    TODO: ne pas laisser vide

Powershell
----------

    TODO: ne pas laisser vide

Python
------

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

Format XML
==========

Ensemble des informations sur la création et l'utilisation des fichiers XML

:Liens_Web:
            * https://fr.wikipedia.org/wiki/Extensible_Markup_Language
                # Présentation du XML
                
            * https://www.tutorialspoint.com/online_xml_editor.htm
                # Générateur online de XML

Généralités
-----------

    TODO: ne pas laisser vide

Powershell
----------

:Liens_Web:
            * http://blog.aidalinfo.fr/?p=75
                # Exemple d'utilisation d'un fichiers XML

Python
------

    TODO: ne pas laisser vide
