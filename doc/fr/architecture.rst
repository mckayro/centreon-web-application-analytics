Fonctionnement
==============

Le plugin Centreon WAA permet d'executer à distance des scenarios Web, en utilisant les fonctionnalités d'un serveur Selenium et d'un navigateur Firefox.

Quand un contrôle est executé, trois étapes sont réalisées :

* Centreon-Engine execute le plugin check_centreon_waa
* Le plugin effectue une connexion au serveur Selenium en spécifiant un scénario à realiser
* Le serveur Selenium executes le scénario spécifié et renvoie le résultat (temps d'execution, nombres d'étapes réussies / nombres d'étapes totales).

.. image:: _static/images/schema1_doc_waa_FR.png

Une explication detaillée du fonctionnement de Selenium est disponible `ici <http://docs.seleniumhq.org/docs/05_selenium_rc.jsp#how-selenium-rc-works>`_.
