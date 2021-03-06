WebDAV
======

You can access ownCloud directly via WebDAV
-------------------------------------------

Here we will explain how to setup WebDAV access on several Operating
Systems. Some applications only allow you to save to a local folder. By
mounting ownCloud to a local folder, you can get around this issue.As
ownCloud can be installed both in the web servers document root or in a
sub-directory, the shorter placeholder **ADDRESS** will used instead of
the full URL to your ownCloud installation.

-  `GNU/Linux operating systems`_
-  `Dolphin file manager (KDE, Kubuntu)`_
-  `Windows`_
-  `OS X`_

GNU/Linux operating systems
---------------------------

First, as an administrator
~~~~~~~~~~~~~~~~~~~~~~~~~~

#. Install the WebDAV support: ``sudo apt-get install davfs2``
#. Reconfigure davfs2 to allow access to normal users:
   ``sudo dpkg-reconfigure davfs2`` (select *Yes* when prompted)
#. Add the users you want to be able to mount the share to the
   ``davfs2`` group: ``sudo usermod -aG davfs2 <user>``
#. Edit ``/etc/fstab``, and add the following line for each user who
   wants to mount the folder (with your details where appropriate)

   -  For version 1.x:
      ``ADDRESS/webdav/owncloud.php /home/<username>/owncloud davfs user,rw,noauto 0 0``
   -  For version 2.x:
      ``ADDRESS/files/webdav.php /home/<username>/owncloud davfs user,rw,noauto 0 0``

Then, as each user who wants to mount the folder
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

#. Create the folders ``owncloud`` & ``.davfs2`` in your home directory
#. Create the file ``secrets`` inside ``.davfs2``, fill it with the
   following (with your credentials where appropriate)

   -  For version 1.x:
      ``ADDRESS/webdav/owncloud.php <username> <password>``
   -  For version 2.x:
      ``ADDRESS/files/webdav.php <username> <password>``

#. Ensure the file is only writable by you either through the file
   manager, or via ``chmod 600 ~/.davfs2/secrets``
#. Run the command: ``mount ~/owncloud``
#. To automatically mount the folder on login, add the command you used
   in step 4 to ``~/.bashrc``

Known issues:
~~~~~~~~~~~~~

+ Resource temporarily unavailable
    If you experience trouble when you create a file in the directory,
    edit ``/etc/davfs2/davfs2.conf`` and add ``use_locks 0``
+ Certificate warnings
    If you use a self-signed certificate, you will get a warning. If you
    are willing to take the risk of a `man in the middle attack`_, run
    this command instead:
    ``echo "y" | mount ~/owncloud > /dev/null 2>&1``

Dolphin file manager (KDE, Kubuntu)
-----------------------------------

#. Open Dolphin and click on where it says *Network* in the left hand
   *Places* column.
#. Click on the icon labeled *Add a Network Folder*
#. It should come up with *WebDAV* already selected. Make sure it is and
   then click *Next*
#. Enter the following settings:

   -  Name: The name you’ll see in the *Places* bookmark, for example
      *ownCloud*
   -  User: Your ownCloud username you use to log in, for example
      *admin*
   -  Server: Your ownCloud domain name, for example *myowncloud.com*
      (without http:// before or directories afterwards)
   -  Folder: Enter ``/files/webdav.php``
   -  Create icon checkbox: Tick to get a bookmark in the *Places*
      column
   -  Port & Encrypted checkbox: Leave as it is unless you have special
      settings or an SSL certificate.

#. Click *Finish* and enter your ownCloud password

You’re done! You can now save, load, sync files in your ownCloud through
Dolphin and other KDE apps. Awesome!

Windows
-------

Windows XP and Vista should work perfectly fine.In Windows 7, you can
map ownCloud as a network folder.

#. in *Services*, enable the *Webclient* service (might be enabled
   already)
#. in the *Registry*, change
   ``HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\WebClient\Parameters\BasicAuthLevel``
   from 1 to 2. Then restart Webclient service (Mouse right click ->
   Restart)
#. go to *My Computer* ? *Mount Network Drive*

   -  in the *Folder* field type ``ADDRESS/files/webdav.php``
   -  check *Connect using different credentials*

However, you have to repeat step 3 after reboot as Windows 7 will not
mount the network folder correc TRUNCATED! Please download pandoc if you
want to convert large files.

.. _GNU/Linux operating systems: #GNU/Linux
.. _Dolphin file manager (KDE, Kubuntu): #Dolphin
.. _Windows: #Windows
.. _OS X: #OSX
.. _man in the middle attack: http://en.wikipedia.org/wiki/Man-in-the-middle_attack