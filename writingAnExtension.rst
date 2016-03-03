Writing An Extension
====================

Creating the basic Extension
----------------------------


Run the command

.. code-block:: bash

    php build/newExtension.php "Sample" "org\openacalendar\sample"

The first "Sample" is the name of the folder that will be created.

The second "org\\openacalendar\\sample" is a PHP namespace that will be used to uniquely identify the extension. 
It should be your domain name in reverse with an extension part at the end - our domain name is "openacalendar.org".

This will create a bunch of files and folders, and give you instructions on activating the extension by adding it to your config.php.

Developing templates
--------------------

When actively developing templates, it is best to keep your install in debug mode by setting this in config.php.

Overriding a template in your extension
---------------------------------------

Simply copy the template you want to override from the core/theme/default folder into your extension.

For example

.. code-block:: bash

    mkdir -p extension/Sample/theme/default/templates/site/index
    cp core/theme/default/templates/site/index/index.html.twig  extension/Sample/theme/default/templates/site/index

You can new edit the file extension/Sample/theme/default/templates/site/index/index.html.twig to change the front page of the site!


