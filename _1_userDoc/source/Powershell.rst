==========
PowerShell
==========

Commandes utilies
=================
Obtenir de l'aide
-----------------

:Liens_Web:
            * https://docs.microsoft.com/fr-fr/powershell/module/microsoft.powershell.utility/?view=powershell-5.1

    #. Obtenir de l'aide depuis le shell ::
    
            get-help [nom_de_la_commande]
            
            ex :
            get-help get-member
            
    #. Les diférents modes de l'aide
    
        * Pour consulter les exemples :: 
        
            get-help Get-Help -examples
            
        * Pour plus d'informations :: 
        
            get-help Get-Help -detailed
            
        * Pour obtenir des informations techniques :: 
            
            get-help Get-Help -full
            
        * Pour l’aide en ligne ::

            get-help Get-Help -online

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
        [Objet_ou_command] | get-member (ou gm)
            # exemple pour une variable : $v_a | get-member

----------------------------------------------------------
            
Caractère spécifiques
=====================

    #. Caractère d'echapement
    
        Le caractère d'échapement est le "`" (accent grave seul [ALT_GR-7])
            * Placé en fin de ligne il permet de ligne, il sert de continuation pour aller
              à la ligne ::
              
                $Reg = get-wmiobject -Namespace Root\Default -computerName `
                       $Comptuer -List | where-object `
                       {$_.Name -eq "StdRegProv"}
                       
           * Placé avant une variable elle sera interprétée comme une chaine de caratère ::
           
                ps:> $v_maVariable = "test"
                
                ps:> write-host "affichage de la variable : $v_maVariable"
                ps:> affichage de la variable : test
                
                ps:> write-host "affichage de la variable : `$v_maVariable"
                ps:> affichage de la variable : $v_maVariable

            * Placé devant un caractère, il serat interpréter comme une commande ::
            
                ps:> $v_maVariable = "test"
                ps:> write-host "blabla`t$v_maVariable"
                ps:> blabla    test
                
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