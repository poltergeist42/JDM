==================
Visual Studio Code
==================

.. index::
   single: IDE & Text Editor; VS Code

.. contents::
   :backlinks: top

Obtenir de l'aide sur les diférentes commandes et fonctionnalitées
==================================================================

    Menu Help --> Interactive Playground

**NDLR**: ça c'est la vie !


Documentation Officielle
========================

    :Liens_Web:
        * `Doc officiel de Microsoft`_ : cette doc est accessible depuis le menu Help --> Documentation

.. _`Doc officiel de Microsoft`: https://code.visualstudio.com/docs#vscode

Snippets
========

    :Liens_Web:
        * `Création de snippets personnalisés`_ : # information sur la création et l'utilisation des snippets
        * `Snippet Generator`_ : Générateur de snippet pour : vscode, Sublime Text et Atom
        
.. _`Création de snippets personnalisés`: https://code.visualstudio.com/docs/editor/userdefinedsnippets
.. _`Snippet Generator`: https://snippet-generator.app/

Multi-Line and multi-Cursor Editing
===================================

    :Liens_Web:
        * `Multi-Line Editing`_

.. _`Multi-Line Editing`: https://kencenerelli.wordpress.com/2018/03/25/visual-studio-code-multi-line-and-multi-cursor-editing/

Placer une ligne vertical sur la droite de la fenêtre de l'editeur
==================================================================

File --> Settings --> Rechercher "Editor:Rulers" --> cliquer sur "Edit in settings.json" ::

    "editor.rulers": [
        
        100
        
        ],