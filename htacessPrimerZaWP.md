Primer izgleda .htaccess fajla za wordpress sajt
Pored koda ispod treba procitati upustvo na sledecem sajtu:
https://www.hireawiz.com/wordpress-optimization-guide

Kod ispod ce resiti:
1. Leverage browser caching
2. Enable gzip compression
3. Ima mali dodatak koji resava ETag
4. Ima deo za bezbednost sajta
Ubrzace vas sajt i povecace vam ocenu


## EXPIRES CACHING ##
    <IfModule mod_expires.c>

        ExpiresActive on
        ExpiresDefault                                      "access plus 1 month"

      # CSS
        ExpiresByType text/css                              "access plus 1 year"


      # Data interchange
        ExpiresByType application/atom+xml                  "access plus 1 hour"
        ExpiresByType application/rdf+xml                   "access plus 1 hour"
        ExpiresByType application/rss+xml                   "access plus 1 hour"

        ExpiresByType application/json                      "access plus 0 seconds"
        ExpiresByType application/ld+json                   "access plus 0 seconds"
        ExpiresByType application/schema+json               "access plus 0 seconds"
        ExpiresByType application/vnd.geo+json              "access plus 0 seconds"
        ExpiresByType application/xml                       "access plus 0 seconds"
        ExpiresByType text/xml                              "access plus 0 seconds"


      # Favicon (cannot be renamed!) and cursor images
        ExpiresByType image/vnd.microsoft.icon              "access plus 1 week"
        ExpiresByType image/x-icon                          "access plus 1 week"

      # HTML
        ExpiresByType text/html                             "access plus 0 seconds"

      # JavaScript
        ExpiresByType application/javascript                "access plus 1 year"
        ExpiresByType application/x-javascript              "access plus 1 year"
        ExpiresByType text/javascript                       "access plus 1 year"

      # Manifest files
        ExpiresByType application/manifest+json             "access plus 1 week"
        ExpiresByType application/x-web-app-manifest+json   "access plus 0 seconds"
        ExpiresByType text/cache-manifest                   "access plus 0 seconds"

      # Media files
        ExpiresByType audio/ogg                             "access plus 1 month"
        ExpiresByType image/bmp                             "access plus 1 month"
        ExpiresByType image/gif                             "access plus 1 month"
        ExpiresByType image/jpeg                            "access plus 1 month"
        ExpiresByType image/png                             "access plus 1 month"
        ExpiresByType image/svg+xml                         "access plus 1 month"
        ExpiresByType image/webp                            "access plus 1 month"
        ExpiresByType video/mp4                             "access plus 1 month"
        ExpiresByType video/ogg                             "access plus 1 month"
        ExpiresByType video/webm                            "access plus 1 month"

      # Web fonts
        # Embedded OpenType (EOT)
        ExpiresByType application/vnd.ms-fontobject         "access plus 1 month"
        ExpiresByType font/eot                              "access plus 1 month"

        # OpenType
        ExpiresByType font/opentype                         "access plus 1 month"

        # TrueType
        ExpiresByType application/x-font-ttf                "access plus 1 month"

        # Web Open Font Format (WOFF) 1.0
        ExpiresByType application/font-woff                 "access plus 1 month"
        ExpiresByType application/x-font-woff               "access plus 1 month"
        ExpiresByType font/woff                             "access plus 1 month"

        # Web Open Font Format (WOFF) 2.0
        ExpiresByType application/font-woff2                "access plus 1 month"

      # Other

        ExpiresByType text/x-cross-domain-policy            "access plus 1 week"

    </IfModule>


# Enable gzip and more

	<IfModule mod_rewrite.c>
	RewriteEngine On
		RewriteCond %{HTTP_REFERER} !^http://(.+.)?yourdomain.com/ [NC]
		RewriteCond %{HTTP_REFERER} !^$
		RewriteCond %{HTTP_REFERER} !google. [NC]
		RewriteCond %{HTTP_REFERER} !search?q=cache [NC]
		RewriteCond %{HTTP_REFERER} !msn. [NC]
		RewriteCond %{HTTP_REFERER} !yahoo. [NC]
		RewriteRule .*.(jpe?g|gif|bmp|png|jpg)$ /wp-content/uploads/nohotlink.jpg [L]
		RewriteBase /
		RewriteRule ^index\.php$ - [L]
		RewriteCond %{REQUEST_FILENAME} !-f
		RewriteCond %{REQUEST_FILENAME} !-d
		RewriteRule . /index.php [L]
	</IfModule>

	<IfModule mod_deflate.c>
		AddOutputFilterByType DEFLATE text/html
		AddOutputFilterByType DEFLATE text/css
		AddOutputFilterByType DEFLATE text/javascript
		AddOutputFilterByType DEFLATE text/xml
		AddOutputFilterByType DEFLATE text/plain
		AddOutputFilterByType DEFLATE image/x-icon
		AddOutputFilterByType DEFLATE image/svg+xml
		AddOutputFilterByType DEFLATE application/rss+xml
		AddOutputFilterByType DEFLATE application/javascript
		AddOutputFilterByType DEFLATE application/x-javascript
		AddOutputFilterByType DEFLATE application/xml
		AddOutputFilterByType DEFLATE application/xhtml+xml
		AddOutputFilterByType DEFLATE application/x-font
		AddOutputFilterByType DEFLATE application/x-font-truetype
		AddOutputFilterByType DEFLATE application/x-font-ttf
		AddOutputFilterByType DEFLATE application/x-font-otf
		AddOutputFilterByType DEFLATE application/x-font-opentype
		AddOutputFilterByType DEFLATE application/vnd.ms-fontobject
		AddOutputFilterByType DEFLATE font/ttf
		AddOutputFilterByType DEFLATE font/otf
		AddOutputFilterByType DEFLATE font/opentype
		# For Olders Browsers Which Can't Handle Compression
		BrowserMatch ^Mozilla/4 gzip-only-text/html
		BrowserMatch ^Mozilla/4\.0[678] no-gzip
		BrowserMatch \bMSIE !no-gzip !gzip-only-text/html
	</IfModule>

# END Snippet



## Send the CORS header for images when browsers request it. ##
    <IfModule mod_setenvif.c>
        <IfModule mod_headers.c>
            <FilesMatch "\.(bmp|cur|gif|ico|jpe?g|png|svgz?|webp)$">
                SetEnvIf Origin ":" IS_CORS
                Header set Access-Control-Allow-Origin "*" env=IS_CORS
            </FilesMatch>
        </IfModule>
    </IfModule>

## Allow cross-origin access to web fonts. ##
    <IfModule mod_headers.c>
        <FilesMatch "\.(eot|otf|tt[cf]|woff2?)$">
            Header set Access-Control-Allow-Origin "*"
        </FilesMatch>
    </IfModule>

## Allow cookies to be set from iframes in Internet Explorer. ##
    <IfModule mod_headers.c>
        Header set P3P "policyref=\"/w3c/p3p.xml\", CP=\"IDC DSP COR ADM DEVi TAIi PSA PSD IVAi IVDi CONi HIS OUR IND CNT\""
    </IfModule>

## Serve resources with the proper media types (f.k.a. MIME types). ##
    <IfModule mod_mime.c>

      # Data interchange

        AddType application/atom+xml                        atom
        AddType application/json                            json map topojson
        AddType application/ld+json                         jsonld
        AddType application/rss+xml                         rss
        AddType application/vnd.geo+json                    geojson
        AddType application/xml                             rdf xml


      # JavaScript

        # Normalize to standard type.
        # https://tools.ietf.org/html/rfc4329#section-7.2

        AddType application/javascript                      js


      # Manifest files

        AddType application/manifest+json                   webmanifest
        AddType application/x-web-app-manifest+json         webapp
        AddType text/cache-manifest                         appcache


      # Media files

        AddType audio/mp4                                   f4a f4b m4a
        AddType audio/ogg                                   oga ogg opus
        AddType image/bmp                                   bmp
        AddType image/svg+xml                               svg svgz
        AddType image/webp                                  webp
        AddType video/mp4                                   f4v f4p m4v mp4
        AddType video/ogg                                   ogv
        AddType video/webm                                  webm
        AddType video/x-flv                                 flv

        # Serving `.ico` image files with a different media type
        # prevents Internet Explorer from displaying then as images:
        # https://github.com/h5bp/html5-boilerplate/commit/37b5fec090d00f38de64b591bcddcb205aadf8ee

        AddType image/x-icon                                cur ico


      # Web fonts

        AddType application/font-woff                       woff
        AddType application/font-woff2                      woff2
        AddType application/vnd.ms-fontobject               eot

        # Browsers usually ignore the font media types and simply sniff
        # the bytes to figure out the font type.
        # https://mimesniff.spec.whatwg.org/#matching-a-font-type-pattern
        #
        # However, Blink and WebKit based browsers will show a warning
        # in the console if the following font types are served with any
        # other media types.

        AddType application/x-font-ttf                      ttc ttf
        AddType font/opentype                               otf


      # Other

        AddType application/octet-stream                    safariextz
        AddType application/x-bb-appworld                   bbaw
        AddType application/x-chrome-extension              crx
        AddType application/x-opera-extension               oex
        AddType application/x-xpinstall                     xpi
        AddType text/vcard                                  vcard vcf
        AddType text/vnd.rim.location.xloc                  xloc
        AddType text/vtt                                    vtt
        AddType text/x-component                            htc

    </IfModule>

## Serve all resources labeled as `text/html` or `text/plain` with the media type `charset` parameter set to `UTF-8`. ##
    AddDefaultCharset utf-8

## Serve the following file types with the media type `charset`  parameter set to `UTF-8`. ##
    <IfModule mod_mime.c>
        AddCharset utf-8 .atom \
                         .bbaw \
                         .css \
                         .geojson \
                         .js \
                         .json \
                         .jsonld \
                         .manifest \
                         .rdf \
                         .rss \
                         .topojson \
                         .vtt \
                         .webapp \
                         .webmanifest \
                         .xloc \
                         .xml
    </IfModule>

## Forcing https ##
    <IfModule mod_rewrite.c>
        RewriteEngine On
        RewriteCond %{HTTPS} !=on
        RewriteRule ^(.*)$ https://%{HTTP_HOST}/$1 [R=301,L]
    </IfModule>

## This solves Etag problem if needed ##
    <IfModule mod_headers.c>
        Header unset ETag
    </IfModule>
    FileETag None
    




# Snipets bellow are for security mostly for wordpress websites #

## Disable unauthorized directory browsing ##
    <IfModule mod_autoindex.c>
        Options -Indexes
    </IfModule>

## Block access to all hidden files and directories ##
    <IfModule mod_rewrite.c>
        RewriteEngine On
        RewriteCond %{REQUEST_URI} "!(^|/)\.well-known/([^./]+./?)+$" [NC]
        RewriteCond %{SCRIPT_FILENAME} -d [OR]
        RewriteCond %{SCRIPT_FILENAME} -f
        RewriteRule "(^|/)\." - [F]
    </IfModule>

## Block access to files that can expose sensitive information. ##
    <FilesMatch "(^#.*#|\.(bak|conf|dist|fla|in[ci]|log|psd|sh|sql|sw[op])|~)$">

        # Apache < 2.3
        <IfModule !mod_authz_core.c>
            Order allow,deny
            Deny from all
            Satisfy All
        </IfModule>

        # Apache ≥ 2.3
        <IfModule mod_authz_core.c>
            Require all denied
        </IfModule>

    </FilesMatch>

## Force client-side SSL redirection. ##
    <IfModule mod_headers.c>
        Header always set Strict-Transport-Security "max-age=16070400; includeSubDomains"
    </IfModule>

## Prevent some browsers from MIME-sniffing the response. ##
    <IfModule mod_headers.c>
        Header set X-Content-Type-Options "nosniff"
    </IfModule>

## Remove the `X-Powered-By` response header that: ##
    <IfModule mod_headers.c>
        Header unset X-Powered-By
    </IfModule>



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
