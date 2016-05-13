bfnar
=====

"Blackfire Next Apache Request." Gets a token from Blackfire and configures Apache to include the X-Blackfire-Query header. I use this to profile gateway -> cloud requests because I don't control the gateway.

Note that it restarts Apache for you.

Setup
-----

Edit `/etc/apache2/sites-enabled/candi-ssl` and add `#RequestHeader set X-Blackfire-Query` in an appropriate location. For example:

    DocumentRoot /var/www/candi
    <Directory />
      Options -Indexes FollowSymLinks
      AllowOverride None
      <ifModule mod_headers.c>
        Header always set X-XSS-Protection "1; mode=block"
        Header always set X-Frame-Options "SAMEORIGIN"
        Header always set X-Content-Type-Options "nosniff"
        Header always set Strict-Transport-Security "max-age=31536000; includeSubDomains"
        #RequestHeader set X-Blackfire-Query
      </ifModule>
    </Directory>


Usage
-----

To add the header:

    sudo path/to/bfnar

To remove the header:

    sudo path/to/bfnar -x
