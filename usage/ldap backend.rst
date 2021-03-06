LDAP backend
============

 Please find the `documentation for LDAP in **ownCloud 4.5**`_ on the linked page.



Info documentation for LDAP backend version 0.2 (as of ownCloud 4). Setting descriptions are valid for earlier versions.
ownCloud ships an LDAP backend since early one. As of version 0.2 of the
backend resp. ownCloud 4 it does not only contain support for users but
also for groups. The LDAP backend allows full use of ownCloud for user
logging in with LDAP credentials including:

-  File sharing with users and groups
-  Access via WebDAV and of course ownCloud Desktop Client
-  Versioning, external Storages and all other ownCloud Goodies

To connect to an LDAP server the configuration needs to be set up
properly. Once the LDAP backend is activated (*Settings*\ →\ *Apps*,
choose ``LDAP user and group backend``, click on ``Enable``) the
configuration can be found on *Settings*\ →\ *Admin*. Read on for a
detailed description of the configuration fields.

LDAP Basic Settings
~~~~~~~~~~~~~~~~~~~

The basic settings are all you need. However, if you have a larger
directory or custom requirements you want to have a look on the advanced
settings afterwards. The basic part allows you to set up a working
connection to your LDAP server and use it with ownCloud.

.. figure:: /images/ladp1.png
   :align: center
   :alt: ldap-settings-basic

   ownCloud LDAP basic settings

The settings in detail
^^^^^^^^^^^^^^^^^^^^^^

-  **Host**: The hostname of the LDAP server
   *Example: directory.my-company.com*
-  **Base**: The base DN of LDAP, from where all users and groups can be
   reached.
   *Example: dc=my-company,dc=com*
-  **Name**: The name as DN of a user who is able to do searches in the
   LDAP directory. Let it empty for anonymous access. It is recommended
   to have a special system user for ownCloud.
   *Example: uid=owncloudsystemuser,cn=sysusers,dc=my-company,dc=com*
-  **Password**: The password for the user given above. Empty for
   anonymous access.
   *Example: \*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\**
-  **User Login Filter**: The filter to use when a users tries to login.
   Use %uid as placeholder for the username
   *Example: uid=%uid*
-  **User List Filter**: The filter to use when a search for users will
   be executed.
   *Example: objectClass=posixAccount*
-  **Group Filter**: The filter to use when a search for groups will be
   executed.
   *Example: objectClass=posixGroup*

LDAP Advanced Settings
~~~~~~~~~~~~~~~~~~~~~~

In the LDAP Advanced settings section you can define options, that are
less common to set. They are not needed for a working connection, unless
you use a non-standard Port, e.g. It can also have a positive effect on
the performance to specifiy distinguished bases for user and group
searches.

.. figure:: /images/ladp.png
   :align: center
   :alt: ldap-settings-advanced

   ownCloud LDAP advanced settings

The settings in detail
^^^^^^^^^^^^^^^^^^^^^^

-  **Host**: The hostname of the LDAP server
   *Example: directory.my-company.com*
-  **Base**: The base DN of LDAP, from where all users and groups can be
   reached.
   *Example: dc=my-company,dc=com*
-  **Name**: The name as DN of a user who is able to do searches in the
   LDAP directory. Let it empty for anonymous access. It is recommended
   to have a special system user for ownCloud.
   *Example: uid=owncloudsystemuser,cn=sysusers,dc=my-company,dc=com*
-  **Password**: The password for the user given above. Empty for
   anonymous access.
   *Example: \*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\**
-  **User Login Filter**: The filter to use when a users tries to login.
   Use %uid as placeholder for the username
   *Example: uid=%uid*
-  **User List Filter**: The filter to use when a search for users will
   be executed.
   *Example: objectClass=posixAccount*
-  **Group Filter**: The filter to use when a search for groups will be
   executed.
   *Example: objectClass=posixGroup*

LDAP Advanced Settings
~~~~~~~~~~~~~~~~~~~~~~

In the LDAP Advanced settings section you can define options, that are
less common to set. They are not needed for a working connection, unless
you use a non-standard Port, e.g. It can also have a positive effect on
the performance to specifiy distinguished bases for user and group
searches.

.. figure:: http://owncloud.org/wp-content/uploads/2012/05/ldap-settings-advanced-e1337599270841.png
   :align: center
   :alt: ldap-settings-advanced

   ownCloud LDAP advanced settings

The settings in detail
^^^^^^^^^^^^^^^^^^^^^^

-  **Port**: The port LDAP server
   *Example: 389*
-  **Base User Tree**: The base DN of LDAP, from where all users can be
   reached. It needs to be given completely despite to the Base DN from
   the Basic settings.
   *Example: cn=users,dc=my-company,dc=com*
-  **Base Group Tree**: The base DN of LDAP, from where all groups can
   be reached. It needs to be given completely despite to the Base DN
   from the Basic settings.
   *Example: cn=groups,dc=my-company,dc=com*
-  **Group Member association**: The attribute that is used to indicate
   group memberships
   *Example: uniquemember*
-  **Use TLS**: Wether to use TLS encrypted connection to the LDAP
   server
   *Example: [X]*
-  **Case insensitive LDAP server (Windows)**: Wether the LDAP server is
   running on a Windows Host
   *Example: [ ]*
-  **Display Name Field**: The attribute that should be used as ownCloud
   username. ownCloud allows a limited set of characters
   (a-zA-Z0-9.-\_@), every other character will be replaced in ownCloud.
   *Example: displayName*
-  **Quota Attribute**: ownCloud can read an LDAP attribute and set the
   user quota there from. Specify the attribute here, otherwise keep it
   empty.
   *Example: ownCloudQuota*
-  **Quota Default**: Override ownCloud default quota for LDAP users who
   do not have a quota set in the attribute given above.
   *Example: 15 GB*
-  **Email Attribute**: ownCloud can read an LDAP attribute and set the
   user email there from. Specify the attribute here, otherwise keep it
   empty.
   *Example: email*

.. _documentation for LDAP in **ownCloud 4.5**: http://owncloud.org/support/ldap-backend/ldap-backend-in-owncloud-4-5/