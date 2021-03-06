Calendars
=========


Creating a calendar
-------------------

.. image:: /images/calender4.png

If you use the calendar the first time,
there will be already a calendar called ‘Default calendar’. You can
manage your calendars with a click on the ``Calendar`` button in the top
right corner. In the dialog, which will appear, you can add, edit,
export, enable, disable and delete your calendars. There will be also a
link for ``CalDav access``.

Synchronising Calendars with CalDav
-----------------------------------
.. image:: /images/calender1.png

You can access your calendars with every CalDAV-compatible
program, i.e. Kontact, Evolution, Thunderbird.

CalDAV-url: http://ADDRESS/apps/calendar/caldav.php .

To use ownCloud
with iCal you will need to use the following url:

CalDAV-url: http://ADDRESS/apps/calendar/caldav.php/principals/username/

Don’t forget the trailing slash! On Mozilla Lightning you need to use the URL: https://ADDRESS/remote.php/caldav/calendars/USERNAME/CALENDARNAME


*Note:the calendar name must be URL-encoded. The default calendar is ``default%20calendar``.*

Creating events
---------------

.. image:: /images/calender2.png

To create an event just click on the date in the
month view or choose the timeframe in the weekview. In the dialog which
will appear you can enter your information like title, category, etc.
With the advanced options you can set the description, the location and
the repetition rate of an event. If the repeating should end you can
choose between setting the end by date or by occurrences. If you choose
in the weekview all days from Monday to Friday it will automatically set
the repeat rule to ‘every weekday’. If the interval of the weekview can
be devided by two it automatically set the repeat rule to ‘Bi-Weekly’.

Exporting / Importing events
----------------------------

Export
~~~~~~

.. image:: /images/calender5.png

You can export either a single event or a
whole calendar. If you want to export a single event click on it and
press the export button in the bottom right corner. If you want to
export a whole calendar use the ‘Calendar’ button as described in the
chapter ‘Creating a calendar’.

Import
======

.. image:: /images/calender3.png

Import your calenar as ``ical`` file using the
files app. Just click on the calendar file to open the import dialog. You can import the calendar into a new calendar or into an already existing calendar.
::

  Hint: If the progress bar doesn't work properly the folder ``apps/calendar/import_tmp/`` has probably no write permission.


Why is the calendar app asking for my current location?
-------------------------------------------------------

.. image:: /images/calender.png

The calendar needs your current position for detecting your
timezone. Without the correct timezone there will be a time offset
between the events in owncloud and your desktop calendar you synchronise
with owncloud. You can also set the timezone manually in the personal
settings.


