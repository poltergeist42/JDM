====
HPVC
====

.. contents::
   :backlinks: top
   :depth: 3


--------------------
Pentest Distribution
--------------------

the distributions below have allmost all tools needed for a pentester. However it is possible to 
install individualy every tool in a non-dedicated os like Ubuntu, Debian and so on.

KALI Linux
==========

:Liens_Web:
      * `Kali Linux`_

.. _`Kali Linux`: https://www.kali.org/


Kali Linux is an open-source, Debian-based Linux distribution geared towards various information
security tasks, such as Penetration Testing, Security Research, Computer Forensics and Reverse
Engineering.

Install and upgrade tools
-------------------------

On a new install of Kali, we need to update, upgrade and fix tools

:Liens_Web:
      * `git repository called “pimpmykali”`_
      
.. _`git repository called “pimpmykali”`: https://github.com/Dewalt-arch/pimpmykali

.. code:: shell
   :number-lines:
   :force:

      sudo apt update && apt install git
      cd /opt
      git clone https://github.com/Dewalt-arch/pimpmykali
      cd pimpmykali
      sudo ./pimpmykali.sh


Parrot Security OS
==================

:Liens_Web:
      * `Parrot os`_

.. _`Parrot Os`: https://www.parrotsec.org/

Parrot OS, is a GNU/Linux distribution based on Debian and designed with Security and Privacy in
mind. It includes a full portable laboratory for all kinds of cyber security operations, from
pentesting to digital forensics and reverse engineering, but it also includes everything needed to
develop your own software or keep your data secure.

####

-----------------
Ennumeration tool
-----------------

Ennumeration tools can provide quickly all elements relative to a specific domain (or a web site).
They are generaly use the OSINT search methodes.

Exemple of data type :
   * subdomain
   * email adress
   * directory and subdirectory
   * file list
   * and so on

Google dork
===========

:Liens_Web:
      * `Google reference`_
      * `Google advanced search operator`_
      * `DDG syntax`_ 
      * `DDG ultimate guide`_ 

.. _`DDG ultimate guide`: https://brettterpstra.com/2019/03/07/the-ultimate-guide-to-duckduckgo/
.. _`DDG syntax`: https://help.duckduckgo.com/duckduckgo-help-pages/results/syntax/
.. _`Google reference`: https://developers.google.com/code-search/reference
.. _`Google advanced search operator`: https://ahrefs.com/blog/google-advanced-search-operators/

Search Engines can be the best "hacker's" friend to enumerate, performe an OSINT or doing social
engenering. Search engine provide a lot of "hiden" helpfull functionnality to do some specific
search.

GoBuster
========

:Liens_Web:
      * `GitHub GoBuster`_

.. _`GitHub GoBuster`: https://github.com/OJ/gobuster

GoBuster is a tool used to brute-force URIs (directories and files), DNS subdomains and virtual host
names.

sublist3r
=========

:Liens_Web:
      * `github Sublist3r`_ 

.. _`github Sublist3r`: https://github.com/aboul3la/Sublist3r

Sublist3r is a python tool designed to enumerate subdomains of websites using OSINT. It helps 
penetration testers and bug hunters collect and gather subdomains for the domain they are targeting.
Sublist3r enumerates subdomains using many search engines such as Google, Yahoo, Bing, Baidu and
Ask. Sublist3r also enumerates subdomains using Netcraft, Virustotal, ThreatCrowd, DNSdumpster and
ReverseDNS.

crt.sh (website)
================

:Liens_Web:
      * `website cert.sh`_

.. _`website cert.sh`: https://crt.sh

permform a analyse on a domain name to list the sub-domain based on the certificat.

OWASP Amass
===========

:Liens_Web:
      * `github OWASP Amass`_

.. _`github OWASP Amass`: https://github.com/OWASP/Amass

The OWASP Amass Project performs network mapping of attack surfaces and external asset discovery
using open source information gathering and active reconnaissance techniques.

theHarvester
============

:Liens_Web:
      * `github theHaverester`_
      * `theHaverester installation`_

.. _`github theHaverester` : https://github.com/laramies/theHarvester
.. _`theHaverester installation`: https://github.com/laramies/theHarvester/wiki/Installation

theHarvester is a very simple to use, yet powerful and effective tool designed to be used in the
early stages of a penetration test or red team engagement. Use it for open source
intelligence (OSINT) gathering to help determine a company's external threat landscape on the
internet. The tool gathers emails, names, subdomains, IPs and URLs using

   .. code:: shell
      :number-lines:
      :force:

      # theHaverester manual
      python3 theHarvester.py -h


enum4Linux
==========

:Liens_Web:
      * `GitHub enum4linux`_
      * `enum4linux Documentation`_

.. _`GitHub enum4linux`: https://github.com/CiscoCXSecurity/enum4linux
.. _`enum4linux Documentation`: https://labs.portcullis.co.uk/tools/enum4linux/

###

-------------
Ports scanner
-------------

nmap
====

:Liens_Web:
      * `nmap.org`_

.. _`nmap.org`: https://nmap.org/

Nmap ("Network Mapper") is a free and open source utility for network discovery and security
auditing. Nmap uses raw IP packets in novel ways to determine what hosts are available on the
network, what services (application name and version) those hosts are offering, what operating
systems (and OS versions) they are running, what type of packet filters/firewalls are in use, and
dozens of other characteristics. It was designed to rapidly scan large networks, but works fine
against single hosts. Nmap runs on all major computer operating systems, and official binary
packages are available for Linux, Windows, and Mac OS X. In addition to the classic command-line
Nmap executable, the Nmap suite includes an advanced GUI and results viewer (Zenmap), a flexible
data transfer, redirection, and debugging tool (Ncat), a utility for comparing scan results (Ndiff),
and a packet generation and response analysis tool (Nping).

   .. code:: shell
      :number-lines:
      :force:

      # nmap
      nmap -A -p- -T4 <ip ou plage ip>

      # Par défaut, le scan s'effectue sur le TCP (-sS). Pour forcer le scan en UCP il faut
      # utiliser l'option -sU.
      #
      # -A: Enable OS detection, version detection, script scanning, and traceroute
      #
      # -p-: permet de scanner tous les ports si le deuxième "-" est absent, seuls les 1000
      #      Premiers ports seront scanner
      #
      # -T4: permet de déterminer la vitesse du scan 0-lent --> 5-rapide

:.. warning:: Attention il n'y a pas de time out en UDP. Le scan peux donc durer indéfiniment. Il
              est donc conseiller de ne scanner que les 1000 premiers ports.

Performe a ping sweep with nmap
-------------------------------

.. code:: shell
   :number-lines:
   :force:

   sudo nmap -sn 192.168.1.0/24

This option tells Nmap not to do a port scan after host discovery and only print the available hosts
that respond to the probe. The default host discovery done with -sn consists of an ICMP echo
request, TCP SYN to port 443, TCP ACK to port 80, and an ICMP timestamp request by default.

N.B : In previous releases of Nmap, -sn was known as -sP.


####

-----------------------
Vulnerability Searching
-----------------------

ExploitDB
=========

:Liens_Web:
      * `ExploitDB (website)`_
      * `ExplotDB (CLI engine)`_

.. _`ExploitDB (website)`: https://www.exploit-db.com/
.. _`ExplotDB (CLI engine)`: https://www.exploit-db.com/searchsploit

ExploitDB tends to be very useful for hackers, as it often actually contains exploits that can be
downloaded and used straight out of the box. It tends to be one of the first stops when you
encounter software in a CTF or pentest.

If you're inclined towards the CLI on Linux, Kali comes pre-installed with a tool called
"searchsploit" which allows you to search ExploitDB from your own machine. This is offline, and
works using a downloaded version of the database, meaning that you already have all of the exploits
already on your Kali Linux!

   .. code:: shell
      :number-lines:
      :force:

      # Update database
      searchsploit -u

      # perform search
      # searchsploit [App_name]
      searchsploit wordpress 5


NATIONAL VULNERABILITY DATABASE (NVD)
=====================================

:Liens_Web:
      * `NVD (website)`_

.. _`NVD (website)`: https://nvd.nist.gov/vuln/search

NVD keeps track of CVEs (Common Vulnerabilities and Exposures) -- whether or not there is an exploit
publicly available -- so it's a really good place to look if you're researching vulnerabilities in a
specific piece of software. CVEs take the form: CVE-YEAR-IDNUMBER


CVE Mitre
=========

:Liens_Web:
      * `CVE Mitre (website)`_

.. _`CVE Mitre (website)`: https://cve.mitre.org/

The mission of the CVE® Program is to identify, define, and catalog publicly disclosed cybersecurity
vulnerabilities.


CERT-FR
=======

:Liens_Web:
      * `CERT-FR (Website)`_

.. _`CERT-FR (Website)`: https://www.cert.ssi.gouv.fr/

Centre gouvernemental de la veille, d'alerte et de réponse aux attaques informatiques


####

-------------
Linux command
-------------

SSH
===

:Liens_Web:
      * `StackOverflow Can I test authentication with an RSA key locally?`_

.. _`StackOverflow Can I test authentication with an RSA key locally?`: https://stackoverflow.com/questions/3891616/can-i-test-authentication-with-an-rsa-key-locally

ssh-add to add your key to your current ssh-agent
ssh-add -d to remove it off your ssh-agent

N.B : Lorsqu'une clef RSA est récupérée depuis un partage SMB saisir la command :

chmod 600 [Fichier_RSA]

####

--------
Weblinks
--------

.. target-notes::