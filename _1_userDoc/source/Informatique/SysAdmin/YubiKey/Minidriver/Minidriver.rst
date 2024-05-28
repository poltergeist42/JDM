==================
YubiKey-Minidriver
==================

.. index::
   single: YubiKey; Minidriver
   single: YubiKey; Minidriver

.. contents::
    :depth: 3
    :backlinks: top

####

--------------------------
Déployer le Driver YubiKey
--------------------------

    .. note:: 
        
        **Liens Web**

        * `YubiKey Minidriver Installation`_
        * `Smart card drivers and tools`_
        
.. _`YubiKey Minidriver Installation`: https://support.yubico.com/hc/en-us/articles/360015654560-Deploying-the-YubiKey-Minidriver-to-Workstations-and-Servers
.. _`Smart card drivers and tools`: https://www.yubico.com/support/download/smart-card-drivers-tools/


Le Minidriver doit être installé sur toutes les machines où la YubiKey sera utilisée comme
carte à puce (smart card) pour y accéder. Cela inclut les serveurs auxquels les utilisateurs se
connectent à distance, ainsi que l'ordinateur de connexion. 

Le Minidriver YubiKey est disponible au téléchargement directement sur le site Web de
Yubico : `Smart card drivers and tools`_.

Information ouverture de session en Bureau à distance
=====================================================

    .. danger:: 
        
        **Attention**

        Pour que l'ouverture de sessions en Bureau à distance fonctionne, il faut que le driver
        YubiKey-Minidriver soit installé avec l'option "INSTALL_LEGACY_NODE" activé sur le serveur
        cible **ET** sur l'ordinateur de connexion.
        
        .. code:: shell
            :number-lines:
            :force:

             msiexec /i YubiKey-Minidriver-4.1.1.210-x64.msi INSTALL_LEGACY_NODE=1 /quiet

        Le déploiement du package avec cette options depuis une GPO nécessite la génération d'un
        fichier de paramétrage séparé.

Générer le fichier de paramètre ".mst" pour le package ".msi"
-------------------------------------------------------------

    .. note:: 
        
        **Liens Web**

        * `Comment ajouter des options à un package MSI déployé par GPO ?`_
        
.. _`Comment ajouter des options à un package MSI déployé par GPO ?`: https://www.it-connect.fr/comment-ajouter-des-options-a-un-package-msi-deploye-par-gpo/#IV_Deployer_un_package_MSI_avec_des_options_par_GPO

    #. Installer Orca en suivante les instructions de l'article it-connect

    #. Ouvrir l'application **Orca** puis cliquer sur *File* > *Open* et séléctionner le 
       package **MSI** YubiKey-Minidriver correspondant à votre architecture.

    #. Créer une nouvelle transformation *Transform* > **New Transform**

        .. image:: images/NewTransform.png
           :width: 500 px
           :align: center

    #. Ouvrir *Tables* > **Property** puis faire un clic droit sur une ligne vierge de la page de
       droite et sélectionner **Add Row**.

        .. image:: images/addRow.png
           :width: 500 px
           :align: center

    # Ajouter le couple clé/valeur suivant :

        * **Property** : INSTALL_LEGACY_NODE
        * **Value** : 1
    
        .. image:: images/mstProperty.png
           :width: 500 px
           :align: center

        .. image:: images/mstValue.png
           :width: 500 px
           :align: center

        
        * La nouvelle propriété sera ainsi ajoutée aux autres.

        .. image:: images/mstProps.png
           :width: 500 px
           :align: center

    #. Générer et sauvegarder la transformation dans un fichier ".mst" : Menu *Transform* > 
       **Generate Transform**

        .. image:: images/mstGenrate.png
           :width: 500 px
           :align: center


        * sauvegarder le fichier avec un nom significatif.

        .. image:: images/mstFileName.png
           :width: 500 px
           :align: center



Déployer Minidriver par GPO
===========================

Les GPO créés pour le déploiement du Minidriver sont de type **Stratégie Ordinateur**

    .. danger:: 
        
        **Attention**

        Le Minidriver est disponible pour les architecture en 32bits et 64bits. Le déploiement sur
        un serveur Bureau à distance nécessite un paramétrage spécifique.

        Il est donc possible que la création de quatre GPO soient nécessaires.

    
    #. Télécharger le package **MSI** YubiKey-Minidriver correspondant à votre architecture.

    #. Créer un dossier de partage pour stocker les packages **MSI** ainsi que les fichiers ".mst".
       Ce dossier devras être accessible depuis tous les postes ou serveurs la YubiKey sera
       utilisée. il est donc important d'accorder les droits de **lecture et d'écriture** aux
       **utilisateurs du domaine** ainsi qu'aux **ordinateurs du domaine**.

           .. note:: 
               
               **Ordinateurs du domains**
       
                .. image:: images/sharedFolder_propscomputer.png
                    :width: 500 px
                    :align: center

               **Utilisateurs du domains**

                   .. image:: images/sharedFolder_propsUsers.png
                      :width: 500 px
                      :align: center

    #. Dans l'outil **Gestion de stratégie de groupe**, créer une nouvelle stratégie de groupe de
       type **Stratégie Ordinateur** au niveau de **l'Objet de stratégie de groupe**. Cette GPO
       pourra être liée ultérieurement.

           .. note:: 
               
               **GPO ordinateur x64**
       
                .. image:: images/newGPO.png
                    :width: 500 px
                    :align: center
    
    .. note:: 
        
        **Information**

        Les prochaines actions doivent être effectués à l'intérieur de la stratégie elle-même.

    #. Dans *Configurations ordinateur* > *Paramètres du logiciel* > **Installation de logiciel**,
       faire un clic droit dans la fenêtre de droite et sélectionner **Nouveau** > **Package**.

        .. note:: 
            
            **Installation de logiciel**
    
            .. image:: images/newSoft.png
                :width: 500 px
                :align: center
    
    #. Sélectionner le package **MSI** directement depuis son emplacement réseau.

        .. note:: 
            
            **Sélection du package MSI**
    
            .. image:: images/packageSelection.png
                :width: 500 px
                :align: center

    #. Déploiement du logiciel

        **Déploiement du logiciel sans le mode "Legacy"**

        .. note:: 
        
            #. Conserver les paramètres par défaut et cliquer sur **OK**.

                .. note:: 
                    
                    **Déploiement du logiciel**
            
                    .. image:: images/softDeployement.png
                        :width: 500 px
                        :align: center

        **Déploiement du logiciel avec le mode "Legacy"**

        .. note:: 
            
            #. Sélectionner le type **"Avancé"**
    
                .. image:: images/softDeployementAdvanced.png
                    :width: 500 px
                    :align: center

            #. Dans l'onglet **Modification** de la fenêtre Propriétés, ajouter le fichier ".mst"

                .. image:: images/softDeployementAdvancedAddMst.png
                   :width: 500 px
                   :align: center
            

        .. note:: 
            
            **Fenêtre de résumer**

            Le résumé du déploiement du logiciel est affiché dans la fenêtre de droite. Etat du
            déploiement apparaît comme "attribué" dans la fenêtre de résumer quelques soit le type
            de déploiement choisie.

                .. image:: images/softSummary.png
                    :width: 500 px
                    :align: center

Configuration optionnelle
-------------------------

Il est possible de créer ou de modifier des entrées de Registre pour configurer le comportement du
Minidriver et de la YubiKey.

    #. Dans *Configurations ordinateur* > *Préférences* > **Registre**, faire un clic droit dans la
           fenêtre de droite et sélectionner **Nouveau** > **Element Registre**.

        .. note:: 
            
            **Nouvelle entrée de Registre**
    
            .. image:: images/newReg.png
                :width: 500 px
                :align: center

        .. note:: 
            
            **Information**
    
            Les informations de cette section sont une simple traduction des informations
            disponibles sur `YubiKey Minidriver Installation`_
    

    :Setting PIN Unblock Code (PUK):

        Lorsqu'une YubiKey est utilisée avec le YubiKey Minidriver pour la première fois, le YubiKey
        Minidriver vérifie pour s'assurer que les valeurs par défaut ne sont pas utilisées pour la
        clé de gestion et le code de déblocage du NIP (PUK). Si les valeurs par défaut sont
        utilisées, le YubiKey Minidriver mettra à niveau la clé de gestion vers une valeur protégée
        et bloquera le PUK. Un PUK bloqué empêchera la fonction de déblocage du NIP d'être active.

        Pour empêcher le blocage du PUK, le registre local doit être configuré avant la
        configuration des clés.
        
            * Clé : **HKLM\\Software\\Yubico\\ykmd**
            * Valeur : **BlockPUKOnMGMUpgrade** (DWORD) - 0 désactive la fonction de blocage du PUK,
              toute autre valeur l'active

        Le Minidriver YubiKey prend en charge le déverrouillage d'un PIN bloqué à l'aide de
        l'interface utilisateur Windows intégrée. Pour activer cette fonction, vous devez autoriser
        l'affichage de l'écran de déverrouillage intégré au moment de la connexion dans la stratégie
        de groupe Windows. Ce paramètre de configuration se trouve dans :
        
            * Configuration de l'ordinateur* > *Modèles d'administration* > *Composants Windows* > **Carte à puce**

        Pour que le PUK reste débloqué, YubiKey Manager ou l'outil Yubico PIV doit être utilisé pour
        définir un PUK non par défaut avant d'utiliser l'interface Windows pour charger ou accéder
        aux certificats stockés sur la YubiKey. Lorsque le Minidriver accède pour la première fois à
        la YubiKey, il vérifie si le PUK est défini sur la valeur par défaut - pour les PUK avec des
        valeurs fournies par l'utilisateur, cela entraînera la décrémentation du compteur de
        tentatives d'une unité. Cela peut être réinitialisé en saisissant le PUK correct via
        l'interface Windows, mais nécessite de changer le PIN PIV.

        La définition du PUK peut être effectuée dans **YubiKey Manager** en accédant à :
        
            *Applications* > *PIV* > *Configurer les PIN* > **Changer le PUK**.


    :Setting Touch Policy:

        La YubiKey peut être configurée pour exiger un contact physique afin de confirmer toute
        opération cryptographique.
        
        C'est une fonctionnalité optionnelle pour augmenter la sécurité, garantissant que toute
        opération d'authentification doit être effectuée en personne. Le Minidriver YubiKey définit
        la politique de contact lorsqu'une clé est importée ou générée pour la première fois. Une
        fois définie pour une clé sur la YubiKey, les politiques ne peuvent pas être modifiées.

        Par défaut, la politique de contact pour les clés importées/générées via le minidriver est
        créée avec le paramètre par défaut de la politique de contact désactivée.

        Pour modifier le comportement de la politique, le registre doit être configuré avant la
        configuration des clés, soit sur la station d'inscription des clés ou déployé sur toutes les
        machines à l'aide d'Objets de stratégie de groupe.

            * Clé : **HKLM\\Software\\Yubico\\ykmd**
            * Valeur : **NewKeyTouchPolicy** (DWORD) - définit la politique de contact sur les
              nouvelles clés générées/importées via le minidriver.
              
              Les valeurs acceptées sont :
        
                * **1 <Jamais>** - Politique par défaut de ne jamais exiger un contact utilisateur.
                * **2 <Toujours>** - La politique est définie pour exiger un contact utilisateur
                  afin de confirmer chaque opération cryptographique. Yubico ne recommande pas
                  d'utiliser ce paramètre, car certains services Windows, comme la connexion,
                  peuvent nécessiter plusieurs opérations cryptographiques en un court laps de temps.

                * **3 <Mise en cache>** - La politique est définie pour exiger un contact physique
                  une fois, puis autoriser les opérations cryptographiques dans une petite fenêtre
                  de temps par la suite. Pour utiliser l'option de contact physique avec la
                  connexion Windows Smart Card, cette option est requise.

        .. important:: 
            
            **Attention**
    
            En raison des limitations du système d'exploitation, **il n'y a aucune invite visuelle à
            l'écran lorsqu'un contact est requis** dans ce scénario (la spécification du minidriver
            de Microsoft sur laquelle ykmd est basé n'a aucune notion d'exigence de contact).

            Par conséquent vous risquez d'avoir un Time out qui retourne une **erreur
            d'authentification Kerberos**.

    
    :Logging Minidriver Behavior:

        En cas d'erreurs lors de l'utilisation de la YubiKey en tant que carte à puce PIV avec le
        YubiKey Minidriver, la journalisation des erreurs peut être activée sur l'ordinateur local à
        l'aide du registre. Une fois activée, les fichiers journaux seront créés par processus en
        cours d'exécution dans C:\Logs. 

            * Clé : **HKLM\\Software\\Yubico\\ykmd**
            * Valeur : **DebugOn** (DWORD) - 1 active la journalisation des erreurs.
    
####

-----------------------------------------
Vérification du déploiement du Minidriver
-----------------------------------------


    .. note:: 
        
        Il est possible de vérifier le déploiement du Minidriver en exécutant la commande suivante :

        **N.B** : Il faut être connecté en tant qu'administrateur pour exécuter cette commande.
        
        .. code:: Powershell
            :number-lines:
            :force:

             Get-WindowsDriver -Online | where {($_.ProviderName -like "Yubico") -and ($_.ClassName -like "SmartCard") -and ($_.Version -like "*")} | select ProviderName,ClassName,Version




####

--------
Weblinks
--------

.. target-notes::