======================
Composants Spécifiques
======================

Programmation des ATMega
========================

Pour programmer un ATmega (328P ; 2560 etc) on peut utiliser Trois environnement différent :

    :AVR_Studio:    Proposer par Microchip (anciennement Atmel) permet de faire du debug
                    au travers de la sonde JTAG mais n'accepte que
                    les programmateur officiels
                    
    :Arduino:       En utilisant le mode "Arduino as ISP. Ne permet pas de programmer
                    autre chose que du '.ino'
                    
    :AVRDUDE:       Tout en ligne de commande, mais accepte tous les programmateur (même
                    'Arduino as ISP'

ATMega 328p-PU Pinout
---------------------

 .. image:: ./Images/Composants/ATMEGA/ATMEGA328-PU-PINOUT.jpg
     :width: 400 px
     :align: center

Installation du programmateur USBASP sous windows 10
----------------------------------------------------

:Liens_Web:
            * http://zadig.akeo.ie/
                # Le logiciel Zadig permet d'installer des pilotes USB
                # pour plusieurs programmateur différents
                
AVRDUDE
-------

    #. Installation
        
        :Liens_Web:
                    * https://sourceforge.net/projects/winavr/files/
                        # dernière version : 2010-01-20
                        
        **/!\\ Ne pas cocher la case 'ajouter au path' mais ajouter les chemins manuellement**
        
        #. Chemins à ajouter dans le path 
            
            * C:\WinAVR-20100110\bin
            * C:\WinAVR-20100110\utils\bin
                        
    #. Utilisation

        :Liens_Web:
                    * https://skyduino.wordpress.com/2011/12/02/tutoriel-avrdude-en-ligne-de-commande/
    
        #. Téléverser un programme ::
        
            avrdude -c [NOM_DU_PROGRAMATEUR] -p [NOM_DU_MICROCONTROLEUR] -v (mode verbose) -U flash:[r|w|v]:[NOM_DU_HEX_A_TELEVERSER]
            
            ex : avrdude -c usbasp -p m2560 -v -U flash:w:Marlin_witbox_2-510.hex
            
        #. Obtenir la liste des noms des microcontroleurs utilisables ::
        
            avrdude -c [NOM_DU_PROGRAMATEUR]
            
            ex : avrdude -c usbasp
    
        


Magnetomettre : HMC5883L
========================

:liens WEB:
            * http://www.instructables.com/id/Interfacing-Digital-Compass-HMC5883L-with-Raspberr/?ALLSTEPS
                # Instructable (install I2C et test en Python3)
                                                
            * http://think-bowl.com/raspberry-pi/i2c-python-library-3-axis-digital-compass-hmc5883l-with-the-raspberry-pi/
                # Exemple de mise en œuvre + liste des fonctions
                    
            * http://www51.honeywell.com/aero/common/documents/myaerospacecatalog-documents/Defense_Brochures-documents/HMC5883L_3-Axis_Digital_Compass_IC.pdf
                # Datasheet du composant
                                                
            * https://www.sparkfun.com/products/10530
                # fiche produit Sparkfun (arduino)
    
Implantation HMC5883L
---------------------
    
    La sérigraphie est masqué lorsque le magnétomètre est enfiché dans une breadbord.
    L’implantation si dessous est donc présenter en **vue de dessus (donc sérigraphie cachée)**
    
        ::
        
            Haut
                3v3
                DRDY
                SDA
                SCL
                GND
                VCC_+5v
            Bas
    
Installation des librairies quick2wire et i2clibraries
------------------------------------------------------

        #. Préparation :
            Si ce n'est pas déjà fait, il faut installer les outils Python :
            
            ::
            
                sudo apt-get update
                sudo apt-get upgrade
                sudo apt-get install i2c-tools
                sudo apt-get install python3-smbus
                     # Quick2wire.i2c peut aussi être utilisé our l'i2c
                    
                sudo apt-get install python3
                sudo reboot
                    
        #. L'installation et configurations des librairies et outils Quick2wire
            **N.B :** le lignes qui suivent sont copiées telles quelles depuis la page instructables
            
            Se positionner à l'endroit ou l'on veut installer quick2wire
                ::
                
                    git clone https://github.com/quick2wire/quick2wire-python-api.git
                        #get quick2wire from github.com

                        #if don't have git, try "sudo apt-get install git"

                    mv ./quick2wire-python-api ./code
                        # renaming the quick2wire library folder to code for tidiness, 
                        # you can skip this if you prefer keeping it original

                    nano setup.env 
                        # create a setup file, basically to point out where the quick2wire library is
                        # situated for your python
                        # after this line, terminal will enter text editing mode, type in these lines

                    export QUICK2WIRE_API_HOME=~/project/code
                        #change the directory address if different than what i'm using
                        #export PYTHONPATH=$PYTHONPATH:$QUICK2WIRE_API_HOME

                    after that CTRL+X, Y, ENTER to quit, save and overwrite

                    back in terminal mode

                    . ./quick2wire.env 
                        # run the environment setup, run this once every time after reboot,
                        # running twice will append the address directory
                        # for checking, use "env |grep quick2wire",
                        # address shown must be the same with the directory where 
                        # you install your quick2wire library

                    cd code
                        #go into the quick2wire folder, this will be where you put your python code

                    git clone https://bitbucket.org/thinkbowl/i2clibraries.git
                        #getting library files containing functions for i2c devices such as HMC5883L,
                        #ITG-3205, ADXL345 and LCD

                    Now you can shut it down with "sudo shutdown -h now" so that we can do the wiring
                                
Configuration du HMC5883L
-------------------------

        #. la déclinaison terrestre
            Pour pouvoir être le plus précis possible, il faut recalibrer la boussole en tenant compte
            de notre décalage par rapport au pôle magnétique. On appel ça : **"la déclinaison terrestre"**
            Pour cela on à besoin de nos coordonnées (les coordonnées du LAB):
            
                * Longitude :  49° 1'22.48"N
                * Latitude  :   2° 1'50.51"E
            
            se qui donne à la date du 18/08/2015 : 0° 9,24'
                        
                        
####

Motteur Pas à Pas : 28BYJ-48
============================

**N.B :** se PAP doit être piloté par un driver comme le UNL2003

Spécification du PAP
--------------------

    +---------------------------------------+----------------+
    | angle par pas (moteur)                |  5.625°        |
    +---------------------------------------+----------------+
    | Nbe de pas / tours (moteur)           | 64 (360/5.625) |
    +---------------------------------------+----------------+
    | ratio (démultiplicateur)              | 1/64           |
    +---------------------------------------+----------------+
    | angle par pas (en sortie d’arbre)     | 0.087890625°   |
    +---------------------------------------+----------------+
    | Nbe de pas / tour (en sortie d'arbre) | 4096           |
    +---------------------------------------+----------------+

Correspondance entre le driver et les GPIO
------------------------------------------
    
        +------------+-------------------------+
        | BCM (GPIO) | Sérigraphie sur UNL2003 |
        +============+=========================+
        |  GPIO17    |           N1            |
        +------------+-------------------------+
        |  GPIO18    |           N2            |
        +------------+-------------------------+
        |  GPIO27    |           N3            |
        +------------+-------------------------+
        |  GPIO22    |           N4            |
        +------------+-------------------------+
        
Phases
------
        +-----------------+---+---+---+---+---+---+---+----+
        |                 | ==> CW Direction (1-2 Phase )  |
        +-----------------+---+---+---+---+---+---+---+----+
        | lead Wire color | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8  |
        +-----------------+---+---+---+---+---+---+---+----+
        | 4 orange        | x | x |   |   |   |   |   | x  |
        +-----------------+---+---+---+---+---+---+---+----+
        | 3 yelow         |   | x | x | x |   |   |   |    |
        +-----------------+---+---+---+---+---+---+---+----+
        | 2 pink          |   |   |   | x | x | x |   |    |
        +-----------------+---+---+---+---+---+---+---+----+
        | 1 blue          |   |   |   |   |   | x | x | x  |
        +-----------------+---+---+---+---+---+---+---+----+
            
        **N.B :** les 8 phases donnent 1 tour complet sur le moteur,
            soit 1/64 de tour en sortie d'arbre.
            
Organisation des phases en python3
----------------------------------
        ::
        
            # Séquence de sortie
            ndp = 8
            phase = list(range(ndp))
            phase[0] = [1,0,0,0]
            phase[1] = [1,1,0,0]
            phase[2] = [0,1,0,0]
            phase[3] = [0,1,1,0]
            phase[4] = [0,0,1,0]
            phase[5] = [0,0,1,1]
            phase[6] = [0,0,0,1]
            phase[7] = [1,0,0,1]
                    
        **N.B :** la liste contenu dans chaque phase, correspond à l'état
            (1 = Hight = True ; 0 = Low = False) à appliquer sur le broches du GPIO
                
            ::
        
                ex  : phase[0] = [1,0,0,0]
                    --> GPIO17 = 1
                    --> GPIO18 = 0
                    --> GPIO27 = 0
                    --> GPIO22 = 0

####

Picamera
========

:liens WEB:
        * http://www.framboise314.fr/picamera-pour-piloter-integralement-la-camera-de-votre-raspberry-pi-en-python/
        * http://picamera.readthedocs.org/en/release-1.0/quickstart.html
            # Quick Start
                                    
        * http://picamera.readthedocs.org/en/release-1.0/recipes1.html
            # CookBook
                
Activation du module caméra sur le RPi
--------------------------------------

    #. se connecter au module de configuration
        ::
        
            * sudo raspi-config
            
    #.* faire la séquence suivante
        ::
        
            "5 Enable Camera" -> [Entré]
                    --> <Enable> -> [Entré]
                    --> <Finish> -> [Entré]
                    --> <Oui> -> [Entré]
                    
installation de la camera
-------------------------

        #.   Insérer la limande dans le ports situé au niveau du port HDMI.
        
            **N.B :** la partie métallique doit être en direction du port HDMI

                    
Instalation de la librairie PiCamera
------------------------------------

        #. Faire les mises à jour système de rigueur puis
            ::
            
                sudo apt-get install python3-picamera
            
utilisation avec python
-----------------------
            ::
            
                import picamera
                
####

Capteur ultrason : HC-SR04
==========================

:Liens Web:
            * https://youtu.be/xACy8l3LsXI
            * http://www.modmypi.com/blog/hc-sr04-ultrasonic-range-sensor-on-the-raspberry-pi
             
Vocabulaire et définissions pour le HC-SR04
-------------------------------------------

    :Trig:
        En Sortie (haut-parleur - Trig)
            # 1 impulsion est égale a 10us (0.00001)
                    
    :Echo:
        En Entrée (Micro - Echo)
        
            # Attention les entrée du RPi étant en 3.3v,
            il faut faire un pont diviseur entre la broche
            "Echo" et le GND pour pouvoir se brancher
            sur le RPi
                
    :Vitesse du son:
        Le son se déplace à une vitesse d'environ 343 m/s (à température ambiante de 20°),
        soit environ 34300 cm/s
            
            
                
    :Distance:
        D = 17150 x time
            # 17150 correspond a la vitesse du son / 2 (34300/2).
            On divise par 2 car seule la distance en l'obstacle et le mur nous intéresse
            et non la distance total parcourue par l'onde radio.
            
Spécification du HC-SR04
------------------------

    :Alimentation:
        5 V
        
    :porté:
        2 cm à 500 cm
        
    :Résolution:
        0.3 cm
        
    :Fréquence:
        40 kHz

####

Captheur de Méthane : MQ4
=========================

:Liens_Web:
            * https://www.pololu.com/file/0J311/MQ4.pdf
                # DATASHEET du composant

            * https://www.aliexpress.com/item/Free-shipping-MQ-4-gas-methane-sensor-module-MQ4-for-arduino/32561647140.html?spm=a2g0s.9042311.0.0.27424c4dETPH08
                # Ref Aliexpress

            * https://www.sparkfun.com/datasheets/Sensors/Biometric/MQ-4.pdf
                # Une autre version de la DATASHHET (avec des dessins plus gros et schéma plus détaillés)

:INFOS:
        * Les capteurs de Type 'MQx' ont besoin d'être alimentés en continue

        * Les capteurs de Type 'MQx' doivent nécessite un délais de minimum 48H pour fournir
          des informations fiables

        * Toutes les valeurs données ici concerne uniquement le Méthane. Pour tout autre gaze 
          détecté par le MQ4, il faut se reporter à la documentation

:/attention\\:
        * Sur la version PCB la résistance Rl, qui devrait être une résistance ajustable de 10 à 47k,
          est une résistance fixe de 1K. D'après la documentation, cette résistance devrait être
          étalonnée pour 5000 ppm soit à peut près 20K

####

Liste des gazes pouvant être détecter par le MQ4
================================================

    * GPL

    * Méthane (CH4)

    * Hydrogène (H2)

    * Monoxyde de Carbone (CO)

    * Alcool

    * Fumé de cigarette

####

Définition des constantes et valeurs de références
==================================================

:Liens_Web:
            * https://www.jayconsystems.com/tutorials/gas-sensor-tutorial/
                # Tous les calculs ont été effectuer sellons les calculs de cette page mais sur la courbe CH4

:RS:        C'est la résistance mesurer mesurer par le capteur. Cette valeur est Variable.

:R0:        C'est la résistance du capteur en condition de gaz normal. Cette valeur est Variable.
            Elle doit être calculer. 
