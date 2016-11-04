Requirements
============


  *  PHP 7.0 or higher
  *  PHP Extension - CURL for importing events
  *  PHP Extension - GD for image manipulation
  *  Postgresql
  *  Apache with ModRewrite (or equivalent)
  *  Command line access
  *  Cron

The requirement for PHP 7.0 or higher was introduced in version 2.0 of this app. If this is a problem for you, 
please check version 1.7, which supports PHP 5.4, 5.5 and 5.6.

It has currently been tested on Linux webservers only, but it may be possible 
to get it working on Windows servers.

The core code will use Open Street Map servers directly. 
Note this is subject to an `Tile usage policy <http://wiki.openstreetmap.org/wiki/Tile_usage_policy>`_ 
and if your site has heavy traffic, you should use another map provider. 
See one of the mapping extensions, such as :doc:`Mapbox<extensionMapbox>`

For developers
--------------

If you want to develop the core software or an extension, you will need some other software:

  *  Composer - https://getcomposer.org/
  
