# Method to host laravel project in Cpanel

![image](https://user-images.githubusercontent.com/29918977/192233624-f3d7c928-4fe2-45fb-b0fe-67af648b88a6.png)

Make one folder that contain laravel files. Here abcd is folder name
Make another file called .htaccess

```
RewriteCond %{HTTP_HOST} ^abc.np$ [NC,OR]   //replace host name
RewriteCond %{HTTP_HOST} ^www.abc.np$       //replace host name
RewriteCond %{REQUEST_URI} !abcd/public/        //replace folder name
RewriteRule (.*) /abcd/public/$1 [L]            //replace folder name

````

![image](https://user-images.githubusercontent.com/29918977/192234216-c434380a-0d62-41a9-811c-a19c061f966c.png)


## This is the code of .htaccess

```


RewriteEngine on
RewriteCond %{HTTP_HOST} ^abc.np$ [NC,OR]
RewriteCond %{HTTP_HOST} ^www.abc.np$
RewriteCond %{REQUEST_URI} !abcd/public/
RewriteRule (.*) /abcd/public/$1 [L]

RewriteEngine On
RewriteCond %{HTTPS} off
RewriteRule ^(.*)$ https://%{HTTP_HOST}%{REQUEST_URI} [L,R=301]

AddOutputFilterByType DEFLATE text/plain
AddOutputFilterByType DEFLATE text/html
AddOutputFilterByType DEFLATE text/xml
AddOutputFilterByType DEFLATE text/css
AddOutputFilterByType DEFLATE application/xml
AddOutputFilterByType DEFLATE application/xhtml+xml
AddOutputFilterByType DEFLATE application/rss+xml
AddOutputFilterByType DEFLATE application/javascript
AddOutputFilterByType DEFLATE application/x-javascript

<ifModule mod_gzip.c>
    mod_gzip_on Yes
    mod_gzip_dechunk Yes
    mod_gzip_item_include file .(html?|txt|css|js|php)$
    mod_gzip_item_include handler ^cgi-script$
    mod_gzip_item_include mime ^text/.*
    mod_gzip_item_include mime ^application/x-javascript.*
    mod_gzip_item_exclude mime ^image/.*
    mod_gzip_item_exclude rspheader ^Content-Encoding:.*gzip.*
</ifModule>

<IfModule mod_expires.c>
  ExpiresActive on

# Perhaps better to whitelist expires rules? Perhaps.
  ExpiresDefault "access plus 1 month"

# cache.appcache needs re-requests in FF 3.6 (thanks Remy ~Introducing HTML5)
  ExpiresByType text/cache-manifest "access plus 0 seconds"

# Your document html
  ExpiresByType text/html "access plus 0 seconds"

# Data
  ExpiresByType text/xml "access plus 0 seconds"
  ExpiresByType application/xml "access plus 0 seconds"
  ExpiresByType application/json "access plus 0 seconds"

# Feed
  ExpiresByType application/rss+xml "access plus 1 hour"
  ExpiresByType application/atom+xml "access plus 1 hour"

# Favicon (cannot be renamed)
  ExpiresByType image/x-icon "access plus 1 week"

# Media: images, video, audio
  ExpiresByType image/gif "access plus 1 month"
  ExpiresByType image/png "access plus 1 month"
  ExpiresByType image/jpg "access plus 1 month"
  ExpiresByType image/jpeg "access plus 1 month"
  ExpiresByType video/ogg "access plus 1 month"
  ExpiresByType audio/ogg "access plus 1 month"
  ExpiresByType video/mp4 "access plus 1 month"
  ExpiresByType video/webm "access plus 1 month"

# HTC files (css3pie)
  ExpiresByType text/x-component "access plus 1 month"

# Webfonts
  ExpiresByType application/x-font-ttf "access plus 1 month"
  ExpiresByType font/opentype "access plus 1 month"
  ExpiresByType application/x-font-woff "access plus 1 month"
  ExpiresByType image/svg+xml "access plus 1 month"
  ExpiresByType application/vnd.ms-fontobject "access plus 1 month"

# CSS and JavaScript
  ExpiresByType text/css "access plus 1 year"
  ExpiresByType application/javascript "access plus 1 year"

  <IfModule mod_headers.c>
    Header append Cache-Control "public"
  </IfModule>

</IfModule>

## EXPIRES CACHING ##
<IfModule mod_expires.c>
ExpiresActive On
ExpiresByType image/jpg "access 1 year"
ExpiresByType image/jpeg "access 1 year"
ExpiresByType image/gif "access 1 year"
ExpiresByType image/png "access 1 year"
ExpiresByType text/css "access 1 month"
ExpiresByType application/pdf "access 1 month"
ExpiresByType application/javascript "access 1 month"
ExpiresByType application/x-javascript "access 1 month"
ExpiresByType application/x-shockwave-flash "access 1 month"
ExpiresByType image/x-icon "access 1 year"
ExpiresDefault "access 2 days"
</IfModule>
# 1 Month for most static assets
<filesMatch ".(css|jpg|jpeg|png|gif|js|ico)$">
Header set Cache-Control "max-age=2592000, public"
</filesMatch>

## EXPIRES CACHING ##

<ifmodule mod_deflate.c>
  # Compress HTML, CSS, JavaScript, Text, XML and fonts
  AddOutputFilterByType DEFLATE image/svg+xml
  AddOutputFilterByType DEFLATE application/javascript
  AddOutputFilterByType DEFLATE application/rss+xml
  AddOutputFilterByType DEFLATE application/vnd.ms-fontobject
  AddOutputFilterByType DEFLATE application/x-font
  AddOutputFilterByType DEFLATE application/x-font-opentype
  AddOutputFilterByType DEFLATE application/x-font-otf
  AddOutputFilterByType DEFLATE application/x-font-truetype
  AddOutputFilterByType DEFLATE application/x-font-ttf
  AddOutputFilterByType DEFLATE application/x-javascript
  AddOutputFilterByType DEFLATE application/xhtml+xml
  AddOutputFilterByType DEFLATE application/xml
  AddOutputFilterByType DEFLATE font/opentype
  AddOutputFilterByType DEFLATE font/otf
  AddOutputFilterByType DEFLATE font/ttf
  AddOutputFilterByType DEFLATE image/x-icon
  AddOutputFilterByType DEFLATE text/css
  AddOutputFilterByType DEFLATE text/html
  AddOutputFilterByType DEFLATE text/javascript
  AddOutputFilterByType DEFLATE text/plain
  AddOutputFilterByType DEFLATE text/xml
  # Remove browser bugs (only needed for really old browsers)
  BrowserMatch ^Mozilla/4 gzip-only-text/html
  BrowserMatch ^Mozilla/4\.0[678] no-gzip
  BrowserMatch \bMSIE !no-gzip !gzip-only-text/html
  Header append Vary User-Agent
</ifmodule>
# compress text, html, javascript, css, xml:
AddOutputFilterByType DEFLATE text/plain
AddOutputFilterByType DEFLATE text/html
AddOutputFilterByType DEFLATE text/xml
AddOutputFilterByType DEFLATE text/css
AddOutputFilterByType DEFLATE application/xml
AddOutputFilterByType DEFLATE application/xhtml+xml
AddOutputFilterByType DEFLATE application/rss+xml
AddOutputFilterByType DEFLATE application/javascript
AddOutputFilterByType DEFLATE application/x-javascript

# Or, compress certain file types by extension:
<files *.html>
SetOutputFilter DEFLATE
</files>


# RewriteEngine on
# RewriteCond %{HTTP_HOST} ^mahendra\.hamropaathshala\.com [NC]
# RewriteRule ^(.*)$ /newschool/public/$1 [L]

# BEGIN cPanel-generated php ini directives, do not edit
# Manual editing of this file may result in unexpected behavior.
# To make changes to this file, use the cPanel MultiPHP INI Editor (Home >> Software >> MultiPHP INI Editor)
# For more information, read our documentation (https://go.cpanel.net/EA4ModifyINI)
<IfModule php7_module>
   php_flag display_errors Off
   php_value max_execution_time 30
   php_value max_input_time 60
   php_value max_input_vars 1000
   php_value memory_limit 5024M
   php_value post_max_size 300M
   php_value session.gc_maxlifetime 1440
   php_value session.save_path "/var/cpanel/php/sessions/ea-php74"
   php_value upload_max_filesize 300M
   php_flag zlib.output_compression On
</IfModule>
<IfModule lsapi_module>
   php_flag display_errors Off
   php_value max_execution_time 30
   php_value max_input_time 60
   php_value max_input_vars 1000
   php_value memory_limit 5024M
   php_value post_max_size 300M
   php_value session.gc_maxlifetime 1440
   php_value session.save_path "/var/cpanel/php/sessions/ea-php74"
   php_value upload_max_filesize 300M
   php_flag zlib.output_compression On
</IfModule>
# END cPanel-generated php ini directives, do not edit

# php -- BEGIN cPanel-generated handler, do not edit
# Set the “ea-php72” package as the default “PHP” programming language.
<IfModule mime_module>
  AddHandler application/x-httpd-ea-php72 .php .php7 .phtml
</IfModule>
# php -- END cPanel-generated handler, do not edit

