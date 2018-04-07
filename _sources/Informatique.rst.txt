============
Informatique
============

Ce document réuni un ensemble d'informations, Manip et autre tips concernant 
la gestion / Maintenance des postes utilisateur et la gestion maintenance des parcs
informatiques.

####

Cours et connaissances génériques
=================================

    #. Microsoft Azure
    
        * https://experiences.microsoft.fr/formations/azure-lab/
            # Liste de Webinar en français sur l'utilisation et l'administration d'Azure
    
    #. Les Expressions Régulières (RegEx)
    
        Une rubrique spéciale RegEx a été créer dans le journal de manip
        
        * https://poltergeist42.github.io/JDM/Regex.html
    
    #. Microsoft Virtual Academy
    
        Cours en ligne gratuis dispenser par microsoft
        
        * https://mva.microsoft.com/

        
    #. VIM / VI
    
        * http://www.formation-lpi.com/IMG/pdf/103.8-vi.pdf
            # MinMap : Memento des principales commandes ou actions
        
####
        
Matériel
========

Information pour la gestion maintenance des matériel

Vérifier les garantie constructeur
----------------------------------

    #. Garantie Dell
    
        * http://www.dell.com/support/home/fr/fr/frdhs1/products/?app=warranty&c=fr&l=fr&s=dhs
        
    #. Garantie HP

        * http://h20565.www2.hpe.com/hpsc/wc/public/home?lang=fr-fr&cc=fr
        

####
        
Poste de travail
================

Toutes les informations concernant l'utilisation et la maintenance des postes utilisateurs.

Excel
-----

    #. Colorer une ligne sur deux dans un tableau Excel
        
        * http://www.pcastuces.com/pratique/astuces/4180.htm
        
            - La commande à saisir pour calculer une les lignes pair : ::
            
                =MOD(LIGNE() ;2)
                
            - Pour les lignes impair : ::
            
                =NON(MOD(LIGNE() ;2))
        
####
        
SysAdmin
========

Ensemble d'informations relative à l'administration Système


Renouveler un certificats sur Exchange 2010
-------------------------------------------

:Liens_Web:
        *https://www.adminpasbete.fr/renouveler-certificat-exchange-2010-facilement/

PowerShell
----------

    #. Installer le module PowerShell ActiveDirectory sous Windows 10
    
        :Liens_Web:
            * https://blogs.technet.microsoft.com/ashleymcglone/2016/02/26/install-the-active-directory-powershell-module-on-windows-10/
                # Explication par l'auteur du script
                
            * https://gallery.technet.microsoft.com/Install-the-Active-fd32e541
                # Le script lui même
    
    
    #. Identifier les PC qui ne se sont pas connecter au domaine depuis
       au moins 180 Jours : 
       
        ::
       
            import-module ActiveDirectory
            $vdate = (Get-Date).adddays(-180)
            Get-ADComputer -filter {(Enabled -eq "True") -and (LastLogonDate -le $vdate)} -property * | ft LastLogonDate, CN
                # applique un filtre sur les élément qui ne sont pas désactivé et qui ne
                # se sont pas connecter de puis au moins 180 Jours
        
        #. pour ne pas filtrer le résultat et voir toutes les propriété : ::
        
            Get-ADComputer -filter * -property *
                # N.B : Fonctionne aussi avec get-ADUser
            
    #. Identifier les comptes utilisateurs qui ne se sont pas connecter au domaine depuis
       au moins 180 Jours : ::

            import-module ActiveDirectory
            $vdate = (Get-Date).adddays(-180)
            Get-ADuser -filter {(Enabled -eq "True") -and (LastLogonDate -le $vdate)} -property * | ft LastLogonDate, CanonicalName
                # applique un filtre sur les élément qui ne sont pas désactivé et qui ne
                # se sont pas connécter de puis au moins 180 Jours
                
    #. Connaitre la date du dernier démarrage d'un serveur ::
    
            Get-CimInstance -ClassName Win32_OperatingSystem | Select CSName, LastBootUpTime
                # Windows2012 r2 et +
                
            ou :
                
            $LastBootTime = (Get-WmiObject win32_Operatingsystem).LastBootUpTime
            [System.Management.ManagementDateTimeConverter]::ToDateTime($LastBootTime)

    #. Se connecter à Exchange ::
    
            $Credentials = Get-Credential
            $ExSession = New-PSSession –ConfigurationName Microsoft.Exchange –ConnectionUri ‘http://SRV-MAIL.poree.local/PowerShell/?SerializationLevel=Full’ -Credential $Credentials –Authentication Kerberos
            Import-PSSession $ExSession
            ...
            Remove-PSSession $ExSession
            
####
            
Router, Firewall, Proxy
=======================

Sophos
------

    #. Configurer le VPN en SSL
    
        :Liens_Web:
            * https://www.sophos.com/en-us/medialibrary/PDFs/documentation/utm90_Remote_Access_Via_SSL_geng.pdf
            