=========
Raspberry
=========

RPi utilisés
============

Model 2 (ID-FIX)
----------------

    ::

      NAME                  : RPi2pierre
      MAC address ETH       : b8:27:eb:65:13:5a
      IP                    : 172.16.32.253
      netmask               : 255.255.255.0

      MAC Address WLAN      : 08:86:3b:6b:4d:58
                            : eth.addr == 08:86:3b:6b:4d:58
                                         # filtre a appliquer dans Wireshark

####

RPI ROV
-------
    ::

      NAME                  : rpiRov
      MAC address ETH       : b8:27:eb:e0:4b:93
      IP                    : 
      netmask               : 

      MAC Address WLAN      : 
                            : eth.addr == d8:eb:97:1c:3e:b4
                                        # filtre a appliquer dans Wireshark

####

Accéder au fichier de configuration du RPI
==========================================
    ::
    
        sudo raspi-config

####

Connaître la configuration matériel du RPI
==========================================

  :CPU:                 * cat /proc/cpuinfo


####

pour passer la langue et le clavier en français
===============================================

:liens WEB:
            * http://the-raspberry.com/changer-langue-raspberry-pi
            * https://www.raspberrypi.org/forums/viewtopic.php?f=65&t=21700

        #.  Changer la langue depuis l'interface de configuration du Pi
        
            * se connecter a l'interface de configuration
                + sudo raspi-config
            
            * Ouvrir le menu "5 Internalisation Options"
            * Ouvrir "I1 Change Locale"
            * Si une langue comme **"en_GB.UTF-8 UTF-8"** est cochée, décochez-la
              en appuyant sur **"Espace"**
            * Cochez la langue **"fr_FR.UTF-8 UTF-8**"
            * Sélectionner **"OK"** puis valider
            * Vérifier le jeu de paramétres régionaux puis valider sur **"OK"**
            * Valider sur "Finish" puis redemarrer
            
        #. Modifier manuellement le fichier keyboard
        
            * Editer le fichier keyboard
                + sudo nano /etc/default/keyboard
                
            * remplacer "gb" par "fr"


------------------------------------------------------------------------------------------

Vocabulaire
===========

HAT (Chapeau)
            C'est le nom que porte les cartes filles sur Raspberry Pi.
            Sur Arduino, cela s'appel un Shield (Bouclier)

------------------------------------------------------------------------------------------

La bibliotheque RPi.GPIO
========================

:liens Web:
            * https://pypi.python.org/pypi/RPi.GPIO
            * http://sourceforge.net/projects/raspberry-gpio-python/
            * http://sourceforge.net/p/raspberry-gpio-python/wiki/Home/
            * http://deusyss.developpez.com/tutoriels/RaspberryPi/PythonEtLeGpio/
            * http://raspberrypi-aa.github.io/session2/input.html
                    
Implantation RPi2
-----------------

         .. image:: ./Images/raspberrypi/GPIO.png
             :width: 400 px
             :align: center

Installation de RPi.GPIO
------------------------

        #.  Si RPi.GPIO n'est pas installer, saisir : ::
            
                pip install RPi.GPIO
            
            Pour mettre à jour la bibliothèque : ::
            
                pip install RPi.GPIO -- upgrade


Utilisation de RPi.GPIO avec Python
-----------------------------------

        #. Importer la bibliothèque : ::
            
                import RPi.GPIO as GPIO
                    # Attention, c'est bien RPi avec un i minuscule

        #. Choisir la notation pour accèder au broche du GPIO.
        
            * Il y a 2 façon d'adresser les broches du GPIO, soit par sont numéro
              de broche (GPIO.BOARD) soit par son nom dans le registre (GPIO.BCM).
              C'est la methode ".setmode()" qui permet de configurer le mode de
              fonctionnement des GPIO.
              
Quick ref, les fonctions associer aux GPIO en python
----------------------------------------------------

:Liens Web:
            * http://raspi.tv/download/RPi.GPIO-Cheat-Sheet.pdf
            * http://raspi.tv/2014/rpi-gpio-port-function-checker
            * https://sourceforge.net/p/raspberry-gpio-python/wiki/browse_pages/
                # doc officielle
          
liste des différentes commandes : ::

    # RPi.GPIO Basics cheat sheet - Don't try to run this. It'll fail!
    # Alex Eames http://RasPi.TV
    # http://RasPi.TV/?p=4320

    # RPi.GPIO Official Documentation http://sourceforge.net/p/raspberry-gpio-python/wiki/Home/

    import RPi.GPIO as GPIO              # import RPi.GPIO module  

    # choose BOARD or BCM
    GPIO.setmode(GPIO.BCM)               # BCM for GPIO numbering
    GPIO.setmode(GPIO.BOARD)             # BOARD for P1 pin numbering

    # Set up Inputs
    GPIO.setup(port_or_pin, GPIO.IN)     # set port/pin as an input
    GPIO.setup(port_or_pin, GPIO.IN,  pull_up_down=GPIO.PUD_DOWN) # input with pull-down
    GPIO.setup(port_or_pin, GPIO.IN,  pull_up_down=GPIO.PUD_UP)   # input with pull-up 

    # Set up Outputs
    GPIO.setup(port_or_pin, GPIO.OUT)               # set port/pin as an output   
    GPIO.setup(port_or_pin, GPIO.OUT, initial=1)    # set initial value option (1 or 0)

    # Switch Outputs
    GPIO.output(port_or_pin, 1)     # set an output port/pin value to 1/GPIO.HIGH/True  
    GPIO.output(port_or_pin, 0)     # set an output port/pin value to 0/GPIO.LOW/False  

    # Read status of inputs OR outputs
    i = GPIO.input(port_or_pin)     # read status of pin/port and assign to variable i
    if GPIO.input(port_or_pin):     # use input status directly in program logic

    # Clean up on exit
    GPIO.cleanup()

    # What Raspberry Pi revision are we running?
    GPIO.RPI_REVISION #  0 = Compute Module, 1 = Rev 1, 2 = Rev 2, 3 = Model B+

    # What version of RPi.GPIO are we running?
    GPIO.VERSION

    # What Python version are we running?
    import sys; sys.version
    
    # Query the setup status of a port
    GPIO.gpio_function(port)        # The result will be a numerical return code, which 
                                    # will have one of the following values…
                                    # 0 = GPIO.OUT
                                    # 1 = GPIO.IN
                                    # 40 = GPIO.SERIAL
                                    # 41 = GPIO.SPI
                                    # 42 = GPIO.I2C
                                    # 43 = GPIO.HARD_PWM
                                    # -1 = GPIO.UNKNOWN


####

Protocole I2C
=============

:liens Web:
            * http://www.instructables.com/id/Interfacing-Digital-Compass-HMC5883L-with-Raspberr/
            * http://elinux.org/RPi_ADC_I2C_Python
            * http://www.bitflippersanonymous.com/raspberry-pi-projects/i2c-temperature
                # exemple pour un capteur de température i2c
                                                
            * http://mchobby.be/wiki/index.php?title=ArduPi-I2C-Support
                # Exemple de comunication en i2c entre un RPi et un arduino
                en utilisant quick2wire.i2c
                                                
                    
:Ref:  
            * Livre (papier) Raspberry Pi2, page 558.
            * Chapitre 14, Section 2.3, paragraphe 2.3.3 : installation de la carte
                    
Installation / Activation de l'I2C
----------------------------------

        #. Entrée dans le fichier de config du rpi
            * sudo raspi-config
                + 9 Advanced Options
                    - A7 I2C
                        
                    [YES], [YES], [Finish]
        
        #. Ajouter une entrée dans le fichier "modules"

            * sudo nano /etc/modules
                + ajouter : i2c-dev
                + Sauvegarder et quitter
        
        #. Ajouter les paquets nécessaires
            * sudo apt-get install i2c-tools
            * sudo apt-get install python-smbus

        #. Redémarer le rpi
            * sudo reboot
                
        #. Ajouter l'utilisateur courant au groupe i2c
            * sudo adduser $USER i2c
                    
Connaître l'adresse des matériels branchés
------------------------------------------
            
        #. se placer dans le dossier modprob.d
            * cd /etc/modprobe.d/
                
        #. exécuter la commande i2cdetect avec des droits élever
            * sudo i2cdetect -y 1
    
        Exemple avec un magnétomètre HMC5883L : ::

            pi@raspiBlanc ~ $ cd /etc/modprobe.d/
            pi@raspiBlanc /etc/modprobe.d $ sudo i2cdetect -y 1
                 0  1  2  3  4  5  6  7  8  9  a  b  c  d  e  f
            00:          -- -- -- -- -- -- -- -- -- -- -- -- --
            10: -- -- -- -- -- -- -- -- -- -- -- -- -- -- 1e --
            20: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
            30: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
            40: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
            50: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
            60: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
            70: -- -- -- -- -- -- -- --

------------------------------------------------------------------------------------------

UART
====

Libérer l'UART
--------------
    
    **N.B :** par défaut l'uart est configuré en mode console pour le débug. pour l'utiliser,
    il faut d'abord le libérer.
    
        #.  Interroger le journal sur les dernier événement de la liaison série pour vérifier
        que l'opération n'a pas déjà été effectuer
        
            ::
            
                dmesg | grep tty
            
            si l'opération n'a pas encore été effectuer, le résultat obtenu doit être : ::

                [    0.002072] console [tty1] enabled
                [    0.195363] 3f201000.uart: ttyAMA0 at MMIO 0x3f201000 (irq = 83, base_baud = 0) is a PL011 rev2
                [    0.695429] console [ttyAMA0] enabled

            
        #. configurer l'UART avec l'outil de configuration du Rpi : ::
        
                sudo raspi-config
            
            
        #. se déplacer dans les menu selon la séquence suivante : ::
        
                [ 8 ] --> [ A8] --> [ Non ]
            
            Le quatrième écran vous informe que Serial est maintenant désactivé : ::
            
                [ Ok ] --> [ Finish ]
            
        #. Redémarrer : ::
        
                sudo reboot
            
        #.  Vérifier dans le journal que l'opération a bien été prise en compte : ::
        
                demsg | grep tty
            
            ce qui doit vous donner le résultat suivant : ::
            
                [    0.002051] console [tty1] enabled
                [    0.195175] 3f201000.uart: ttyAMA0 at MMIO 0x3f201000 (irq = 83, base_baud = 0) is a PL011 rev2

            On constate que la dernière ligne à disparue, le mode débug sur la sortie UART
            est donc bien désactivée.

------------------------------------------------------------------------------------------

PWM, Servo moteur et DC Motor
=============================

:liens Web:
            * https://fr.wikipedia.org/wiki/Modulation_de_largeur_d'impulsion
                # La page wikipedia sur la Modulation de Largeur d'Impulsion   
                (Pulse Width Modulation -- PWM)

            * http://deusyss.developpez.com/tutoriels/RaspberryPi/PythonEtLeGpio/#LIII-B-7
                # utilisation du PWM sur raspberry (en français)
                        
            * https://www.youtube.com/watch?v=BLtV0Z38S94
                # utilisation du PWM sur raspberry (vidéo)
                        
            * https://www.youtube.com/watch?v=ddlDgUymbxc
                # utilisation du servo moteur avec le RPi (video)
                        
            * https://www.youtube.com/watch?v=v2jpnyKPH64
                # principe de fonctionnement d'un servo moteur (video)
                        
            * https://www.youtube.com/watch?v=W7cV9_W12sM
                # utilisation d'un DC Motor avec le Pi (vidéo)
                
            * https://sourceforge.net/p/raspberry-gpio-python/wiki/PWM/
                # doc officiel GPIO.PWM (y'a pas grand chose)
        
    #. utilisation general du PWM / PFM
        Exemple d' utilisation (en python 3) : ::
        
            [ debut de script ]
                import RPI.GPIO as GPIO
                    # importation de la bibliothèque RPI
                GPIO.setmode(GPIO.BCM)
                    # Utilisation des GPIO en mode "BCM"
                
                une_broche_du_pi = 25
                GPIO.setup(une_broche_du_pi, GPIO.OUT)
                    # On choisi la sur la quelle on veut faire du PWM
                    # Il vaut mieux éviter de choisir une broche qui est aussi utilisée
                    # pour autre chose comme de l'I2C, du SPI ou du Serial
                
                frequence = 50
                rapportCyclique = 50
                
                p = GPIO.PWM(une_broche_du_pi, frequence)
                    # on initialise le PWM sur la broche choisie et on indique la fréquence
                    
                p.start(rapportCyclique)
                    # On l'impulsion en indiquant le rapport cyclique (Duty Cycle)
                    #
                    # Le rapport cyclique correspond au rapport de la durée de l’impulsion
                    # sur la periode. Cette valeur est exprimée en pourcentage
                    # voir https://fr.wikipedia.org/wiki/Rapport_cyclique_d'ouverture
                
                rapportCyclique = 80
                p.ChangeDutyCycle(rapportCyclique)
                    # pour changer le rapport cyclique "a la volée", on utilise
                    # la methode RPI.GPIO.PWM.ChangeDutyCycle()
                
                frequence = 100
                p.ChangeFrequency(frequence)
                    # On peut changer la frequence "a la volee". On parle alors de PFM
                    # on utilise la méthode RPI.GPIO.PWM.ChangeFrequency()
                    
                p.stop()
                    # on arrête l'impulsion
                    
                GPIO.cleanup()
                    # on libère toutes les GPIO
            [fin de script ]
            
    #. servo moteur :
        La période pour un servo moteur est généralement de 20ms
        (a controler avec la documentation). les angles : 0 ; 90 ; 180 son généralement
        associes a des durée d'impulsion de 0.5 ; 1.5 ; 2.5 ms ce qui donne les rapports cycliques
        (duty cycle) suivants : ::

        
            0.5/20 = 2.5%
            1.5/20 = 7.5%
            2.5/20 = 12.5 %
        
        L'ensemble des valeurs de 0 a 180° son donc comprises entre 0.5 et 2.5 ms soit
        entre 2.5% et 12.5%.
        
    #. DC motor :
        Le rapport cyclique permet de gérer la vitesse du moteur(valeur de 0 à 100).
        Il est préférable d'utiliser 2 broches PWM pour gérer le sens de rotation.
        
        +---+--+----------------------+
        | A | B|      Actions         |
        +===+==+======================+
        | 0 | 0| rotation off         |
        +---+--+----------------------+
        | 0 | 1| rotation on (sens 1) |
        +---+--+----------------------+
        | 1 | 0| rotation on (sens 2) |
        +---+--+----------------------+
        | 1 | 1| rotation off         |
        +---+--+----------------------+
        
        La fréquence est a adapter en fonction du bruit du moteur
        (quant il "chante", c'est pas bon)

####

Input pull-up / pull-down
=========================

:liens Web:
            * http://deusyss.developpez.com/tutoriels/RaspberryPi/PythonEtLeGpio/#LIII-B-8
                # un petit exemple en fr et en python
                
            * http://raspberrypi-aa.github.io/session2/input.html
                # petit panorama sur les entrées (interruption et pull-up-down)

    #. Pull-Up et Pull-Down sur le RPi
        Le RPi possède en interne une résistance de tirrage qui peut être activée
        de 2 façons différentes :
        
            - Pull-Up ([résistance entre le +3.3v et la broche] + gnd)
            - Pull-Down (+3.3v + [résistance entre la broche et le gnd])
            
        Activation de la Pull-Up : ::
            
            GPIO.setup(channel, GPIO.IN, pull_up_down=GPIO.PUD_UP)
            
        Activation de la Pull-Down : ::
        
            GPIO.setup(channel, GPIO.IN, pull_up_down=GPIO.PUD_DOWN)
            
####

Les interruptions (python + GPIO)
=================================

:liens Web:
            * http://raspi.tv/2013/how-to-use-interrupts-with-python-on-the-raspberry-pi-and-rpi-gpio
                # introductions aux interruptions (part 1)
                
            * http://raspi.tv/2013/how-to-use-interrupts-with-python-on-the-raspberry-pi-and-rpi-gpio-part-2
                # part2 - Threaded callback
                
            * http://raspi.tv/2013/how-to-use-interrupts-with-python-on-the-raspberry-pi-and-rpi-gpio-part-3
                # part 3 - Multiple threaded callback interrupts in Python
                
            * http://eduscol.education.fr/sti/sites/eduscol.education.fr.sti/files/ressources/pedagogiques/4346/4346-4-rpi-gpio.pdf
                # petite présentation en fr (avec exemple en python)
                
            * http://raspberrypi-aa.github.io/session2/input.html
                # petit panorama sur les entrées (interuption et pull-up-down)
                
            * http://deusyss.developpez.com/tutoriels/RaspberryPi/PythonEtLeGpio/#LIII-B-9
                # Les 3 types d'interruptions expliquées en Français
                
####

Plein d'astuce pour la gestion au quotidien
===========================================

:liens Web:
            * http://www.framboise314.fr/raspbian-tout-un-tas-de-trucs/#Effacement_de_lrsquocran
                # Exemple complet d'utilisation d'un Raspberry Pi et des GPIO dans docker

####

Utiliser les GPIO dans un container (Docker)
============================================

:Liens_Web:
            * https://iotbytes.wordpress.com/create-your-first-docker-container-for-raspberry-pi-to-blink-an-led/

            * https://stackoverflow.com/questions/30059784/docker-access-to-raspberry-pi-gpio-pins
                # La réponse de Tobias du 12/01/2018 présentes les 3 moyen d'accéder aux GPIO


