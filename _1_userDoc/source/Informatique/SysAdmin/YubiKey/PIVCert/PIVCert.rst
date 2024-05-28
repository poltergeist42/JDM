==========================
YubiKey - PIV - Certificat
==========================

.. index::
   single: PIV - Certificat
   single: YubiKey; PIV - Certificat

.. contents::
    :depth: 3
    :backlinks: top

####

---
PIV
---
    
    .. glossary::

        PIV : Personal Identity Verification

####

-----------
certificats
-----------

    * **Autorité de certification (CA)** : Par défaut, le CA expire au bout de 5 ans.

    * **Certificat utilisateur final** : Par défaut, le certificat utilisateur final expire au bout
      de 1 an.

    * **Renouvellement automatique** : par défaut, Le certificat utilisateur final est renouvelé
      automatiquement 6 semaines avant l'expiration.

      **N.B** : le renouvellement ne pourra être effectué que le poste émettant la demande et
                capable de communiquer avec l'autorité de certification.

      L'autorité de certification n'est pas renouvelé automatiquement. Il est donc important de
      surveiller la date d'expiration.

Préparer l'autorité de certification
====================================

    #. installer le role "Active Directory certificat Services" sur le DC.

            .. image:: images/addADCS.png
               :width: 500 px
               :align: center

    #. Cocher la case "Certification Authority".

        .. image:: images/roleServicesCA.png
           :width: 500 px
           :align: center

    #. cliquer sur **Configure Active Directory Certificate Services on the destination server**

        .. image:: images/ADCStargetServer.png
           :width: 500 px
           :align: center

    #. Renseignez les information d'authentification.

    #. Cochez la case "Certification Authority"

    #. Sélectionner le "Enterprise CA" > "Root CA" > "Create a new private key"

    #. Accepter les paramètres tous les paramètres par défaut puis cliquer sur le boutons
       **configure**.

Créer un modèle de certificat
=============================

    #. exécuté **certtmpl.msc**

    #. Clique droit sur *SmartCard Logon* > **Duplicate Template**

    #. Onglet **Compatibility** :

        * Certification Authority : Sélectionner la compatibilité du serveur CA
        * Certificate recipient : Sélectionner la compatibilité du client avec lla version la plus
          ancienne des poste de travail

    #. Onglet **General** :

        .. image:: images/generalTab.png
           :width: 500 px
           :align: center

    #. Onglet **Request Handling** :

        .. image:: images/tabRequestHandling.png
           :width: 500 px
           :align: center

    #. Onglet **Cryptography**

        .. image:: images/tabCryptography.png
           :width: 500 px
           :align: center

    #. Onglet **Security** : ajouter **utilisateurs du domaine** 

        .. image:: images/tabSecurity.png
           :width: 500 px
           :align: center

Ajouter le modèle de certificat à l'authorité de certification
==============================================================

    #. exécuté **certsrv.msc**

    #. *Certificat Authority* > *<CA name> > *Certificate Templates* > clique droit, *New* >
       **Certificate Template to Issues**

    #. Descendre dans la fenêtre et sélectionner le modèle créé précédemment.

        .. image:: images/selectTemplate.png
           :width: 500 px
           :align: center

            .. important:: 
                
                **Attention**
        
                Le certificat peut metre jusqu'à 8h00 pour ce répliquer au travers de
                l'infrastructure.
        


####

-----------------------
Créer les GPO SmartCard
-----------------------

    #. Créer une nouvelle GPO appelée "Yubikey" et la lier au niveau du domaine.

    #. *Computer* > *Administrative Template* > *Windows Components* > *Smart Card* > 
       *Allow ECC certificates to be used for logon and authentication* > **Enabled**

    #. *Computer* > *Windows Settings* > *Security Settings* > *Local Policies* >
       *Security Options* > *Interactive logon: Smart card logon* > *Define this policy setting* >
       **No Action**

    #. *Computer* > *Windows Settings* > *Security Settings* > *Public Key Policies* >
       *Certificate Services Client - Auto-Enrollment* > *Define this policy setting* >
       *Configuration Model* > **Enabled**

           .. image:: images/gpoAutoEnroll.png
              :width: 500 px
              :align: center

    #. *Computer* > *Windows Settings* > *Security Settings* > *Public Key Policies* >
       *Certificate Services Client - Enrollment Policy* > *Configuration Model* > **Enabled**

        #. *user* > *Windows Settings* > *Security Settings* > *Public Key Policies* >
       *Certificate Services Client - Auto-Enrollment* > *Define this policy setting* >
       *Configuration Model* > **Enabled**

           .. image:: images/gpoAutoEnroll.png
              :width: 500 px
              :align: center

    #. *user* > *Windows Settings* > *Security Settings* > *Public Key Policies* >
       *Certificate Services Client - Enrollment Policy* > *Configuration Model* > **Enabled**

####

-------------------------------------
Ajouter le certificats sur la YubiKey
-------------------------------------

    .. note:: 
        
        **Liens Web**

        * `HOW TO - Use YubiKey To Secure Your Domain Network - Youtube`_
        
.. _`HOW TO - Use YubiKey To Secure Your Domain Network - Youtube`: https://www.youtube.com/watch?v=KsGcSCqs4Ps





    
    .. note:: 
        
        Ouvrir l'invite de commande en tant que autre utilisateur et s'authentifier avec le compte
        souhaiter.
        
        .. code:: Powershell
            :number-lines:
            :force:

             # certreq -enroll [YubiKey_certificat_template_name]
             certreq -enroll YubiKey

####

--------
Weblinks
--------

.. target-notes::