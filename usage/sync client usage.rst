Sync Client Usage
=================


What is Syncing?
----------------

First it is important to recall what syncing is. **Syncing** tries to keep
the files on both repositories the same. That means if a file is added
to one repository it is going to be copied to the other repository. If a
file is changed on one repository, the change is propagated to the other
repository. And also, if a file is deleted on one side, it is deleted on
the other. As a matter of fact, in ownCloud syncing we do not have a
typical client/server system where the server is always master.

This is the major difference to other systems like a file backup where
just changes and new files are propagated but never something is
deleted.

CSync uses file times
---------------------

To decide which file is newer and needs to be synced to the other
repository, "csync" , the underlying sync engine, uses the files
modification times.

The modification timestamp is part of the files metadata. It is
available on every relevant filesystem and is the natural indicator for
a file change.

It does not require special action to create and has a general meaning.
One design goal of csync is to not require a special server component,
that’s why it was used.

To compare the modification times of two files from different systems,
it is needed to operate on the same base. Before version ``1.1.0`` , csync
requires both sides running on the exact same time, which can be
achieved through enterprise standard ``ntp time synchronisation [1]`` on all
machines.

Start ownCloud Client
---------------------

To start ownCloud Client, click on the desktop icon or start it from the
application menu. In the system tray, an ownCloud icon appears.

A left click on the tray icon open a status dialog which gives an
overview on the configured sync folders and allows to add and remove
more sync folder connections as well as pausing a sync connection.

A right click on the tray icon gives other configuration options.

Command line switches
---------------------

ownCloud Client supports the following command line switches:

::

      --logwindow          : open a window to show log output at startup.
      --logfile <filename> : write log output to file .
      --flushlog           : flush the log file after every write.

Config File
-----------

ownCloud Client reads a configuration file which on Linux can be found
at ``$HOME/.local/share/data/ownCloud/owncloud.cfg``

It contains settings in the ini file format known from Windows. Please
note that changes here should be done carefully as wrong settings can
cause disfunctionality.

These are config settings that might be changed:

+ Poll time for the remote repository:                


  ``remotePollInterval`` – Integer value (milliseconds), default 30000  
                                                         
For systems which have notify for local file system changes (Linux  only currently) this is the frequency it polls for remote changes. The following two values are ignored.

+ Poll time for local repository and exeed factor:

  ``localPollInterval`` – Integer value (milliseconds), default: 10000

For systems which poll the local file system (currently Win and Mac)
this is the frequency they poll locally. The remotePollInterval is
ignored on these systems.

+ Poll Timer Exceed Factor:

  ``PollTimerExceedFactor`` – Integer value, default 10

The exceed factor is the factor after which a remote poll is done. That
means the effective frequency for remote poll is ``localPollInterval pollTimerExceedFactor``

+ Maximum Log lines:

   The maximum count of log lines shown in the log window.
   ``maxLogLines`` , Default 20000

