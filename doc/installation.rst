Installation
============

Requirement
-----------

* A desktop with Firefox 4 or above
* A server with Selenium and Firefox
* A monitoring server with Centreon Engine or Nagios

Desktop installation
--------------------

The desktop is for creating scenarios with Selenium IDE.

Installation:

* Start Firefox
* Go to `Selenium download page <http://seleniumhq.org/download/>`_
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
~~~~~~~~~~~~~~~~~

The minimal Java version is 1.6.

On Debian::

  # apt-get install sun-java6-jre sun-java6-bin

On CentOS or CES::

  # yum install java-1.6.0-openjdk

For other installation, go to the `java site <http://www.java.com>` and download the JRE.

Virtual X server installation
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The Selenium server must run a browser for executing scenarios. An X server must be installed.

For lighter installation, we will use the Framebuffer server (xvfb).

On Debian::

  # apt-get install xvfb

On CentOS or CES::

  # yum install xorg-x11-server-Xvfb

To start the server on boot, a script is available in the centreon waa source package.
To install this script, copy the init-xvfb for your distribution into /etc/init.d and the default-xvfb into /etc/default.

To activate this start options::

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
~~~~~~~~~~~~~~~~~~~~

The browser must be a Firefox or Iceweasel.

On Debian::

  # apt-get install iceweasel

On CentOS or CES::

  # yum install firefox

Selenium server installation
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The Selenium server is a JAR archive. We can download this archive from the `selenium download page <http://seleniumhq.org/download>`_ in the "Selenium Server" section.
We copy the downloaded archive into a directory and make a symbolic link to make the upgrade easier.

Example::

  # mkdir /opt/selenium
  # cd /opt/selenium
  # cp ~/selenium-server-standalone-version.jar /opt/selenium
  # ln -sf selenium-server-standalone-version.jar selenium-server-standalone.jar

To start the server on boot, a script is available in the centreon waa source package.
To install this script, copy the init-selenium for your distribution into /etc/init.d and the default-selenium into /etc/default.

To activate this start options::

On Debian::

  # useradd -r -s /bin/bash -d /var/run/selenium -m selenium
  # mkdir -p /var/log/selenium 
  # chmod a+x /etc/init.d/selenium
  # update-rc.d selenium defaults

On CentOS or CES::

  # useradd -r -s /bin/bash -d /var/run/selenium -m selenium
  # mkdir -p /var/log/selenium 
  # chmod a+x /etc/init.d/selenium
  # chkconfig --add selenium

The configuration variables are:

* **SELENIUM_LIB** : The path to the Selenium JAR
* **SELENIUM_PORT** : The listening port for Selenium server
* **SELENIUM_LOGDIR** : The log directory 
* **SELENIUM_PID** : The path for PID file
* **SELENIUM_FFPROFILE** : The Firefox profile used to run the scenarios
* **X_DISPLAY** : The X display port

Check installation
------------------

This check must be installed on the monitoring server (central or poller)

PERL requirements
~~~~~~~~~~~~~~~~~

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

Check installation
~~~~~~~~~~~~~~~~~~

The check is check_centreon_waa, you must copy this file into the Nagios plugin directory::

  # cp check_centreon_waa /usr/lib/nagios/plugins/
  # chown nagios: /usr/lib/nagios/plugins/check_centreon_waa
  # chmod a+x /usr/lib/nagios/plugins/check_centreon_waa

Scenario directory
~~~~~~~~~~~~~~~~~~

This check uses a Selenium scenario in HTML format, these scenarios are copied into a directory::

  # mkdir /var/lib/centreon_waa
  # chown nagios: /var/lib/centreon_waa
