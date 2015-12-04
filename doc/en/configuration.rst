Check configuration
===================

This part describes the configuration of the Centreon Web.

.. note::
    If you use plugin-packs and have installed ces-packs-applications-selenium 
    and ces-plugins-applications-selenium, please ignore these steps. You can 
    directly use App-Selenium-WAA host template and check "Create service linked to template".

Command configuration
~~~~~~~~~~~~~~~~~~~~~

The command is configured in the "Configuration > Commands > Checks".
To add a new command, click on the **Add** link.

We complete the form with the following information:

* Command Name : App-Selenium-Scenario
* Command Type : Check
* Command Line : $USER1$/centreon_plugins.pl --plugin apps::selenium::plugin --mode scenario --selenium-hostname $_HOSTSELENIUMHOST$ --selenium-port $_HOSTSELENIUMPORT$ --directory $_HOSTSCENARIODIR$ --scenario $_SERVICESCENARIONAME$ --timeout $_SERVICETIMEOUT$ --warning $_SERVICEWARNING$ --critical $_SERVICECRITICAL$

.. image:: _static/images/waa_configuration_01_CMD.png

Service template configuration
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

To facilitate the service configuration, we configure a service template.

The service template is configured in the **Configuration => Services => Templates*
to add a new service template, click on the **Add** link.

We complete the form with the following information:

* Alias : Scenario-Selenium
* Service Template Name : App-Selenium-Scenario-WAA
* Template Service Model : generic-service
* Check Command : App-Selenium-Scenario

Define the following macros:

* SCENARIONAME = @NAMEOFTHETEST@
* TIMEOUT = @CENTENGINETIMEOUT@
* WARNING = @WARNINGEXECUTIONTIME@
* CRITICAL = @CRITICALEXECUTIONTIME@

.. image:: _static/images/waa_configuration_02_STPL.png

Host configuration
~~~~~~~~~~~~~~~~~~

Add a new Host through **Configuration => Hosts => Add**.

Specify hostname, alias, IP address and select **generic-host** template. You must define following macros:

* SCENARIODIR = /var/lib/centreon_waa  [Local directory containing scenario]
* SELENIUMHOST = 192.168.1.1 [Set the IP Address of your Selenium server]
* SELENIUMPORT = 4444 [Change according to your configuration]

You can create a host template if you want, as in the screenshot below: 

.. image:: _static/images/waa_configuration_03_HTPL.png

Service configuration
~~~~~~~~~~~~~~~~~~~~~

The service is configured in the "Configuration > Services > Service by hosts"
to add a new service, click on the **Add** link.

We complete the form with the following information:

* Description : Scenario01 : The service name
* Service template : App-Selenium-Scenario-WAA
* The macro **SCENARIONAME** to specify the test associated to this service (you can override some of the macro defined in the service template if you want).


