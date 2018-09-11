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

    * s - State (l'état) : Il s'agit de l'état dans lequel l'environnement est.

    * s' : l'état dans le quel on va arriver

    * a - Action : Les actions que peut prendre l'agent

    * R - Reward (Récompense) : Récompense obtenu par l'agent pour rentrez dans un certain état
      (+1, 0 ou -1)

    * :math:`\gamma` (Gamma) - Discount (Réduction): il s'agit du facteur de réduction 
      (compris entre 0 et 1). Plus cette valeur est proche de 0, plus ont s'éloigne du résultat
      et / ou de la solution.

    * V : La valeur d'un certain état

    * P - Processus de Décision Markovien (MDP) : Moyenne de la somme des états possibles (s')

Equation simplifiée
-------------------

Sous cette forme simplifié, l'équation est déterministe. Elle ne tien pas compte des éléments 
aléatoires (`Stochastique <https://fr.wikipedia.org/wiki/Stochastique>`_).

    .. math::

       V(s) = \underset {a} {max}(R(s, a) + \gamma V(s'))

Chaine de Markov et Processus de Décision Markovien (MDP)
=========================================================

    :Liens_Web:
                * https://pdfs.semanticscholar.org/968b/ab782e52faf0f7957ca0f38b9e9078454afe.pdf
                    # Martijn van Otterlo, 2009, Markov Decision Processes: Concepts and Algorithms

                * https://fr.wikipedia.org/wiki/Processus_stochastique
                    # Définition Wikipédia



Equation de Belman augmentée du MDP
-----------------------------------

    * TODO: revoir la vidéo 9.

    .. math::

       V(s) = \underset {a} {max} \left (R(s, a) + \gamma \sum P(s, a, s')V(s') \right)
