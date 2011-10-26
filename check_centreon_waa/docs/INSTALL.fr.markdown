check\_centreon\_waa : Installation
===================================

Pré-requis
----------

Pour l'utilisation de ce plugin, il faut :

* Un poste client avec Firefox 4.0 ou supérieur
* Un serveur qui effectuera les test Selenium
* Un serveur de supervision Nagios/Centreon Engine ou Nagios compatible

Installation sur le poste client
--------------------------------

Le poste client permet de créer des scénarios avec l'ide Selenium.

Pour l'installation :

* Lancer le navigateur Firefox
* Se rendre à l'URL suivante <http://seleniumhq.org/download/>
* Dans la partie "Selenium IDE", cliquer sur le lien "Download version x.x.x released"
* Valider l'installation du module XPI
* Redémarrer Firefox

Après le redémarrage de Firefox, l'ide Selenium est disponible dans "Outils > Selenium IDE"

Installation du serveur Selenium
--------------------------------

Le serveur Selenium est le serveur qui va effectuer l'exécution des scénario. Il fonctionne sur le moteur Selenium Server.

### Installation de Java

Il faut la machine virtuelle Java 1.6 pour faire fonctionner Selenium Server.

Sous debian:

    apt-get install sun-java6-jre sun-java6-bin

Sinon aller sur le site <http://www.java.com> pour télécharger la machine virtuelle JRE. Voir <http://www.java.com/fr/download/help/linux_install.xml>.

### Installation du serveur virtuel X

Selenium Server doit lancer un navigateur pour exécuter les scénarios, il faut installer un serveur X pour cela.

L'installation du serveur virtuel X xvfb permet de ne pas lancer un serveur X complet.

Sous debian:

    apt-get install xvfb

Sous CentOS 5.6 :

    yum install xorg-x11-server-Xvfb

Pour le lancement automatique de ce serveur, un script d'init est disponible dans le répertoire extras des sources. Ce script se nomme _distrib_-xvfb.
Il faut copier le fichier pour votre distribution linux dans le répertoire /etc/init.d.
Pour activer le lancement automatique :

Sous debian:

    chmod a+x /etc/init.d/xvfb
    update-rc.d xvfb defaults	

Sous CentOS 5.6 :

    chmod a+x /etc/init.d/xvfb
    chkconfig --add xvfb

Dans le fichier de lancement du service xvfb, on peut configurer les informations suivantes :

* **X\_SERVER\_NUMBER** : Le numéro du serveur X
* **FBDIR** : Le répertoire contenant les fichiers des serveurs X

### Installation du navigateur web

On installe le navigateur web Firefox sur le serveur.
Ce navigateur servira à exécuter les scénarios.

Sous debian :

    apt-get install iceweasel

Sous CentOS 5.6 :

    yum install firefox

### Installation du serveur Selenium Server

Le Selenium Server est une archive JAR. On peut trouver cette archive sur le site de Selenium à la page <http://seleniumhq.org/download> dans la section "Selenium Server".
On copie l'archive dans un répertoire, et on crée un lien sympbolique pour faciliter les mises à jour.
Dans l'exemple le répertoire du serveur Selenium est /opt/selenium.

    cd /opt/selenium
    ln -s selenium-server-standalone-version.jar selenium-server-standalone.jar

Pour le lancement automatique de ce serveur, un script d'init est disponible dans le répertoire extras des sources. Ce script se nomme selenium.
Il faut copier le fichier pour votre distribution linux dans le répertoire /etc/init.d.
Pour activer le lancement automatique :

Sous debian:

    chmod a+x /etc/init.d/selenium
    update-rc.d selenium defaults	

Sous CentOS 5.6 :

    chmod a+x /etc/init.d/selenium
    chkconfig --add selenium

Dans le fichier de lancement du service Selenium Server, on peut configurer les options suivantes :

* **SELENIUM\_LIB** : Le chemin de l'archive Selenium Server
* **SELENIUM\_PORT** : Le port d'écoute du serveur Selenium
* **SELENIUM\_LOGDIR** : Le répertoire pour les fichiers de log du serveur Selenium
* **SELENIUM\_PID** : Le fichier pid du service

Installation de la sonde de supervision
---------------------------------------

La sonde de supervision permet de lancer le scénario à vérifier. Elle fait appel au serveur Selenium qui exécutera le scénario.
Cette sonde sera installée sur les serveurs de supervision.

### Les dépendances PERL

La liste des modules PERL devant être installée :

* Getopt::Long
* Time::HiRes
* XML::XPath
* WWW::Selenium

Ces dépendances peuvent être installées par les paquets ou par CPAN.

Si on installe les modules par CPAN, la ligne de commande est :

    cpan -i Getopt::Long Time::HiRes XML::XPath WWW::Selenium

### Installation de la sonde

Pour installer la sonde, on copie le fichier check\_centreon\_waa dans le répertoire des sondes Nagios.
Dans l'exemple le répertoire sera /usr/lib64/nagios/plugins.

On modifie les droits sur le fichier.

    chown nagios: /usr/lib64/nagios/plugins/check_centreon_waa
    chmod a+x /usr/lib64/nagios/plugins/check_centreon_waa

### Répertoire des scénarios

Pour l'exécution de la sonde, les scénarios seront déposés sous la forme d'un fichier html dans un répertoire unique.
Le nom du fichier sans son extension html sera le nom du scénario.
On va créer un répertoire pour stocker ces fichiers, dans l'exemple /var/lib/centreon\_waa.

    mkdir /var/lib/centreon_waa
    chown nagios: /var/lib/centreon_waa
