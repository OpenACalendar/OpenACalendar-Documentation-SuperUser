Extension Mapbox
================

This extension makes your site use Mapbox as a map tile provider.

If you do not configure this (or another map tile provider) your site will use Open Street Map servers directly. 
Note this is subject to an `Tile usage policy <http://wiki.openstreetmap.org/wiki/Tile_usage_policy>`_ and if your site has heavy traffic you should set up an alternative.

Available since v1.6.3.

Installation
------------

This extension is included with the core software and only needs to be set up.

Setting up
----------

Edit your config.php and add Mapbox as an extension.

You need to add two config variables:

.. code-block:: php

    $CONFIG->mapboxProjectId = 'mapbox.streets';
    $CONFIG->mapboxPublicAPIToken = 'pk.xxxxxxxxxxxxxxx';
	
The API token given here should be a public token.

