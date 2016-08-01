Web API V1
==========

Introduction
------------

Web API1 is a read only API.

Almost all end points are fully public. Some End points relate to private user information for that user, and a key is part of the URL.

Apart from that, no key, app or authentication is needed to access this API.

Multi Site or Single Site Mode
------------------------------

In Multi Site mode, it is important to note whether you access these on the index domain or an actual calendar.

In Single Site mode, this does not matter.

Common Parameters
-----------------

For end points that return time in a local timezone, the GET parameter "mytimezone" can be passed. This should be:

  *  One of the timezones that is configured for this calendar - it is from a country that is selected.
  *  In this format http://php.net/manual/en/timezones.php eg "Europe/London"


List Events in ATOM format
--------------------------

There are 2 different set of ATOM end points.

One lists events as they are created. This is useful for keeping an eye on a calendar.

The other lists events a certain number of days before they start. This is useful for getting notifications of upcoming events.


Endpoints for a feed as events are created
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

*  /api1/events.create.atom
*  /api1/group/{slug}/events.create.atom
*  /api1/tag/{slug}/events.create.atom
*  /api1/area/{slug}/events.create.atom
*  /api1/venue/{slug}/events.create.atom
*  /api1/venue/virtual/events.create.atom
*  /api1/curatedlist/{slug}/events.create.atom
*  /api1/country/{code}/events.create.atom

Slug should be the number only eg /group/1-the-best should become 1.

Country code is the 2 character code eg GB.

Endpoints for a feed before events
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

*  /api1/events.before.atom
*  /api1/group/{slug}/events.before.atom
*  /api1/tag/{slug}/events.before.atom
*  /api1/area/{slug}/events.before.atom
*  /api1/venue/{slug}/events.before.atom
*  /api1/venue/virtual/events.before.atom
*  /api1/curatedlist/{slug}/events.before.atom
*  /api1/country/{code}/events.before.atom

Slug should be the number only eg /group/1-the-best should become 1.

Country code is the 2 character code eg GB.

Pass the optional parameter "days" to set how many days. Eg:

*  /api1/events.before.atom?days=5


List Events in ICAL format
--------------------------

End Points
^^^^^^^^^^

In Multi Site mode, these end points are accesed on the Site pages:

  *  /api1/events.ical
  *  /api1/group/{slug}/events.ical
  *  /api1/tag/{slug}/events.ical
  *  /api1/area/{slug}/events.ical
  *  /api1/venue/virtual/events.ical
  *  /api1/venue/{slug}/events.ical
  *  /api1/curatedlist/{slug}/events.ical
  *  /api1/country/{code}/events.ical
  *  /api1/person/{username}/events.ical

Slug should be the number only eg /group/1-the-best should become 1.

Country code is the 2 character code eg GB.



List Events in JSON and JSONP format
------------------------------------

Parameters
^^^^^^^^^^

  *  includeMedias - boolean "true" or "false", optional, false by default. Whether to include medias attached to the event.

List Events in JSON format
--------------------------

In Multi Site mode, these end points are accesed on the Site pages:

  *  /api1/events.json
  *  /api1/group/{slug}/events.json
  *  /api1/tag/{slug}/events.json
  *  /api1/area/{slug}/events.json
  *  /api1/venue/virtual/events.json
  *  /api1/venue/{slug}/events.json
  *  /api1/curatedlist/{slug}/events.json
  *  /api1/country/{code}/events.json
  *  /api1/person/{username}/events.json

Slug should be the number only eg /group/1-the-best should become 1.

Country code is the 2 character code eg GB.

List Events in JSONP format
---------------------------

JSONP end points are the same as the JSON end points, except with a ".jsonp" extension.

Pass the GET parameter "callback" to specify what javascript function should be called.

eg:

  *  /api1/events.jsonp?callback=myFunc

Show Event in ICAL
------------------

*  /api1/event/{slug}/info.ical

Slug should be the number only eg /group/1-the-best should become 1.


Show Event in JSON
------------------

In Multi Site mode, this end point is accesed on the Site pages:

*  /api1/event/{slug}/info.json

Slug should be the number only eg /group/1-the-best should become 1.


Show Event in JSONP
-------------------

In Multi Site mode, this end point is accesed on the Site pages:

*  /api1/event/{slug}/info.jsonp

Slug should be the number only eg /group/1-the-best should become 1.

Pass the GET parameter "callback" to specify what javascript function should be called.

List Groups
-----------


In Multi Site mode, this end point is accesed on the Site pages:

*  /api1/groups.json


List Histories in ATOM format
-----------------------------

This lists every edit made to this calendar as it happens. 

Subscribe to this in a app on your phone to be notified of any edits, for instance.

In Multi Site mode, this end point is accesed on the Site pages:

  *  /api1/histories.atom


