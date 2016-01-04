# Centreon Web Application Analytics

## Overview

This repository holds files needed to setup a Selenium server that can plan scenarii written with Selenium IDE.

## Selenium server

It can be installed either through RPM using documentation provided here as part of CES: htt://documentation.centreon.com
Using RPM, files in this repository are NOT needed.

Those who want to install without RPM can follow the documentation and use files provided in this repository.

## Selenium plugin

This is the client part, in charge of reading the scenario, and sending commands to the Selenium server.

We used to provided a plugin called "check_centreon_waa". It is now deprecated and replaced by the Selenium plugin found in Centreon Plugins.
Thos who wish to use it can either download it from Git (community) or use the associated Plugin Pack (entreprise clients).
