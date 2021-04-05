================
Machine Learning
================

---------------------
L'équation de Bellman
---------------------

:Liens_Web:

            * https://www.rand.org/content/dam/rand/pubs/papers/2008/P550.pdf
                # Richard Bellman, 1954, The Theory of Dynamic Programming

L'équation de Bellman est à la base de l'apprentissage par renforcement.

Concept / définission
=====================

    * :math:`s` - State (l'état) : Il s'agit de l'état dans lequel l'environnement est.

    * :math:`s'` : l'état dans le quel on va arriver

    * :math:`a` - Action : Les actions que peut prendre l'agent

    * :math:`R` - Reward (Récompense) : Récompense obtenu par l'agent pour rentrez dans un certain état
      (+1, 0 ou -1)

    * :math:`\gamma` (Gamma) - Discount (Réduction): il s'agit du facteur de réduction 
      (compris entre 0 et 1). Plus cette valeur est proche de 0, plus ont s'éloigne du résultat
      et / ou de la solution.

    * :math:`V` : La valeur d'un certain état

Equation simplifiée
-------------------

Sous cette forme simplifié, l'équation est déterministe. Elle ne tien pas compte des éléments 
aléatoires (`Stochastique <https://fr.wikipedia.org/wiki/Stochastique>`_).

    .. math::

       V(s) = \underset {a} {max} \left (R(s, a) + \gamma V(s') \right)

Pénalité de vie
===============

La pénalité est une valeur négative (à définir soit même) affectée à chaque action. Cela permet de 
forcer l'IA à trouver une solution le plus vite possible.

Plus la récompense :math:`R` est proche de 0, moins le risque pris par l'IA sont important. Plus la
récompense :math:`R` est éloigné, plus les risques pris part l'IA seront important.

Il faut trouver une valeur qui pousse l'IA à trouver une solution tout en ne prenant que des risques
modérés.

    :Exemples:

        Pour une Récompense Final de 1 si nous affectons une Récompense d'Action de 0, -0.3, -0.5
        ou -2

            * Si RA= :math:`0` : L'IA n'optimisera pas la recherche de solution.

            * Si RA= :math:`-0.3` : L'IA optimisera légèrement sa recherche de solution mais aucuns risque
              ne sera pris dans le choix de l'action.

            * Si RA= :math:`-0.5` : l'IA optimisera beaucoup sa recherche de solution, mais ne prendra que 
              des risques modérés.

            * Si RA= :math:`-2` : l'IA prendra tous les risques possibles pour parvenir à une solution le 
              plus vite possible.

Chaine de Markov et Processus de Décision Markovien (MDP)
=========================================================

    :Liens_Web:
                * https://pdfs.semanticscholar.org/968b/ab782e52faf0f7957ca0f38b9e9078454afe.pdf
                    # Martijn van Otterlo, 2009, Markov Decision Processes: Concepts and Algorithms

                * https://fr.wikipedia.org/wiki/Processus_stochastique
                    # Définition Wikipédia

                * https://fr.wikipedia.org/wiki/Processus_de_Markov
                    # Définition Wikipédia

    :Définissions:
                * :math:`P` - Processus de Décision Markovien (MDP) : Moyenne de la somme des états
                  possibles (:math:`s'`). Il s'agit de l'introduction d'un facteur aléatoire dans un 
                  environnement déterministe.

Equation de Belman augmentée du MDP
-----------------------------------

    * **Le processus de Markov** : Il va définir la façon dont l'environnement est construit.

    * **Le MDP** : Il va décrire la façon dont l'agent prend une décision.

    .. math::

       V(s) = \underset {a} {max} \left (R(s, a) + \gamma \underset {s'} {\sum} P(s, a, s')V(s') \right)

Q-Learning : Intuittion
=======================

    :Définissions:

                * :math:`Q` - Qualité : définit la qualité de l'action à venir :math:`Q(s, a)` par 
                  opposition à :math:`V` qui définit la valeur de l'état :math:`V(s)`.

Définission de l'équation de Bellman en Q-Learning
--------------------------------------------------

On peut définir que :math:`V(s)` considère la meilleure action possible. Par opposition, avec
:math:`Q(s, a)` on calcule une valeur pour chaque action, qu'elle soit la meilleure ou non.

1. Définition de base

        .. math::

           Q(s, a) = R(s, a) + \gamma \underset {s'} {\sum} P(s, a, s')V(s')


On constate que l'équation correspond à ce qui est contenu entre les parenthèses dans l'équation
de Bellman.

2. Définition de l'équation en mode récursif (avec :math:`V(s')` remplacer par :math:`Q(s', a')`)

        .. math::

           Q(s, a) = R(s, a) + \gamma \underset {s'} {\sum} \left (P(s, a, s') \underset {a'} {max} Q(s', a') \right)

Différence temporelle
=====================

    :Définissions: 

                * :math:`Q_{t-1} (s, a)` - Avant : C'est l'état précédent de l'action

                * :math:`Q_t (s, a)` - Après : C'est le nouvel état de l'action

                * :math:`TD_t (a, s)` - Différence temporelle : C'est l'apport d'information pour 
                  une action entre Après et Avant.

                * :math:`\alpha` - Alpha : c'est un coefficient multiplicateur pour :math:`TD_t (a, s)`
                  ce coefficient est compris entre O et 1. La nouvelle valeur obtenue, sera ajouté à
                  :math:`Q_{t-1} (s, a)` pour devenir le nouveau :math:`Q_t (s, a)`.

                  **Attention** : 

                        * Pour :math:`\alpha = 0`, on aura :math:`Q_t (s, a) = Q_{t-1} (s, a)`. L'IA
                          n'apprendra donc rien.

                        * Pour :math:`\alpha = 1`, on aura :math:`Q_t (s, a) = R(s,a) + \gamma \underset {a'} {max} Q(s', a')`.
                          L'IA prendra donc toujours la valeur de la nouvelle action, y compris si 
                          cette action est erronée (comportement aléatoire).

                  La valeur de :math:`\alpha` doit donc être réajuster pour que la 
                  différence temporelle soit égale à :math:`0`.


Calcul de la Différence temporelle
----------------------------------

    .. math::

       TD_t (a, s) = \underset {après} {R(s,a) + \gamma \underset {a'} {max} Q(s', a')} - \underset {avant} {Q_{t-1} (s, a)}

Calcul de la Qualité d'une action avec la correction de la différence temporelle
--------------------------------------------------------------------------------

Version condensée :

    .. math::

      Q_t (s, a) = Q_{t-1}(s, a) + \alpha TD_t (a, s)

Version étendue, avec :math:`TD_t (a, s)` remplacée par son expression :

    .. math::
       
       Q_t (s, a) = Q_{t-1}(s, a) + \alpha \left (R(s,a) + \gamma \underset {a'} {max} Q(s', a') - Q_{t-1} (s, a) \right)

--------------------------------
Artificial Neural Networks (ANN)
--------------------------------

    :Liens_Web:
            * http://yann.lecun.com/exdb/publis/pdf/lecun-98d.pdf
                Document traitant de l'importance de normaliser l'échelle des données d'entrée des neurones

.. todo::

   * dans l'annexe, revoir la vidéo "Le Neurone"

   * Faire le schéma d'un neurone (voir la vidéo à 14m23) en ajoutant les termes : Synapses, poid et
     fonction d'activation

####

------------
scikit-learn
------------

  :Liens_Web:
      * http://scikitlearn/stable/documentation

Installer toute la suite scientifique (avec scikit-learn)
=========================================================

    .. code:: shell

        pip install numpy scipy matplotlib ipython scikit-learn pandas pillow

        # pour pouvoir utiliser les codes du livre "Machine Learning avec scikit-learn"
        pip install mglearn

        # Pour pouvoir utiliser jupyter
        pip install jupyter

        ## Pour lancer jupyter
        jupyter notebook

Import systèmatique pour tout les code
======================================

  .. code:: python

        import numpy as np
        import matplotlib.pyplot as plt
        import pandas as pd
        import mglearn
        from IPython.display import display

####

Apprentissage supervisé
=======================

  :L'aprentissage supervisé:
      Il est utiliser lorsque nous voulons prédire une certaine sortie à partir d'une entrée connue
      et que nous connaissons des paires d'entrée/sortie. Ces paires d'entrée/sortie constitue le 
      jeu d'apprentissage.

      La classification et la régression sont les deux types majeurs de problèmes de 
      l'apprentissage supperviser.

  :Classification:
      Dans le cas de la classification, le but est de prédire une étiquette de classe, qui est un
      choixpossible parmi une liste de possibilités. ::

        ex:
        prédire la variété d'un iris en fonction de ces carractéristique (taille des pétals, forme,
        etc...)

      On distingue parfois de type de classification :
        * La classification binaire, dans laquelle le problème comporte exactement deux classes.
        * La classification multiclasse, dans laquelle il y a plus de deux classes.

  :Régression:
      Dans le cas de tâches dite de régression, le but est de prédire une valeur continue, c'est à
      dire un nombre en virgule flottante en termes de programmation, ou un nombre réel en termes
      de mathématiques. ::

        ex:
        Prédire un salaire annuel en fonction de l'éducation, de l'âge, du sexe et du lieu de vie.

Algorithms
==========

Les k plus proches voisins
--------------------------