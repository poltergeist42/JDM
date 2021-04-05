===============
Hacking Ethique
===============

.. contents::
   :backlinks: top
   :depth: 3

Scan de port avec nmap
======================

        .. code-block:: shell
           :linenos:
           :force:

            # nmap
            nmap -A -p- -T4 <ip ou plage ip>

            # Par défaut, le scan s'effectue sur le TCP (-sS). Pour forcer le scan en UCP il faut
            # utiliser l'option -sU.
            #
            # -A: Enable OS detection, version detection, script scanning, and traceroute
            #
            # -p-: permet de scanner tous les ports si le deuxième "-" est absent, seuls les 1000
            #      Premiers ports seront scanner
            #
            # -T4: permet de déterminer la vitesse du scan 0-lent --> 5-rapide

:.. warning:: Attention il n'y a pas de time out en UDP. Le scan peux donc durer indéfiniment. Il
              est donc conseiller de ne scanner que les 1000 premiers ports.