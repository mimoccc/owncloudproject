iOS – Synchronize iPhone/iPad
=============================




Synchronizing the Calendar
~~~~~~~~~~~~~~~~~~~~~~~~~~

#. Open the settings application.
#. Select Mail, Contacts, Calendars.
#. Select Add Account.
#. Select Other as account type.
#. Select Add CalDAV account.
#. For server, type ``ADDRESS/remote.php/caldav/principals/username``
#. Enter your user name and password.
#. Select Next.
#. If your server does not support SSL, a warning will be displayed.
   Select Continue.
#. If the iPhone is unable to verify the account information perform the
   following:

   -  Select OK.
   -  Select advanced settings.
   -  Make sure Use SSL is set to OFF.
   -  Change port to 80.
   -  Go back to account information and hit Save.

Your calendar should now be visible in the Calendar application

Synchronizing the Address book
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

#. Open the settings application.
#. Select Mail, Contacts, Calendars.
#. Select Add Account.
#. Select Other as account type.
#. Select Add CardDAV account.
#. For server, type ``ADDRESS/remote.php/carddav/principals/username``
#. Enter your user name and password.
#. Select Next.
#. If your server does not support SSL, a warning will be displayed.
   Select Continue.
#. If the iPhone is unable to verify the account information perform the
   following:

   -  Select OK.
   -  Select advanced settings.
   -  Make sure Use SSL is set to OFF.
   -  Change port to 80.
   -  Go back to account information and hit Save.

Now should now find your contacts in the address book of your
iPhone.Problems have been reported for iOS 4.X. A possible solution is
at the `forum`_. 



.. _forum: http://forum.owncloud.org/viewtopic.php?f=3&t=71&p=2211#p2197