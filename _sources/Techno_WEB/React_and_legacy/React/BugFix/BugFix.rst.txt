=========
Bug & Fix
=========

.. index::
   single: Bug&Fix
   single: React; Bug&Fix
   single: NPM; Bug&Fix

.. contents::
    :depth: 3
    :backlinks: top

####

-----------------------------------------------------------------
Erreur d'execution d'un script dans une librairie de node_modules
-----------------------------------------------------------------

Il peut arriver qu'une erreur se produise lors de l'éxécution d'un script issue d'une librairie
(les éléments contenus dans node_modules). Cette erreur se produit la plus part du temps après une
mise à jour d'une librairie ou de NPM lui même.

Pour corriger se genre de problème il faut lancé un audit et une correction des libraires.

    .. code:: shell

        npm update
        npm audit fix --force

####

--------
Weblinks
--------

.. target-notes::   