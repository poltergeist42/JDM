======================
Composants Spécifiques
======================

Magnetomettre : HMC5883L
========================

:liens WEB:
            * http://www.instructables.com/id/Interfacing-Digital-Compass-HMC5883L-with-Raspberr/?ALLSTEPS
                # Instructable (install I2C et test en Python3)
                                                
            * http://think-bowl.com/raspberry-pi/i2c-python-library-3-axis-digital-compass-hmc5883l-with-the-raspberry-pi/
                # Exemple de mise en oeuvre + liste des fonctions
                    
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
                    
        #. l'installation et configurations des librairies et outils Quick2wire
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
            de notre décalage par rapport au pole magnétique. On appel ça : **"la déclinaison terrestre"**
            Pour cela on à besoin de nos coordonnées (les coordonnées du LAB):
            
                * Longitude :  49° 1'22.48"N
                * Latitude  :   2° 1'50.51"E
            
            se qui donne à la date du 18/08/2015 : 0° 9,24'
                        
                        
------------------------------------------------------------------------------------------

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
-----------------------------------------
    
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

------------------------------------------------------------------------------------------

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
                
------------------------------------------------------------------------------------------

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
        
            # Attention les entrée du RPi etant en 3.3v,
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