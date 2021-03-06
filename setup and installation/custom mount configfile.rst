Custom Mount Configuration
==========================


Since ownCloud version 4 it is possible to configure the filesystem to
mount external storage providers into ownCloud’s virtual filesystem.You
can configure the filesystem by creating and editing
``/config/mount.php``, the configuration file holds a php array
configuring 2 types of entries:

-  Group mounts: each entry configures a mount for each user in group.
-  User mounts: each entry configures a mount for a single user or for
   all users.

For each type, there is an array with the user/group name as key, and an
array of configuration entries as value. Each entry consist of the class
name of the storage backend and an array of backend specific options.
The template ``$user`` can be used in the mount point or backend options. As
of writing the following storage backends are available for use:

-  Local Filesystem
-  FTP
-  Webdav
-  `OpenStack Swift`_
-  SMB (not available in 4.0)

Example:
~~~~~~~~

::

    <?php
    return array(
        'group'=>array(
            'admin'=>array(
                '/$user/files/Admin_Stuff'=>array('class'=>'OC_Filestorage_Local','options'=>array(...)),
            ),
        ),
        'user'=>array(
            'all'=>array(
                '/$user/files/Pictures'=>array('class'=>'OC_Filestorage_DAV','options'=>array(...)),
            ),
            'someuser'=>array(
                '/someuser/files/Music'=>array('class'=>'OC_Filestorage_FTP','options'=>array(...)),
            ),
        )
    );

Backends:
---------

Local Filesystem:
~~~~~~~~~~~~~~~~~

The local filesystem backend mounts a folder on the server into the
virtual filesystem, the class to be used is ``OC_Filestorage_Local`` and
takes the following options:

-  ``datadir`` : the path to the local directory to be mounted.

Ensure that the web server has sufficient permissions on the mounted folder

Example:
~~~~~~~~

``array('class'=>'OC_Filestorage_Local','options'=>array
('datadir'=>'/home/someuser/Music')``

FTP:
~~~~

The FTP backend mounts a folder on a remote FTP server into the virtual
filesystem and is part of the ‘External storage support’ app, the class
to be used is ``OC_Filestorage_FTP`` and takes the following options:

-  ``host``: the hostname of the ftp server.
-  ``user``:the username used to login on the ftp server
-  ``password``: the passwordt to login on the ftp server
-  ``secure``: whether to use ftps:// to connect to the ftp server instead
   of ftp:// (optional, defaults to false)
-  ``root``: the folder inside the ftp server to mount (optional, defaults
   to ‘/’)



PHP needs to be build with FTP support for this backend to work.


Example:
~~~~~~~~

``array('class'=>'OC_Filestorage_FTP,'options'=>array
('host'=>'ftp.myhost.com','user'=>'johndoe','password'=>
'secret','root'=>'/Videos')``

WebDAV:
~~~~~~~

The WebDAV backend mounts a folder on a remote WebDAV server into the
virtual filesystem and is part of the ‘External storage support’ app,
the class to be used is ``OC_Filestorage_DAV``\ and takes the following
options:

-  ``host``: the hostname of the webdav server.
-  ``user``: the username used to login on the webdav server
-  ``password``: the passwordt to login on the webdav server
-  ``secure``: whether to use https:// to connect to the webdav server
   instead of http:// (optional, defaults to false)
-  ``root``: the folder inside the webdav server to mount (optional,
   defaults to ‘/’)

Example:
~~~~~~~~

``array('class'=>'OC_Filestorage_DAV,'options'=>array
('host'=>'myhost.com/webdav.php','user'=>'johndoe',
'password'=>'secret','secure'=>true)``

OpenStack Swift:
~~~~~~~~~~~~~~~~

The Swift backend mounts a container on an OpenStack Object Storage
server into the virtual filesystem and is part of the ‘External storage
support’ app, the class to be used is ``OC_Filestorage_SWIFT``\  and
takes the following options:

-  ``host``: the hostname of the authentication server for the swift
   storage.
-  ``user``: the username used to login on the swift server
-  ``token``: the authentication token to login on the swift server
-  ``secure``: whether to use ftps:// to connect to the swift server instead
   of ftp:// (optional, defaults to false)
-  ``root``: the container inside the swift server to mount (optional,
   defaults to ‘/’)

Example:
~~~~~~~~

``array('class'=>'OC_Filestorage_SWIFT,'options'=>array
('host'=>'swift.myhost.com/auth','user'=>'johndoe',
'token'=>'secret','root'=>'/Videos','secure'=>true)``

SMB:
~~~~

The SMB backend mounts a folder on a remote Samba server into the
virtual filesystem and is part of the ‘External storage support’ app,
the class to be used is ``OC_Filestorage_SMB``\  and takes the following
options:

-  ``host``: the hostname of the samba server.
-  ``user``: the username used to login on the samba server
-  ``password``: the passwordt to login on the samba server
-  ``share``: the share on the samba server to mount
-  ``root``: the folder inside the samba share to mount (optional, defaults
   to ‘/’)

The SMB backend requires ``smbclient`` to be installed on the server and
is currently only available in git



Example:
~~~~~~~~

``array('class'=>'OC_Filestorage_SMB,'options'=>array
('host'=>'myhost.com','user'=>'johndoe','password'=>
'secret','share'=>'/test','/Pictures')``


.. _OpenStack Swift: http://openstack.org/projects/storage/