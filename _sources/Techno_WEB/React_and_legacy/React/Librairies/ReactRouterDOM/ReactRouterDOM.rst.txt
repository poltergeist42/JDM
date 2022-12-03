================
React-Router-DOM
================

.. index::
   single: ReactRouterDOM
   single: React; ReactRouterDOM

.. contents::
    :depth: 3
    :backlinks: top

####

:Liens_Web:
    * `gérer la navigation programmatique`_

    * `faire un redirect avec le composant react-router-dom après une requête POST`_

    * `Quick Start`_ : semble être la doc officiel

.. _`gérer la navigation programmatique`: https://www.journaldunet.fr/web-tech/developpement/1441259-comment-gerer-la-navigation-programmatique-avec-react-router/
.. _`faire un redirect avec le composant react-router-dom après une requête POST`: https://www.journaldunet.fr/web-tech/developpement/1441289-comment-faire-un-redirect-avec-le-composant-react-router-dom-apres-une-requete-post/
.. _`Quick Start`: https://reacttraining.com/react-router/web/guides/quick-start

React-routeur-dom est un paquet qui permet de rediriger vers une nouvelle url et donc de naviguer entre les différentes pages
en gardant l'esrpie "monopage" de React.

Cette librairie est utilisée depuis le composoant racine, génrallement le composant "App.js".

.. warning::
    A chaque changement de composant ce dernier est recharger dans le DOM. Il est donc important de
    **percisté les données** avec le localstorage ou une base de donnés. Dans le cas contraite
    toutes les données seront perdu puisque le composant sera chargé à son état initial.

####

------------------------------
Cookbook : React-Router-DOM v6
------------------------------

:Liens_Web:
        * `Comprendre React Router V6 en 20 minutes`_

.. _`Comprendre React Router V6 en 20 minutes`: https://www.youtube.com/watch?v=hOg-hJDw1NM

Le composant <Switch/> n'est plus utilisé dans la v6. Il est remplacé par le composant <Routes/>

    #. Le composant <BrowserRouter></BrowserRouter> doit être placé au plus haut dans l'arborescence,
       générallement dans "index.js".

       .. code:: JavaScript

          // Document : index.js

          // Import de librairie
          import React from 'react';
          import ReactDOM from 'react-dom/client';
          import { BrowserRouter } from 'react-router-dom';

          // Import des pages et des composant
          import App from './App';

          const root = ReactDOM.createRoot(document.getElementById('root'));
          root.render(
            <BrowserRouter>
                <App />
            </BrowserRouter>
          );

    #. Il faut ensuite définir les différente routes dans le composant <App /> à l'aide des
       composants <Routes></Routes> et <Route>.
       
       La nécéssité de créer des routes et liée au faite d'avoir plusieurs pages chacune dépendantes
       d'une URL spécifique. Il peut cependant y avoir des composant statiques commun entre toutes
       les pages. C'est le cas des barres de navigation et des footers. Ces éléments doivent être
       placés en dehors du composant <Routes></Routes>.

       .. code:: JavaScript

         // Document : App.js

         // Import de librairie Tiers
         import React from 'react';
         import { Routes, Route } from 'react-router-dom';

         // Import des pages et des composant
         import Navigation from './components/Navigation/Navigation';
         import Home from './pages/Home/Home';
         import Entree from './pages/Entree/Entree';
         import Resume from './pages/Resume/Resume';

         // Import de CSS
         import './App.css';

         const App = () => {
         return (
             <>
             <Navigation />
             <Routes>
                 <Route path="/Entree" element={<Entree />} />
                 <Route path="/Resume" element={<Resume />} />
                 {/* Toutes les entrée de l'URL différente des routes précédente sont redirigé vers 'Home' */}
                 <Route exact path="/" element={<Home />} />
                 <Route path="*" element={<Home />} />
             </Routes>
             </>
           )
         }

        export default App;
 
####

---------------
Link vs NavLink
---------------

    :<Link />:      Permet de créer des liens vers des routes. C'est l'équivalent des
                    balises <a></a> dans le html.

    :<NavLink />:   Permet également de créer des liens vers des routes mais avec une notion
                    d'analyse de l'éléments sélectionné. Cette analyse permet de mettre en evidence
                    le liens sélectionné par rapport aux autres liens non séléctionnés. NavLink est
                    donc plus souvent utilisé dans les barres de navigation.

####

--------
Weblinks
--------

.. target-notes::