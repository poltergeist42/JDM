======
KRBTGT
======

.. index::
   single: KRBTGT
   single: SysAdmin; KRBTGT

.. contents::
    :depth: 3
    :backlinks: top

####

----------
Descrition
----------

:Liens_Web:
    * `Krbtgt`_

.. _`Krbtgt`:https://neoconsultin.io/krbtgt/

Krbtgt est un compte critique d’infrastructure dans la sécurité Active Directory. Ce compte est un
built-in présent dans Active Directory.

Ce compte est très important et très stratégique puisque le
Hash de son mot de passe est utilisé pour crypter/chiffré et signer tous les tickets Kerberos.

####

------------------------------------------
Réinitialisation du mot de passe de KRBTGT
------------------------------------------

:Liens_Web:
    * `réinitialiser le mot de passe krbtgt`_
    * `Script - Reset-KRBTGT-Password`_

.. _`réinitialiser le mot de passe krbtgt`: https://www.it-connect.fr/active-directory-comment-reinitialiser-le-mot-de-passe-krbtgt/

.. _`Script - Reset-KRBTGT-Password`: https://github.com/zjorz/Public-AD-Scripts/blob/master/Reset-KrbTgt-Password-For-RWDCs-And-RODCs.ps1

    .. warning:: 
        
        Le compte krbtgt historise ses deux derniers mots de passe. Il est donc important de
        réinitialiser 2 fois le mot de passe.

        La durée maximale d'un ticket Kerberos étant de 10 heures, il faut donc attendre au
        minimum 10 heure entre les 2 réinitialisations. Pour ne pas provoquer de coupure auprès des
        utilisateurs.


####

--------
Weblinks
--------

.. target-notes::