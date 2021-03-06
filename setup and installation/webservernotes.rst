Webserver Notes
===============


nginx configuration
-------------------

-  You need to insert the following code into
   ``your nginx config file.``
-  Adjust ``server_name``, ``root``, ``ssl_certificate`` and
   ``ssl_certificate_key`` to suit your needs.
-  Make sure your ssl certificates are readable by the server (see
   `http://wiki.nginx.org/HttpSslModule`_).



::

    # redirect http to https.
    server {
      listen 80;
      server_name owncloud.example.org;
      rewrite ^ https://$server_name$request_uri? permanent;  # enforce https
    }

    # owncloud (ssl/tls)
    server {
      listen 443 ssl;
      ssl_certificate /etc/nginx/certs/server.crt;
      ssl_certificate_key /etc/nginx/certs/server.key;
      server_name owncloud.example.org;
      root /path/to/owncloud;
      index index.php;
      client_max_body_size 1000M; # set maximum upload size

      # deny direct access
      location ~ ^/(data|config|\.ht|db_structure\.xml|README) {
        deny all;
      }

      # default try order
      location / {
        try_files $uri $uri/ @webdav;
      }

      # owncloud WebDAV
      location @webdav {
        fastcgi_split_path_info ^(.+\.php)(/.*)$;
        fastcgi_pass 127.0.0.1:9000; # or use php-fpm with: "unix:/var/run/php-fpm/php-fpm.sock;"
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
        fastcgi_param HTTPS on;
        include fastcgi_params;
      }

      # enable php
      location ~ \.php$ {
        fastcgi_pass 127.0.0.1:9000; # or use php-fpm with: "unix:/var/run/php-fpm/php-fpm.sock;"
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
        fastcgi_param HTTPS on;
        include fastcgi_params;
      }
    } 

WARNING: You can use Owncloud without SSL/TLS support, but we strongly
encourage you not to do that:

-  Remove the server block containing the redirect
-  Change ``listen 443 ssl`` to ``listen 80;``
-  Remove ``ssl_certificate`` and ``ssl_certificate_key``.
-  Remove ``fastcgi_params HTTPS on;``

*NOTE: If you want to effectively increase maximum upload size you will
also have to modify your ``php-fpm configuration`` (``usually at
/etc/php5/fpm/php.ini``) and increase ``upload\_max\_filesize`` and
``post\_max\_size`` values. You’ll need to restart php5-fpm and nginx
services in order these changes to be applied.*

lighttpd
--------

If you want to use lighttpd, we expect you to know how to install a php
web app. |;)|\  Just a little advice: As .htaccess files are ignored by
lighttpd, you have to secure the /data folder by yourself, otherwise
your ``owncloud.db``` database and user data is puplicly readable even if
directory listing is off. Add these snippets to your lighttpd config
file:

Disable access to data folder
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

::

    $HTTP["url"] =~ "^/owncloud/data/" {
         url.access-deny = ("")
       }

Disable directory listing
~~~~~~~~~~~~~~~~~~~~~~~~~

::

    $HTTP["url"] =~ "^/owncloud($|/)" {
         dir-listing.activate = "disable"
       }

yaws
----

Basic Configuration
~~~~~~~~~~~~~~~~~~~

This should be in your ``yaws\_server.conf``. In the config the
``dir\_listings = false`` is important and also the redirect from ``/data``
to somewhere else, because files will be saved in this directory and it
should not be accessable from the outside.

::

    <server owncloud.myserver.com/>
            port = 80
            listen = 0.0.0.0
            docroot = /var/www/owncloud/src
            allowed_scripts = php
            php_handler = <cgi, /usr/local/bin/php-cgi>
            errormod_404 = yaws_404_to_index_php
            access_log = false
            dir_listings = false
            <redirect>
                    /data == /
            </redirect>
    </server>

Custom 404 error mod
~~~~~~~~~~~~~~~~~~~~

The apache .htaccess file that comes with ownCloud is configured to
redirect requests to nonexistent pages. To emulate that behaviour, you
need a custom error handler for yaws. See this `github gist for further
instructions`_ on how to create and compile that error handler.

Hiawatha
--------

Add ``WebDAVapp = yes`` to the ownCloud VirtualHost. Users accessing
WebDAV from MacOS will also need to add ``AllowDotFiles = yes``.

Disable access to data folder
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

::

    UrlToolkit {
        ToolkitID = denyData
        Match ^/data DenyAccess
    }

 

pagekite
--------

You can use `pagekite`_ to make your local ownCloud accessible from the
internet.



.. _github gist for further instructions: https://gist.github.com/2200407
.. _pagekite: https://pagekite.net/wiki/Howto/GNULinux/OwnCloud/

.. _`http://wiki.nginx.org/HttpSslModule`: http://wiki.nginx.org/HttpSslModule

.. |;)| image:: http://owncloud.org/wp-includes/images/smilies/icon_wink.gif