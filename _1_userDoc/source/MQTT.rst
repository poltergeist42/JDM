====
MQTT
====

------------
Installation
------------

Windows
=======

    :Liens_WEB:
            * https://www.youtube.com/watch?v=n0l5xNOH4Dk


    #. Download mosquitto https://mosquitto.org/download/

    #. Download openssl http://slproweb.com/products/Win32Ope

    #. Copy openssl32\bin folder to mosquitto C:\openssl\bin --- C:\Program Files(x86)\mosquitto 

    #. Copy required dll files C:\openssl\libeay32.dll --- C:\Program Files(x86)\mosquitto

    #. Copy required dll files C:\openssl\ssleay32.dll --- C:\Program Files(x86)\mosquitto

    #. Download pthreadVC2.dll ftp://sources.redhat.com/pub/pthreads-win32/dll-latest/dll/x86/

    #. Copy pthreadVC2.dll file C:\Downloads\pthreadVC2.dll --- C:\Program Files(x86)\mosquitto 

    #. Test subscriber / server mosquitto_sub -v -t 'home/light'

    #. Test publisher / client mosquitto_pub -t 'home/light' -m 'Turn ON' 

    #. Test2 publisher / client mosquitto_pub -t 'home/light' -m 'Turn OFF'
