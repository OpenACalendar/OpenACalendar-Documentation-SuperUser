Web API V2
==========



*Note the current version of this API is still in progress, and some details may change*

Introduction
------------

Web API2 is a writeable API with user authentication by an OAuth like procedure.

Apps
----

All access must be done by an app.

Currently only system administrators can create apps.

Permissions app can ask for.

* Write User Actions  - write that user is attending events, write to users curated lists
* Write Calendar - write to events, groups, etc

Set callback methods the app is allowed to use. Callback methods are explained more later.

* URL
* Display
* Javascript

This stops stolen app credentials being used to widely. For example, in an Android app the app token and app secret must be in the app and an attacker could extract them. But if this app is configured for is callback javascript only and not is callback url, the attacker can't use those tokens in a web service.

* allowed callback URLs - text field, list them separated by new lines. The start of the callback URL specified later must match one of these. eg If you set allowed callback URLs to http://myserver.com/callback then http://myserver.com/callback/user/348 will pass but http://www.myserver.com/callback/user/348 will fail

Permissions Escalation
----------------------

You can set which permissions to ask for, and users will be able to edit permissions given. User can revoke permissions later.

So apps can start by asking for read access only then ask for write access later (by repeating the same process with a different scope parameter). Or they may ask for write access but get read access only. Or they may start with write access but then be bumped down to read access only later.

Apps therefore must always call /api2/current_user.json to check permissions.

Note each user grants permissions once per app. So if a user installs the same app twice (eg Android phone and Android Tablet), they all use the permissions. So if one app asks for and obtains better permissions, the other app will have that permission to.


Notes
-----

All tokens are random alphanumeric strings that could be between 1 or 255 chars long - the length is picked at random to increase the number of possibilities. Always allow for 255 chars long tokens in your app.

HTTPS should be used if possible. If the site doesn't have SSL installed then that's a security risk, but if so then the normal web login form and session cookies are over HTTP so whatever.

Passing variables can be GET or POST.

At the moment, all responses are JSON as denoted by .json at the end of URLS. We may add .xml and where applicable, .atom, .rss or .ical/.ics later. We may also provide URLs with nothing at the end, in which case the server will use the Accept header to decide what to send back.

A sys admin or app owner will be able to regenerate all user_token and user_secret for that app. This won't change any permissions users has granted, but will mean that all installs of the app have to re-authenticate.



User Authentication Workflow
----------------------------

Get Request Token
^^^^^^^^^^^^^^^^^

This is called in the app direct to the API, so the user can't see this.

Call /api2/request_token.json

pass:

 * app_token
 * app_secret

One of:

 * callback_url - URL to send user back to.
 * callback_display - boolean, "true". If set, the Access Token will just be shown on screen. Use for CLI scripts that say "Go to this URL, Get an Access Code, Paste it here!"
 * callback_javascript - boolean, "true". If set, Javascript interfaces will be called. This is used for Android apps that can place a WebView on a page and detect JS calls - your app can pick up and continue as soon as a Access Code is granted.

If you request a method your app is not allowed to use, it will be ignored. If you set more than 1, it will be random what happens and that's your fault.

Optional permissions to ask for. If you try to ask for a permission that your app doesn't have, it will be ignored.

 * scope - comma or space separated list of 
   * permission_write_user_actions
   * permission_write_calendar

Optional

 * user_token & user_secret - You may already have Read access for a user, and be asking for write access. In this case you know which user you want back, and if you get back a different user that gets complicated. So pass these, and this request token will be for this user only.
 * state - pass a alphanumeric string of up to 255 chars in length. This will be sent back later. Use this to mitigate against http://homakov.blogspot.co.uk/2012/07/saferweb-most-common-oauth2.html

Get as JSON:

 * request_token

Redirect User to get user permission
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Redirect User in their own web browser to /api2/login.html

Pass:

 * app_token
 * request_token

Here the user is asked to login then approve the app.

If callback_url is set, users web browser is redirected to this url with the GET param:

 * authorisation_token
 * state

(Because this is a GET request, there is a limit to the size of the request. http://stackoverflow.com/questions/7724270/max-size-of-url-parameters-in-get Otherwise we would pass request_token to)

If callback_display is set, authorisation_token will just be shown to user.

If callback_javascript is set, then

* OpenACalendar.accessGranted(authorisation_token,state) is called
* OpenACalendar.accessDenied() is called

Exchange Authorisation Token for User Token
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

This is called in the app direct to the API, so the user can't see this.

Call /api2/user_token.json

Pass:

 * app_token
 * app_secret
 * request_token
 * authorisation_token

Get back

 * user_token
 * user_secret


Call Authentication
-------------------

*Note the current version of this API is still in progress, and some details may change*

All requests to call the API (with the exception of those used to authenticate a user) must be authenticated


Authenticated with app and user
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Pass as GET or POST parameters:

 * app_token
 * user_token
 * user_secret


Check current user
------------------

*Note the current version of this API is still in progress, and some details may change*

Call:

	*  GET or POST request /api2/current_user.json

Authentication [with app and user](/en/developers/core/webapi2.callauthentication.md) is required.

Get back

	* user object, with details
	* permissions object, listing permissions granted




List Areas
----------

*Note the current version of this API is still in progress, and some details may change*

Call:

  *  GET request for /api2/area/list.json

Authentication [with app and user](/en/developers/core/webapi2.callauthentication.md) is required.

Parameters:

  *  include_deleted - boolean. 




Show Area
---------

*Note the current version of this API is still in progress, and some details may change*

Call:

	*  GET request for /api2/area/xx/info.json

xx is the slug - eg 4

Authentication [with app and user](/en/developers/core/webapi2.callauthentication.md) is required.






Edit Area
---------

*Note the current version of this API is still in progress, and some details may change*

Call:

	*  POST request to /api2/area/xx/info.json

xx is the slug - eg 4

Authentication [with app and user](/en/developers/core/webapi2.callauthentication.md) is required.


Parameters:

	*  title



List Countries
--------------

*Note the current version of this API is still in progress, and some details may change*

Call:

  *  GET request for /api2/country/list.json

Authentication [with app and user](/en/developers/core/webapi2.callauthentication.md) is required.

This returns a list of countries this calendar has currently enabled, 
and not all countries available to be enabled.




Show Country
------------

*Note the current version of this API is still in progress, and some details may change*

Call:

  *  GET request for /api2/country/xx/info.json

xx is the two character country code - eg GB

Authentication [with app and user](/en/developers/core/webapi2.callauthentication.md) is required.

# Web API 2 - Edit Event

_Note the current version of this API is still in progress, and some details may change_

Call:

  *  POST request to /api2/event/xx/info.json

xx is the slug - eg 4

Authentication [with app and user](/en/developers/core/webapi2.callauthentication.md) is required.


Parameters:

  *  summary
  *  description
  *  url
  *  ticket_url



List Events
-----------

*Note the current version of this API is still in progress, and some details may change*

Call:

	*  GET request for /api2/event/list.json

Authentication [with app and user](/en/developers/core/webapi2.callauthentication.md) is required.

Parameters:

	*  include_deleted - boolean. 



Show Event
----------

Call:

  *  GET request for /api2/event/xx/info.json

Authentication [with app and user](/en/developers/core/webapi2.callauthentication.md) is required.

xx is the slug - eg 4





Edit Group
----------

*Note the current version of this API is still in progress, and some details may change*

Call:

  *  POST request to /api2/group/xx/info.json

xx is the slug - eg 4

Authentication [with app and user](/en/developers/core/webapi2.callauthentication.md) is required.


Parameters:

  *  title
  *  description
  *  url






List Groups
-----------

*Note the current version of this API is still in progress, and some details may change*

Call:

*  GET request for /api2/group/list.json

Authentication [with app and user](/en/developers/core/webapi2.callauthentication.md) is required.

Parameters:

*  include_deleted - boolean. 




Show Group
----------

*Note the current version of this API is still in progress, and some details may change*

Call:

  *  GET request for /api2/group/xx/info.json

Authentication [with app and user](/en/developers/core/webapi2.callauthentication.md) is required.

xx is the slug - eg 4





Edit Venue
----------

*Note the current version of this API is still in progress, and some details may change*

Call:
  *  POST request to /api2/venue/xx/info.json

xx is the slug - eg 4

Authentication [with app and user](/en/developers/core/webapi2.callauthentication.md) is required.


Parameters:
  *  title
  *  description
  *  address
  *  address_code
  *  lat & lng - these must be specified together

List Venues
-----------

Call:

	*  GET request for /api2/venue/list.json

Authentication [with app and user](/en/developers/core/webapi2.callauthentication.md) is required.

Parameters:

	*  include_deleted - boolean. 



Show Venue
----------

Call:

  *  GET request for /api2/venue/xx/info.json

xx is the slug - eg 4

Authentication [with app and user](/en/developers/core/webapi2.callauthentication.md) is required.







