Extension Facebook
==================


Purpose
-------

This extension provides interaction with Facebook.

Importing by URL
----------------

If someone tries to import a single event from Facebook by URL, this extension will import the data.

If this extension is not set up, Facebook events can not be imported.


Installation
------------


Edit your config.php and add Facebook as an extension.

Go to the :doc:`sysadmin Web UI <systemAdministratorWebUI>`.

Go to the url /sysadmin/facebookuser

First you must enter an Facebook App ID and Secret. Obtain one from the Facebook Developers site. https://developers.facebook.com/

This app must be set up as a web app, and it must be given the correct domain of the site.

Once the App ID and Secret have been entered, a FaceBook user must press the "Login with Facebook" button. 
They may be asked to give the app permissions to read their account. We do not ask for permissions to write to Facebook.

You should now see App ID, App Secret and User Token all filled in.

The extension has been set up.


Usage
-----

If set up properly, it will just work.


