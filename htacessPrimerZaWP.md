Primer izgleda .htaccess fajla za wordpress sajt<br>
Pored koda ispod treba procitati upustvo na sledecem sajtu:<br>
https://www.hireawiz.com/wordpress-optimization-guide<br>

Kod ispod ce resiti:<br>
1. Leverage browser caching<br>
2. Enable gzip compression<br>
Ubrzace vas sajt i povecace vam ocenu<br>

# BEGIN WordPress
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

# END WordPress
