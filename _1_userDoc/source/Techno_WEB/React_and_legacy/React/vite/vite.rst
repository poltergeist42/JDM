====
Vite
====

.. index::
   single: Vite
   single: React; Vite

.. contents::
    :depth: 3
    :backlinks: top

####

    .. note:: 
        
        **Liens Web**

        * `ViteJs`_
        
.. _`ViteJs`: https://vitejs.dev/


-----------
Description
-----------

Vite (French word for "quick", pronounced /vit/) is a build tool that aims to provide a faster and
leaner development experience for modern web projects. It consists of two major parts:

  * A dev server that provides rich feature enhancements over native ES modules, for example
    extremely fast Hot Module Replacement (HMR).

  * A build command that bundles your code with Rollup, pre-configured to output highly optimized
    static assets for production.

Vite is opinionated and comes with sensible defaults out of the box, but is also highly extensible
via its Plugin API and JavaScript API with full typing support.

Key Features
============

 * **Instant Server Start**: Vite uses native ES modules to serve code, eliminating the need for
   bundling during development.

 * **Lightning Fast HMR**: Hot Module Replacement (HMR) that stays fast regardless of app size.

 * **Out-of-the-box Support**: Support for TypeScript, JSX, CSS, and more with no need for separate
   loaders.

 * **Optimized Build**: Pre-configured Rollup build with multi-page and library mode support.

 * **Universal Plugins**: Rollup-superset plugin interface shared between dev and build.

 * **Fully Typed APIs**: Flexible programmatic APIs with full TypeScript typing.

Usage with React
================

Vite has built-in support for React projects. To create a new React project using Vite,
you can use the following command:

    .. note:: 
        
        For a new project :

        
        .. code:: bash
            :number-lines:
            :force:

             npm create vite@latest <my-react-app> -- --template React

             # or
             npm create vite . # for a new project in the current directory (without template preset)


This will set up a new React project with Vite as the build tool, providing a fast development
environment and optimized production builds.

####

-------------------------------------
Migrate from Create React App to Vite
-------------------------------------

    .. note:: 
        
        **Liens Web**

        * `Killing the Create React App - CRA to Vite migration guide (Javascript)`_
        
.. _`Killing the Create React App - CRA to Vite migration guide (Javascript)`: https://dev.to/navdeepm20/killing-the-create-react-app-cra-to-vite-migration-guide-javascript-1f5


####

--------
Weblinks
--------

.. target-notes::