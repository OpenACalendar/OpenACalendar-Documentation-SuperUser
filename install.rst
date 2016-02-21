Install
=======

Install Single Site Mode
------------------------

Get the code and place on a web server.

(If downloading the code as a release from the website, it is complete. If downloading as source code or from Git, you will need to use composer to install libraries. Run "composer install" in the root directory. https://getcomposer.org/ )

Set up a Postgres database.

Copy config.dist.php to config.php and and edit it.

Run the PHP script "core/cli/upgradeDatabase.php".

Run the PHP script "core/cli/loadStaticData.php".

Run the PHP script "core/cli/createUser.php USERNAME EMAIL PASSWORD sysadmin" 
to create your first user.

Run the PHP script "core/cli/createSite.php SLUG EMAIL" where slug is something 
like "site". (If the site will always be used in Single Site mode the slug does not matter.)

The folder "webSingleSite" must be served by the webserver. Enable SSL if possible. 
Note there is an .htaccess file in there that Apache must use.

The folder "cache/templates.web" must be writable be the webserver.

Enable :doc:`a required cron job <cron>`.

Install Single Site Mode where all files are under web root
-----------------------------------------------------------

You will notice that the code has a filesystem where the webroot is under other code. 
We realise this may make it hard to install on some hosts. You can change the folders 
around so all code is under the web root.

In "webSingleSite", create the folder "oacapp". For security reasons, set up apache not to serve 
this folder using an .htaccess file or other method. 

Move all folders except "webSingleSite" underneath your new "oacapp" folder.

Edit the file "webSingleSite/localConfig.php", and change the constant APP_ROOT_DIR 
so it is defined thus:

    define('APP_ROOT_DIR', __DIR__.DIRECTORY_SEPARATOR.'oacapp'.DIRECTORY_SEPARATOR);

Note when updating in future, be careful not to overwrite this file.
	
The files under "webSingleSite" can now be deployed onto your webserver, and 
the rest of the set up instructions for Single Site Mode followed.

Install Multi Site Mode
-----------------------


Choose domain names
^^^^^^^^^^^^^^^^^^^

The folder "webIndex" must be served by the webserver, on a single name (eg "www.example.com"). 

The folder "webSite" must be served by the webserver, on a name that allows any 
subdomain to reach it (eg "*.example.com").

There must be a common domain between them (eg in this case, it's "example.com"). This is because cookies are shared among them.

Let's go!
^^^^^^^^^

Get the code and place on a web server.

(If downloading the code as a release from the website, it is complete. If downloading as source code or from Git, you will need to use composer to install libraries. Run "composer install" in the root directory. https://getcomposer.org/ )

Set up a Postgres database.

Copy config.dist.php to config.php and edit it.

Run the PHP script "core/cli/upgradeDatabase.php".

Run the PHP script "core/cli/loadStaticData.php".

Run the PHP script "core/cli/createUser.php USERNAME EMAIL PASSWORD sysadmin" 
to create your first user.

Create the demo calendar. Run the PHP script "core/cli/createSite.php SLUG EMAIL" 
where slug was set in your config.

The folder "webIndex" must be served by the webserver, on a single name (eg "www.example.com"). 
Enable SSL if possible. Note there is an .htaccess file in there that Apache must use.

The folder "webSite" must be served by the webserver, on a name that allows any 
subdomain to reach it (eg "*.example.com"). Enable SSL if possible. 
Note there is an .htaccess file in there that Apache must use.

Note you may have to be careful about the order of the apache virtual hosts to 
make sure that the  "webSite" folder does not get requests intended for the "webIndex" folder.

(You may notice folders "webSysAdmin" and "webSysAdminNotSecure" - these have been deprecated and can be ignored.)

The folder "cache/templates.web" must be writable be the webserver.

Enable :doc:`a required cron job <cron>`.




