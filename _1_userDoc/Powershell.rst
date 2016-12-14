==========
PowerShell
==========

Commandes utilies
=================

Activer / Desactiver le mode debugage
-------------------------------------

    #. activer le mode debugage ::
        
            set-psdebug -trace 2
    
    #. Desactiver le mode debugage ::
        
            set-psdebug -trace 0
            
----------------------------------------------------------
            
Autoriser l'execution des script
--------------------------------

        ::
        
            set-ExecutionPolicy
            
----------------------------------------------------------
            
Connaitre toutes les methodes d'un objet
========================================

    ::
        [Objet_ou_command] | get-members (ou gm)
            # exemple pour une variable : $v_a | get-members

----------------------------------------------------------

Declarer une variable
=====================

    #. variable typee dynamiquement ::
        
        $maVarible = valeur
        
    #. variable fortement typee ::
    
        [bool] $maVarible = true
        
       N.B : par convention les string se declarent avec des simples cotes ::
    
        $maVarible = 'text'
        
variables spécifiques
---------------------

    :$_:        contient l'objet en cours dans le pipeline
    :$Error:    contient les objets d'erreur de la seesion PowerShell en cours
    
----------------------------------------------------------

Equivalent du print (ou du echo)
================================

    #. Methode classique avec la commande 'write-host'
        Dans cette commande, les simples cotes ne permettent pas d'interpreter de
        variable. L'utilisation des doubles cotes permet l'interpretation de variable ou
        d'objet ::
    
            PS C:\Users\polter> $valeur = 2
            PS C:\Users\polter> write-host '$valeur'
            $valeur
            PS C:\Users\polter> write-host "$valeur"
            2

    #. Methode 'plus propre' avec l'option 'format' (-f)
    
        Avec cette methode on utilise les doubles cotes pour encadrer le texte, les
        accolades avec un numero d'index a l'interieur (commancant a 0). Les variables sont
        placees a l'exterieur du bloc (apres le '-f') et separees par des virgules ::
        
            PS C:\Users\polter> $valeur = 2
            PS C:\Users\polter> $valeur2 = 2
            PS C:\Users\polter> "{0} + {1} = {2}" -f $valeur, $valeur2, ($valeur + $valeur2)
            2 + 2 = 4
            
----------------------------------------------------------

Déclarer une fonction
=====================

    ::
    
        function [nom_de_la_fonction] {
        [command_1]
        [command_2]
        [etc_...]
        }
        
        ex :
        
            function f_maFonction { get-cliditem }