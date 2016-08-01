Upgrading
=========

Place in Read only mode
-----------------------

You can place the site in read only mode by setting these configuration variables:


.. code-block:: php

    $CONFIG->siteReadOnly = true
    $CONFIG->siteReadOnlyReason = "Upgrading"

Stop Message Que
----------------

If you are using the message que, stop any workers. See :doc:`message que documentation<installMessageQue>`

Backup
------

Backup the database contents and the file store folder, if used - check the "fileStoreLocation" configuration option.

Replace files
-------------

Place the new files over the old ones. (If you have had to change any 
"localConfig.php" files to accomodate your webserver, be careful to preserve 
the changes.)

Upgrade Database
----------------

Run the PHP script "php core/cli/upgradeDatabase.php".

Run the PHP script "php core/cli/loadStaticData.php".


Clear Caches
------------

On servers not in Debug mode, delete the existing cached templates. These are 
found in "cache/templates.cli" and "cache/templates.web". (It doesn't hurt to 
do this on debug servers so if in doubt, just do it.)

Build assets
------------

If you have changed theme variables or are using custom extensions, you should :doc:`run the web asset compilation procedure again<webAssets>`.

Increase asset version
----------------------

There are Apache config files included in the software that turn on browser caching 
for assets, such as images, CSS and JS. This should help speed up subsequent page loads for users. However when you update, you must make sure users get the latest version of all assets. To do this, the asset version must be incremented.

Your config.php should contain this variable:

.. code-block:: php

    $CONFIG->assetsVersion = 1

This is set to 1 by default - increase it by 1 every time you perform an upgrade.


Turn off read only mode
-----------------------

Set

.. code-block:: php

    $CONFIG->siteReadOnly = false


Start Message Ques
------------------

If you are using the message que, start new workers. See :doc:`message que documentation<installMessageQue>`


Advanced; Minimising errors when upgrading - Database upgrades
--------------------------------------------------------------

Following the upgrade procedure above means that there is a small period of time during which
the code has been upgraded and the database hasn't. Users may see errors during that time.

This can be avoided. Database changes are designed to be additions that can be upgraded before the code is upgraded.

Check out the new code into a seperate folder. Give this folder the same config.php and extensions as your normal web app.

Then run the PHP scripts "php core/cli/upgradeDatabase.php" and "php core/cli/loadStaticData.php" 
from this seperate folder.

Now update the code in your normal web app. The new DB structure will be in place already; thus minimising downtime.

