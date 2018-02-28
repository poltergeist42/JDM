==========
PowerShell
==========

Commandes utiles
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
            
    #. Obtenir la liste de toutes les blibliothèques d'aide dans PowerShell ::
    
        help about
        
    #. Obtenir de l'aide sur le formatage et l'utilisation des commentaires

        :Liens_Web:
            * https://msdn.microsoft.com/en-us/library/aa965353%28VS.85%29.aspx?f=255&MSPPError=-2147217396

        * Command powershell ::
    
            help about_comment_based
            
    #. Obtenir de l'aide sur les méthodes ou les propriétés d'un objet ".net"
    
        #. Identifier le type (TypeName) de l'objet avec Get-Member
        
            ::
            
                > $a = ""
                > $a | gm
                
                    TypeName : System.String
                    
        #. Rechercher dans Google le TypeName identifier et aller sur la page 
           Microsoft MSDN correspondant a la classe de l'objet
        
            ::
            
                Recherche : System.String
                
                Résultat :
                
                    String classe (System) - MSDN - Microsoft
                    https://msdn.microsoft.com/fr-fr/library/system.string(v=vs.110).aspx

        #. Séléctionner dans le menu de gauche la rubrique désirée (Constructeur, Méthode,
           Propriétés)
            
Activer / Désactiver le mode débogage
-------------------------------------

    #. activer le mode débogage ::
        
            set-psdebug -trace 2
    
    #. Désactiver le mode débogage ::
        
            set-psdebug -trace 0
            
----------------------------------------------------------

Slicing
=======
    
    ::
    
        $a = "test.txt"
        $a.Substring(0, $a.length -4)
        > test
        $a.Substring(2, $a.length -4)
        > st.t
        $a.Substring($a.length -4)
        > .txt
        
----------------------------------------------------------

Windows PowerShell Integrated Scripting Environment (ISE)
---------------------------------------------------------

    #. Pour lancer PowerShell ISE depuis la console ::
    
        PS c:\ISE

----------------------------------------------------------
            
Autoriser l’exécution des script
--------------------------------

        ::
        
            set-ExecutionPolicy
            
----------------------------------------------------------

Lancer un script depuis la console powershell
---------------------------------------------

    ::
    
        PS C:\. .\[mon_script].ps1
            # Ne pas oublier le premier "."

----------------------------------------------------------
            
Connaître toutes les méthodes d'un objet
----------------------------------------

    ::
    
        [Objet_ou_command] | get-member (ou gm)
            # exemple pour une variable : $v_a | get-member

----------------------------------------------------------

Séléctionner une commande depuis une fenêtre graphique
------------------------------------------------------

    ::
    
        Show-Command

----------------------------------------------------------

Créer des variables en PowerShell sous forme de tableau
=======================================================

:Liens_Web:
    * http://gmergit.blogspot.fr/2011/11/recemment-jai-eu-besoin-de-creer-des.html

----------------------------------------------------------

Les Tableau
===========

    #. Les Tableau fixe
        Ces tableau ne permettent pas d'ajouter ou de supprimer des données ::
        
            PS C:\> $monTableau = @(1, 'a')
            PS C:\> $monTableau
            1
            a
            PS C:\> $monTableau.Add('z')
            Exception lors de l'appel de « Add » avec « 1 » argument(s) : « La collection était d'une taille fixe. »
            Au caractère Ligne:1 : 1
            + $monTableau.Add('z')
            + ~~~~~~~~~~~~~~~~~~~~
                + CategoryInfo          : NotSpecified: (:) [], MethodInvocationException
                + FullyQualifiedErrorId : NotSupportedException

                
    #. Les Tableau dynamiques
        Ces tableau permettent d'ajouter ou de supprimer des éléments ::
        
            PS C:\> [System.Collections.ArrayList]$monTableau = @(1, 'a')
            PS C:\> $monTableau
            1
            a
            PS C:\> $monTableau.Add('Z')
            2
            PS C:\> $monTableau
            1
            a
            Z
            PS C:\>

----------------------------------------------------------
            
Caractère spécifiques
=====================

    #. Caractère échappement
    
        Le caractère d’échappement est le "`" (accent grave seul [ALT_GR-7])
            * Placé en fin de ligne il permet de ligne, il sert de continuation pour aller
              à la ligne ::
              
                $Reg = get-wmiobject -Namespace Root\Default -computerName `
                       $Comptuer -List | where-object `
                       {$_.Name -eq "StdRegProv"}
                       
           * Placé avant une variable elle sera interprétée comme une chaine de caractère ::
           
                ps:> $v_maVariable = "test"
                
                ps:> write-host "affichage de la variable : $v_maVariable"
                ps:> affichage de la variable : test
                
                ps:> write-host "affichage de la variable : `$v_maVariable"
                ps:> affichage de la variable : $v_maVariable

            * Placé devant un caractère, il sera interpréter comme une commande ::
            
                ps:> $v_maVariable = "test"
                ps:> write-host "blabla`t$v_maVariable"
                ps:> blabla    test
                
                
----------------------------------------------------------

Déclarer une variable
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
    :$Error:    contient les objets d'erreur de la session PowerShell en cours

Ecrire un bloc de texte sur plusieur ligne dans une variable (le here-string)
-----------------------------------------------------------------------------
    
        Pour écrire un bloc de texte sur plusieur ligne dans une variable, il faut
        entourer le bloc avec @' ... '@ ou @" ... "@. ::
        
            Simples cotes
            PS C:\> $myvar = @'
            >> blabla ...
            >> Je s'appel groot !
            >> etc ...
            >> '@
            
            Doubles cotes :
            PS C:\> $myvar = @"
            >> blabla ...
            >> Je s'appel groot !
            >> etc ...
            >> "@
            
        **Rappel** : Les simples cotes ne permettent pas d'interpréter les variables
        qu'elles contiennent alors que les double le permettent.
    
----------------------------------------------------------

Equivalent du print (ou du echo)
================================

    #. Methode classique avec la commande 'write-host'
        Dans cette commande, les simples cotes ne permettent pas d’interpréter de
        variable. L'utilisation des doubles cotes permet l'interpretation de variable ou
        d'objet ::
    
            PS C:\Users\polter> $valeur = 2
            PS C:\Users\polter> write-host '$valeur'
            $valeur
            PS C:\Users\polter> write-host "$valeur"
            2

    #. Méthode 'plus propre' avec l'option 'format' (-f)
    
        Avec cette méthode on utilise les doubles cotes pour encadrer le texte, les
        accolades avec un numéro d'index a l’intérieur (commençant a 0). Les variables sont
        placées a l’extérieur du bloc (après le '-f') et séparées par des virgules ::
        
            PS C:\Users\polter> $valeur = 2
            PS C:\Users\polter> $valeur2 = 2
            PS C:\Users\polter> "{0} + {1} = {2}" -f $valeur, $valeur2, ($valeur + $valeur2)
            2 + 2 = 4
            
----------------------------------------------------------

Renvoyer la sortie d'une commande vers une fenêtre graphique
============================================================

    ::
    
        PS C:\Users\polter> [commande] | Out-GridView
            # La fenêtre qui apparait permet alors d'appliquer des filtres en direct
            
        ex :
        
        PS C:\Users\polter> get-cliditem | Out-GridView

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
            
----------------------------------------------------------

Admisitration Exchange
======================

    #. Page d'information pour toutes les versions d'exchange
    
        * https://technet.microsoft.com/en-us/library/mt587043(v=exchg.150).aspx
    
    #. Exchange Online cmdlets
    
        * https://technet.microsoft.com/EN-US/library/jj200780(v=exchg.160).aspx
    
    #. Exchange Online Protection cmdlets
    
        * https://technet.microsoft.com/EN-US/library/dn621038(v=exchg.160).aspx
        
    #. Office 365 Security & Compliance Center PowerShell
    
        * https://technet.microsoft.com/en-us/library/mt587091(v=exchg.160).aspx
        
    #. Exchange 2016 cmdlets
    
        * https://technet.microsoft.com/EN-US/library/bb124413(v=exchg.160).aspx
        
    #. Exchange 2013 cmdlets
    
        * https://technet.microsoft.com/EN-US/library/bb124413(v=exchg.150).aspx
        
    #. Exchange 2010 Cmdlets
    
        * https://technet.microsoft.com/en-us/library/bb124413(v=exchg.141).aspx
        
----------------------------------------------------------

Automatisation de Windows et de Windows Server avec Windows PowerShell
======================================================================

:Liens_Web:
    * https://technet.microsoft.com/fr-fr/library/dn249523(v=wps.630).aspx

    #. DHCP Server Cmdlets
        * https://technet.microsoft.com/en-us/library/jj590751(v=wps.620).aspx
    
----------------------------------------------------------
    
stocker un chemin puis y retourné
=================================

    #. Pour stocker le repertoire de travail courant ::
    
        Push-Location
        
    #. Pour retourner dans le repertoire de travail stocker précédement ::
    
        Pop-Location
        
----------------------------------------------------------
        
Tester si un chemin exist
=========================

    ::

        Test-Path [chemin_a_tester]
        
        ex :
        
        PS C:\> Test-Path c:\test
        False
        
----------------------------------------------------------
        
Créer des interfaces graphiques
===============================
    
    #. Avec WindowsForm
    
        :Liens_Web:
            * https://justanitblog.wordpress.com/2016/01/28/powershell-creation-dune-interface-graphique/
               # un example windowsForm et WPF
               
    #. Avec WPF (en XAML avec visual studio)


        :Liens_Web:
            * https://www.supinfo.com/articles/single/1933-interface-graphique-xaml-script-powershell
                # une astuce pour ne pas avoir à ecrire le code XAML
                
----------------------------------------------------------

WmiObject
=========

Conaitre les iformations de tous les medias
-------------------------------------------
    ::

        ## Pour obtenir les infos de tous les médias
        Get-WmiObject Win32_LogicalDisk -comp "localhost" | select -Property * | fl

        ## Pour obtenir les infos d'un média en particulier (ex : le disque dur C:
        Get-WmiObject Win32_LogicalDisk -comp "localhost" | where {$_.Name -like "C:"} | select -Property * | fl
        
Connaitre la clef de licence de Windows
---------------------------------------
    ::
    
        (Get-WmiObject -query ‘select * from SoftwareLicensingService’).OA3xOriginalProductKey
        
Connaitre les information du BIOS
---------------------------------
    ::
    
        Get-WmiObject win32_bios | select *