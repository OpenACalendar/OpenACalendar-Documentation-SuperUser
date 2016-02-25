Web Assets (JS, CSS, Images, etc)
=================================


Compiled from source files in core and extensions
-------------------------------------------------

Images, CSS and JavaScript can all be part of the Core code, or part of any extension.

Such files are in "/core/theme/<themename>/" or "/extension/<extensionname>/theme/<themename>/"

They are compiled by a build process into one of:

   *  /webIndex/theme/<themename>
   *  /webSite/theme/<themename>
   *  /webSingleSite/theme/<themename>
   
During compilation, assets with the same name in an extension will override assets in the core. In this way, extensions can override parts of the assets.
   
Theme variables
---------------

These can be set in a file in the core, or as part of any extension.

These can be found in "/core/theme/<themename>/variables.ini" or "/extension/<extensionname>/theme/<themename>/variables.ini".

Variables with the same name in an extension will override variables in the core. In this way, extensions can alter the assets.

Variables are used:

  *  They are automatically available as variables in LESS when CSS is complied.
  *  When emails are sent, the variables are loaded into variables in Twig so Twig templates can style the emails.

   
Compiling assets
----------------

The compilation scripts are in the folder "build".

First, run "composer install" in the build folder to get libraries that are not shipped with the app.

You may need to edit "build/localConfig.php" if you have moved parts of the application around.

Then simply run "php build.php".

The results are automatically placed in the correct web folders.

The results are portable; for a given set of extensions and configuration you can compile the assets on a dev machine then move them to production server.

Non Compiled
------------

Some standard libraries live in the normal web folders and are not compiled in any way.

Any changes (ie upgrading the libraries) will involve a change to the file names.

Because of this, the webserver can tell all web browsers to cache them for a long time.

