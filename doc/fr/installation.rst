Installation
============

Depuis les paquets
~~~~~~~~~~~~~~~~~~

Serveur Selenium
----------------

Le serveur peut être un installé sur un de vos **satellites de supervision**. Cependant, si vous souhaitez mettre en oeuvre des scenarios nombreux et complexes, il est recommandé d'utiliser un **serveur dédié**.

Si vous utilisez les dépôts Centreon Enterprise Server, utiliser la commande suivante pour installer votre serveur :: 

     yum install centreon-selenium-server


Sonde de supervision
--------------------

Si vous bénéficier de l'offre **Plugins Packs**, vous pouvez installer facilement la sonde de supervision et les modèles d'hôtes et services associés via les commandes suivantes ::   

     yum install ces-packs-applications-selenium
     yum install ces-plugins-applications-selenim

.. note:: 

   Si vous n'avez pas accès aux plugins packs, l'installation du plugin peut être réalisée en suivante la procédure décrite dans la partie "Depuis les sources".
    

Depuis les sources
~~~~~~~~~~~~~~~~~~

Pré-requis 
----------

* Un environnement de bureau avec Firefox 4 ou plus récent
* Un serveur avec selenium et firefox d'installé
* Un serveur de supervision avec Centreon-engine ou Nagios.
* Un clone du git du projet http://git.centreon.com/centreon-web-applications-analytics


Installation de l'outil de scénario
-----------------------------------

Cette partie concerne le déploiement de l'IDE Selenium afin de réaliser vos scénarios.

Installation:

* Lancer Firefox
* Telécharger Selenium `Selenium download page <http://seleniumhq.org/download/>`
* Dans la section **Selenium IDE**, telécharger la dernière version
* Redémarrer Firefox

Vous avez désormais accès au Selenium IDE via le menu "Outils".

Installation du serveur Selenium
--------------------------------

Ce serveur habrite l'outil Selenium RC qui permet d'automatiser l'execution de vos scénarios dans Firefox. 

.. warning::
   
   Vérifier la compatibilité de Selenium avec votre version de Firefox `Changelog <https://selenium.googlecode.com/svn/trunk/java/CHANGELOG>`_.

   Par exemple, si vous utilisez une version de Firefox =< 10, vous devez utilisez une version de Selenium <= 2.20.0

Installation de Java
--------------------

La version Java minimum est 1.6. (validé avec la 1.7)

Sur Debian::

  # apt-get install sun-java6-jre sun-java6-bin

Sur CentOS/RHEL::

  # yum install java-1.6.0-openjdk


Pour les autres OS, reporter vous au `site officiel de java <http://www.java.com>` et télécharger le JRE correspondant.

Installation du serveur X virtuel
---------------------------------

Le serveur Selenium doit lancer un navigateur dpour executer ses scénarios, un serveur X doit donc être installé.

Pour une installation plus légère, nous utiliser Xvfb.

Sur Debian::

  # apt-get install xvfb

Sur CentOS/RHEL::

  # yum install xorg-x11-server-Xvfb

Pour lancer le serveur au démarrage, un script est disponible sur le git.

Pour l'installer, copier le init-xvfb dans le repertoire /etc/init.d et le fichier default-xvfb dans /etc/default

Pour activer son lancement :

Sur Debian::

  # chmod a+x /etc/init.d/xvfb
  # update-rc.d xvfb defaults
  # mkdir -p /usr/local/labkey/

Sur CentOS/RHEL::

  # chmod a+x /etc/init.d/xvfb
  # chkconfig --add xvfb
  # mkdir -p /usr/local/labkey/

Les variables à configurer sont les suivantes :

* **X_SERVER_NUMBER** : Le port X Display
* **FBDIR** : Répertoire de cache du démon

Installation du navigateur
--------------------------

Le navigateur utilisé est Firefox ou Iceweasel.

Sur Debian::

  # apt-get install iceweasel

Sur CentOS::

  # yum install firefox

Installation du serveur Selenium
--------------------------------

Le serveur Selenium est une archive JAR téléchargeable depuis cette `page <http://seleniumhq.org/download>`_ dans la section **Serveur Selenium**.

Copier l'archive dans un répertoire et créer un lien symbolique (facultatif, facilite une éventuelle mise à jour).

Exemple::

  # mkdir /opt/selenium
  # cd /opt/selenium
  # cp ~/selenium-server-standalone-version.jar /opt/selenium
  # ln -sf selenium-server-standalone-version.jar selenium-server-standalone.jar

Pour lancer le serveur au démarrage, un script est disponible sur le git.

Pour l'installer, copier le init-selenium dans le repertoire /etc/init.d et le fichier default-selenium dans /etc/default

Pour activer son lancement:

Sur Debian::

  # useradd -r -s /bin/bash -d /var/run/selenium -m selenium
  # mkdir -p /var/log/selenium
  # chown selenium: /var/log/selenium
  # chmod a+x /etc/init.d/selenium
  # update-rc.d selenium defaults

Sur CentOS/RHEL::

  # useradd -r -s /bin/bash -d /var/run/selenium -m selenium
  # mkdir -p /var/log/selenium
  # chown selenium: /var/log/selenium
  # chmod a+x /etc/init.d/selenium
  # chkconfig --add selenium

Les variables de configuration sont les suivantes : 

* **SELENIUM_LIB** : Chemin vers l'archive JAR du serveur Selenium 
* **SELENIUM_PORT** : Port d'écoute du serveur Selenium
* **SELENIUM_LOGDIR** : Répertoire des logs
* **SELENIUM_PID** : Chemin vers le fichier PID
* **SELENIUM_FFPROFILE** : Profil firefox a utiliser lors de l'exécution de vos scénarios
* **X_DISPLAY** : Le port X Display

Sonde Centreon WAA
~~~~~~~~~~~~~~~~~~

Le plugin doit être installé sur un de vos **serveurs de supervision** (central or poller).

Pré-requis Perl
---------------

Liste des librairies nécessaires:

* Getopt::Long
* Time::HiRes
* XML::XPath
* WWW::Selenium

Sur Debian::

  # apt-get install libtest-www-selenium-perl

Sur CentOS/RHEL ::

  # yum install perl-Test-WWW-Selenium perl-XML-XPath

Pour une installation via CPAN (non-recommandé!)::

  # cpan -i Getopt::Long Time::HiRes XML::XPath WWW::Selenium

Plugin tree
-----------

To install the check, please clone the centreon-plugins 3.0 git and copy needed files.

  # cd /usr/local/src
  # git clone http://git.centreon.com/centreon-plugins.git 
  # mv centreon-plugins/* /usr/lib/nagios/plugins/



Scenario directory
------------------

Le plugin utilise des scénarios Sélénium au format HTML, ces scénarios doivent être copiés en local sur le serveur de supervision exécutant le plugin::

  # mkdir /var/lib/centreon_waa
  # chown centreon-engine. /var/lib/centreon_waa


