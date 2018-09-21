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

            * Si RA=0 : L'IA n'optimisera pas la recherche de solution.

            * Si RA=-0.3 : L'IA optimisera légèrement sa recherche de solution mais aucuns risque
              ne sera pris dans le choix de l'action.

            * Si RA=-0.5 : l'IA optimisera beaucoup sa recherche de solution, mais ne prendra que 
              des risques modérés.

            * Si RA=-2 : l'IA prendra tous les risques possibles pour parvenir à une solution le 
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
                * P - Processus de Décision Markovien (MDP) : Moyenne de la somme des états
                  possibles (s\'). Il s'agit de l'introduction d'un facteur aléatoire dans un 
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

                * Q - Qualité : définit la qualité de l'action à venir :math:`Q(s, a)` par opposition à 'V',
                  qui définit la valeur de l'état :math:`V(s)`.

Définission de l'équation de Bellman en Q-Learning
--------------------------------------------------

On peut définir que :math:`V(s)` considère la meilleure action possible. Par opposition, avec
:math: `Q(s, a)` on calcule une valeur pour chaque action, qu'elle soit la meilleure ou non.

    1. Définition de base

            .. math::

               Q(s, a) = R(s, a) + \gamma \underset {s'} {\sum} P(s, a, s')V(s')


On constate que l'équation correspond à ce qui est contenu entre les parenthèses dans l'équation
de Bellman.

    2. Définition de l'équation en mode récursif (avec :math:`V(s')` remplacer par :math:`Q(s', a')`)

            .. math::

               Q(s, a) = R(s, a) + \gamma \underset {s'} {\sum} \left (P(s, a, s') \underset {a} {max} Q(s', a') \right)

Différence temporelle
=====================

    .. todo::
       * revoir la Vidéo 13

       * Déffinir la Différence temporelle

       * Définir l'équation de Bellman en intégrant la diférence temporelle
