Tips and ticks
--------------

#. How to create a firefox profile

  Use your firefox for create a profile. Add your information into this profile (add proxies configuration, add-ons...).
  When the configuration is finished, you must copy the profile into a directory in Selenium server. You must remove cache directory from profile directory and verify the size of this profile.
  If the profile if to large, it can cause some perfomance issues.
  For finish the configuration, you must modify the default script of Selenium for change the SELENIUM_FFPROFILE and restart the Selenium server.

#. Deactivate add ons auto update

  The auto update block the start of firefox browser and cause a Nagios timeout.
  For deactivate the auto update, go to **Options > Advanced > Update** and uncheck the options in section **Automatically check for updates to**

#. Pause in scenario

  If you have some latencies problem in your site, you can add some pause in your scenario and think to use clickAndWait action.
