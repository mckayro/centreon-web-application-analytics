Installation
============

Prerequisites
~~~~~~~~~~~~~

.. note::
    Centreon advises to install the Selenium server on a dedicated poller for
    web scenarios monitoring and not on an existing monitoring poller. This
    allows to do not impact monitoring of hosts and services.

Hardware requirements for the server:

* 6 vCPU 3 GHz
* 8 Gb RAM
* a minimum filesystem space of 30 Gb 

Software requirements:

* A monitoring server with Centreon Engine
* Firefox minimum version or Iceweasel 27.0.1
* Selenium version 2.40

From packages
~~~~~~~~~~~~~

Selenium server
---------------

This server could be installed on a **monitoring poller**. If you plan to deploy huge number or complex scenarios, we strongly recommend to use a **dedicated server** to run Selenium.

If you are using Centreon Enterprise Server. Type the following command to install Selenium-server and all the dependencies needed ::

  # yum install centreon-selenium-server

To start Selenium and xorg-x11-server-Xvfb services use the following commands ::

  # /etc/init.d/xvfb start
  # chkconfig --add xfvb
  # chkconfig --level 2345 xfvb on
  # /etc/init.d/selenium start
  # chkconfig --add selenium
  # chkconfig --level 2345 selenium on
	
Centreon Selenium Plugin
------------------------

If you are using Centreon Enterprise Server with Plugins Pack repository. Type the following commands to install the plugin and associated host/service templates ::

  # yum install ces-packs-applications-selenium
  # yum install ces-plugins-applications-selenium

.. note:: 
    If you do not have the plugin-packs license, please follow installation steps described above in the "From sources > 

From sources
~~~~~~~~~~~~

Init scripts and variables files needed for the Selenium server are provided in this repository : https://github.com/centreon/centreon-web-application-analytics
They are NOT needed when using RPM packaging.

Desktop installation
--------------------

The desktop is for creating scenarios with Selenium IDE.

Installation:

* Start Firefox
* Go to `Selenium download page <http://seleniumhq.org/download/>`
* In section *Selenium IDE*, download the last release of Selenium IDE
* Validate the XPI
* Restart Firefox

After the restart of Firefox, you can find the Selenium IDE in "Tools > Selenium IDE"

Selenium server installation
----------------------------

This server runs the Selenium RC server which drives the Firefox browser.

.. warning::
   You must verify the compatibility between Firefox and Selenium server. This information is in Selenium server `Changelog <https://selenium.googlecode.com/svn/trunk/java/CHANGELOG>`_.
   For example, if you have Firefox 10 or below, you must use Selenium server version 2.20.0 or below.

Java installation
-----------------

The minimal Java version is 1.6.

On Debian::

  # apt-get install sun-java6-jre sun-java6-bin

On CentOS or CES::

  # yum install java-1.6.0-openjdk

For other installation, go to the `java site <http://www.java.com>` and download the JRE.

Virtual X server installation
-----------------------------

The Selenium server must run a browser for executing scenarios. An X server must be installed.

For lighter installation, we will use the Framebuffer server (xvfb).

On Debian::

  # apt-get install xvfb

On CentOS or CES::

  # yum install xorg-x11-server-Xvfb

To start the server on boot, a script is available in the Git.
To install this script, copy the init-xvfb for your distribution into /etc/init.d and the default-xvfb into /etc/default.

To activate this start options:

On Debian::

  # chmod a+x /etc/init.d/xvfb
  # update-rc.d xvfb defaults
  # mkdir -p /usr/local/labkey/

On CentOS or CES::

  # chmod a+x /etc/init.d/xvfb
  # chkconfig --add xvfb
  # mkdir -p /usr/local/labkey/

The configuration variables are:

* **X_SERVER_NUMBER** : The X display port
* **FBDIR** : The directory for cache framebuffer file

Browser installation
--------------------

The browser must be a Firefox or Iceweasel.

On Debian::

  # apt-get install iceweasel

On CentOS or CES::

  # yum install firefox

Selenium server installation
----------------------------

The Selenium server is a JAR archive. We can download this archive from the `selenium download page <http://seleniumhq.org/download>`_ in the "Selenium Server" section.
We copy the downloaded archive into a directory and make a symbolic link to make the upgrade easier.

Example::

  # mkdir /opt/selenium
  # cd /opt/selenium
  # cp ~/selenium-server-standalone-version.jar /opt/selenium
  # ln -sf selenium-server-standalone-version.jar selenium-server-standalone.jar

To start the server on boot, a script is available in the centreon waa source package.
To install this script, copy the init-selenium from Git into /etc/init.d and the default-selenium into /etc/default.

To activate this start options:

On Debian::

  # useradd -r -s /bin/bash -d /var/run/selenium -m selenium
  # mkdir -p /var/log/selenium
  # chown selenium: /var/log/selenium
  # chmod a+x /etc/init.d/selenium
  # update-rc.d selenium defaults

On CentOS or CES::

  # useradd -r -s /bin/bash -d /var/run/selenium -m selenium
  # mkdir -p /var/log/selenium
  # chown selenium: /var/log/selenium
  # chmod a+x /etc/init.d/selenium
  # chkconfig --add selenium

The configuration variables are:

* **SELENIUM_LIB** : The path to the Selenium JAR
* **SELENIUM_PORT** : The listening port for Selenium server
* **SELENIUM_LOGDIR** : The log directory
* **SELENIUM_PID** : The path for PID file
* **SELENIUM_FFPROFILE** : The Firefox profile used to run the scenarios
* **X_DISPLAY** : The X display port

Centreon WAA Plugin
~~~~~~~~~~~~~~~~~~~

This check must be installed on the **monitoring server** (central or poller). We strongly recommend to use a **poller**

PERL requirements
-----------------

The list of perl plugins:

* Getopt::Long
* Time::HiRes
* XML::XPath
* WWW::Selenium

On Debian::

  # apt-get install libtest-www-selenium-perl

On CentOS or CES with epel repository::

  # yum install perl-Test-WWW-Selenium perl-XML-XPath

With CPAN::

  # cpan -i Getopt::Long Time::HiRes XML::XPath WWW::Selenium

Plugin installation
-------------------

To install the plugin, it is necessary to get Centreon Plugins project.

::

  # cd /tmp
  # git clone http://git.centreon.com/centreon-plugins.git
  # mv centreon-plugins/* /usr/lib/nagios/plugins/

Scenario directory
------------------

This check uses a Selenium scenario in HTML format, these scenarios are copied into a directory::

  # mkdir /var/lib/centreon_waa
  # chown centreon-engine:centreon-engine: /var/lib/centreon_waa
