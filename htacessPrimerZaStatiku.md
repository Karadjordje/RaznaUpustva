Primer izgleda .htaccess fajla za staticki sajt

Kod ispod ce resiti:
1. Leverage browser caching
2. Enable gzip compression
3. Ima mali dodatak koji resava ETag
4. Ima deo za bezbednost sajta
Ubrzace vas sajt i povecace vam ocenu


## EXPIRES CACHING ##
    <IfModule mod_expires.c>
        # Enable expirations
        ExpiresActive On 
        # Default directive
        ExpiresDefault "access plus 1 month"

        ExpiresActive On
        ExpiresByType image/jpg "access plus 1 year"
        ExpiresByType image/jpeg "access plus 1 year"
        ExpiresByType image/gif "access plus 1 year"
        ExpiresByType image/png "access plus 1 year"
        ExpiresByType text/css "access plus 1 month"
        ExpiresByType application/pdf "access plus 1 month"
        ExpiresByType application/javascript "access plus 1 year"
        ExpiresByType text/x-javascript "access plus 1 month"
        ExpiresByType application/x-shockwave-flash "access plus 1 month"
        ExpiresByType image/x-icon "access plus 1 year"
    </IfModule>

## EXPIRES CACHING ##
    <IfModule mod_deflate.c>
        # Compress HTML, CSS, JavaScript, Text, XML and fonts
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
        AddOutputFilterByType DEFLATE image/svg+xml
        AddOutputFilterByType DEFLATE image/x-icon
        AddOutputFilterByType DEFLATE text/css
        AddOutputFilterByType DEFLATE text/html
        AddOutputFilterByType DEFLATE text/javascript
        AddOutputFilterByType DEFLATE text/plain
        AddOutputFilterByType DEFLATE text/xml

        ## Remove browser bugs (only needed for really old browsers) ##
        BrowserMatch ^Mozilla/4 gzip-only-text/html
        BrowserMatch ^Mozilla/4\.0[678] no-gzip
        BrowserMatch \bMSIE !no-gzip !gzip-only-text/html
        Header append Vary User-Agent
    </IfModule>



## This solves Etag problem if needed ##
    Header unset ETag
    FileETag None



# Snipets bellow are for security mostly for wordpress websites #

## Disable unauthorized directory browsing ##
    Options All - Indexes

## Sometimes hackers break into a WordPress site and install a backdoor. These backdoor files are often disguised as core WordPress files and are placed in /wp-includes/ or /wp-content/uploads/ folders. ##
## Save the file and then upload it to your /wp-content/uploads/ and /wp-includes/ directories. ##
    <Files *.php>
        deny from all
    </Files>

## Protect your wp-config.php file from unathorized access, simply add this code to your .htaccess ##
    <files wp-config.php>
        order allow,deny
        deny from all
    </files>

## This blocks users from accessing wp-admin so use it with caution ##
## Protect .htaccess From Unauthorized Access ##
    <files ~ "^.*\.([Hh][Tt][Aa])">
        order allow,deny
        deny from all
        satisfy all
    </files>


## A common technique used in brute force attacks is to run author scans on a WordPress site and then attempt to crack passwords for those usernames. ##
## BEGIN block author scans ##
    RewriteEngine On
    RewriteBase /
    RewriteCond %{QUERY_STRING} (author=\d+) [NC]
    RewriteRule .* - [F]
## END block author scans ##


## Disable the Server Signature ##
    ServerSignature Off


## Block access to multiple file types ##
	<FilesMatch "\.(htaccess|htpasswd|ini|psd|log|sh)$">
    	Order allow, deny
    	Deny from all
	</FilesMatch>
