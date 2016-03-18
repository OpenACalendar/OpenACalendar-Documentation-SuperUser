Writing An Extension
====================

Creating the basic Extension
----------------------------

First, run "composer install" in the "build" folder to get libraries that are not shipped with the app.

Then run the command

.. code-block:: bash

    php build/newExtension.php "Sample" "org\openacalendar\sample"

The first "Sample" is the name of the folder that will be created.

The second "org\\openacalendar\\sample" is a PHP namespace that will be used to uniquely identify the extension. 
It should be your domain name in reverse with an extension part at the end - our domain name is "openacalendar.org".

This will create a bunch of files and folders, and give you instructions on activating the extension by adding it to your config.php.

Develop in debug mode
---------------------

When actively developing extensions, it is best to keep your install in debug mode by setting this in config.php.

.. code-block:: php

    $CONFIG->isDebug = true;


Overriding a template in your extension
---------------------------------------

Simply copy the template you want to override from the core/theme/default folder into your extension.

For example

.. code-block:: bash

    mkdir -p extension/Sample/theme/default/templates/site/index
    cp core/theme/default/templates/site/index/index.html.twig  extension/Sample/theme/default/templates/site/index

You can new edit the file extension/Sample/theme/default/templates/site/index/index.html.twig to change the front page of the site!

You may particularly want to do this for the privacy and terms and conditions pages, which by default just say "TODO".


.. code-block:: bash

    mkdir -p extension/Sample/theme/default/templates/index/index
    cp core/theme/default/templates/index/index/privacy.html.twig  extension/Sample/theme/default/templates/index/index
    cp core/theme/default/templates/index/index/terms.html.twig  extension/Sample/theme/default/templates/index/index
    
    
Adding a new web page
---------------------

(The phrase "web page" is used to indicate a page a human looks at - adding an API end point is slightly different.)

First, you need to create a route to link the URL to your code. This route file should be in

  *  "extension/Sample/webSite/index.routes.php" - in Multi Site mode, for pages that appear under a particular calendar.
  *  "extension/Sample/webIndex/index.routes.php" - in Multi Site mode, for pages that appear at the root of the site. 

In single Site mode, either place will be included. But there is also:  
  
  *  "extension/Sample/webSingleSite/index.routes.php" - for pages that should work in Single Site mode only.

It should contain:

.. code-block:: php

    <?php
    $app->match('/askmarc', "org\openacalendar\sample\controllers\IndexController::askMarc");

This links the URL to the controller, which should be placed in "extension/Sample/php/org/openacalendar/sample/controllers/IndexController.php" and contain:

.. code-block:: php

    <?php
    namespace org\openacalendar\sample\controllers;
    
    use Silex\Application;
    use Symfony\Component\HttpFoundation\Request;
    
    class IndexController {
        function askMarc(Application $app, Request $request) {
            return $app['twig']->render('extension/sample/index/askMarc.html.twig', array());
        }
    }

This is the code that is called - here you can run any normal PHP. Finally, it renders the twig template. This should be put at "extension/Sample/theme/default/templates/extension/sample/index/about.html.twig":

.. code-block:: twig

    {% extends 'index/page.html.twig' %}
    
    {% block pageTitle %}Ask Marc - {% endblock %}
    
    {% block content %}
	    <p>Ask Marc</p>
    {% endblock %}

Finally, you need to make sure that the URL /askMarc is routed to index.php by your webserver. This may require a change to the .htaccess in the relevant web folder to add:

.. code-block:: bash

    RewriteRule  ^askmarc(.*)$ /index.php/askmarc  [L]

