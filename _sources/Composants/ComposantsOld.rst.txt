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
