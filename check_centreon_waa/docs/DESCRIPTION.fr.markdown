check\_centreon\_waa : Description du fonctionnement
====================================================

Le plugin check\_centreon\_waa utilise une architecture avec un serveur exécutant les scénarios.

Le fonctionnement est :

* Nagios exécute la sonde check\_centreon\_waa
* La sonde se connecte au serveur Selenium et demande l'exécution des actions du scénario
* Le serveur Selenium lance sur son serveur un navigateur web (Firefox) pour effectuer les actions

Le fonctionnement de Selenium Server est décrit à l'url suivante : <http://seleniumhq.org/docs/05_selenium_rc.html#how-selenium-rc-works>
