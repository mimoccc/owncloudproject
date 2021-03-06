Custom user backend configuration
=================================

--------------



Since ownCloud 4.5 it’s possible to configure additional user backends
in ownCloud’s configuration file (config/config.php) using the following
syntax:

::

    'user_backends'=>array(
      array(
        'class'=>...,
        'arguments'=>array(...)
      )
    )

Currently the “External user support” (user\_external) app supports the
provides the following user backends:

IMAP
~~~~

provides authentication against IMAP servers

**Class:**\ OC\_User\_IMAP
 **Arguments:**\ a mailbox string as defined `here`_
 **Example:**

::

    'user_backends'=>array(
      array(
        'class'=>'OC_User_IMAP',
        'arguments'=>array('{imap.gmail.com:993/imap/ssl}INBOX')
      )
    )

 

SMB
~~~

provides authentication against Samba servers

**Class:**\ OC\_User\_SMB
 **Arguments:**\ the samba server to authenticate against
 **Example:**

::

    'user_backends'=>array(
      array(
        'class'=>'OC_User_SMP',
        'arguments'=>array('localhost')
      )
    )

FTP
~~~

provides authentication against FTP servers

**Class:**\ OC\_User\_FTO
 **Arguments:**\ the FTP server to authenticate against
 **Example:**

::

    'user_backends'=>array(
      array(
        'class'=>'OC_User_FTP',
        'arguments'=>array('localhost')
      )
    )



.. _here: http://www.php.net/manual/en/function.imap-open.php