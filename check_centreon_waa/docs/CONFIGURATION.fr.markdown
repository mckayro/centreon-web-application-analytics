check\_centreon\_waa : Configuration
====================================

Description de la configuration de la sonde dans Centreon, et configuration d'un service lié à un scénario.

Configuration de la commande
----------------------------

La configuration de la commande s'effectue dans la partie "Configuration > Commands > Checks"
On ajoute une nouvelle commande avec en cliquant sur le lien _Add_.

On rempli le formulaire avec les informations suivantes :

* Command Name : check\_centreon\_waa : Le nom de la commande dans Centreon
* Command Type : check : Le type de la commande, ici check
* Command Line : $USER1$/check\_centreon\_waa -c $ARG1$ -w $ARG2$ -d $ARG3$ -t $ARG4$ -r $ARG5$ : La ligne de commande à exécuter par Nagios
* Graph Template : Default Graph
* Arguments Description :

        ARG1 : Le temps d'exécution maximum en secondes pour le niveau critique
        ARG2 : Le temps d'exécution maximum en secondes pour le niveau attention
        ARG3 : Le répertoire où sont stockés les scénarios
        ARG4 : Le nom du scénario
        ARG5 : Le serveur Selenium sous la forme host:port

Configuration du modèle de service
----------------------------------

Pour faciliter la configuration des services, on configure un modèle de service.

La configuration du modèle de service s'effectue dans la partie "Configuration > Services > Templates".
On ajoute une nouvelle commande avec en cliquant sur le lien _Add_.

On rempli le formulaire avec les informations suivantes :

* Alias : scenario\_waa
* Service Template Name : scenario\_waa
* Template Service Model : actif-service
* Check Command : check\_centreon\_waa

Les informations supplémentaires sont à remplir suivant les besoins.

Configuration d'un service
--------------------------

La configuration d'un service s'effectue dans la partie "Configuration > Service > Services by host"
On ajoute une nouvelle commande avec en cliquant sur le lien _Add_.

On rempli le formulaire avec les informations suivantes :

* Description : Scenario01 : Le nom du service qui sera relatif à un scénario
* Service template : scenario\_waa
* Args : Les arguments de la commande

        ARG1 : Exemple 60
        ARG2 : Exemple 50
        ARG3 : Exemple /var/lib/centreon\_waa
        ARG4 : Exemple scenario01
        ARG5 : Exemple selenium.domain.tld:4444

Les informations supplémentaires sont à remplir suivant les besoins.
