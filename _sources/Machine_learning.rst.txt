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

    * y - Discount (Réduction): il s'agit du facteur de réduction (compris entre 0 et 1). 
      Plus cette valeur est proche de 0, plus ont s'éloigne du résultat et / ou de la solution.

    * V : La valeur d'un certain état
