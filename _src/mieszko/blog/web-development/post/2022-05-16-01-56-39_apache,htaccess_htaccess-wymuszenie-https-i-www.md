<!--t .htaccess - informacje zebrane t-->
<!--d Jeśli chce wymusić **https** i nie mieć przedrostek www w adresie ``` RewriteEngine on RewriteCond %{HTTPS} off RewriteRUle (.*) d-->
<!--tag apache,htaccess tag-->

Jeśli chce wymusić **https** i nie mieć przedrostek www w adresie

```
<IfModule mod_rewrite.c>
RewriteEngine on
RewriteCond %{HTTPS} off
RewriteRUle (.*) https://www.urbanowski.info/$1 [R=301,L]

RewriteCond %{HTTP_HOST} !^www. [NC]
RewriteRule ^ https://www.%{HTTP_HOST}%{REQUEST_URI} [L,R=301]

RewriteCond %{HTTPS_HOST} !^www. [NC]
RewriteRule ^ https://www.%{HTTPS_HOST}%{REQUEST_URI} [L,R=301]

# i przesylam wszystkie zapytania ktore nie sa do plikow lub katalogow do index.php.
RewriteCond %{REQUEST_FILENAME} !-f
RewriteCond %{REQUEST_FILENAME} !-d 
RewriteRule ^ index.php [L]
</IfModule>
```

Jeśli chce wymusić **https** i **mieć** przedrostka www w adresie (to do weryfikacji)

```
<IfModule mod_rewrite.c>
RewriteEngine on
RewriteCond %{HTTPS} off
RewriteRUle (.*) https://urbanowski.info/$1 [R=301,L]

RewriteCond %{HTTP_HOST} ^www.(.+)$ [NC]
RewriteCond %{HTTPS_HOST} ^www.(.+)$ [NC]
RewriteRule ^ https://%1%{REQUEST_URI} [L,R=301]

# i przesylam wszystkie zapytania ktore nie sa do plikow lub katalogow do index.php.
RewriteCond %{REQUEST_FILENAME} !-f
RewriteCond %{REQUEST_FILENAME} !-d 
RewriteRule ^ index.php [L]
</IfModule>
```

Podstawowy plik
```
# BEGIN WordPress
<IfModule mod_rewrite.c>
RewriteEngine On
RewriteBase /
RewriteCond %{REQUEST_FILENAME} !-f
RewriteCond %{REQUEST_FILENAME} !-d
RewriteRule . /index.php [L]
</IfModule>

# END WordPress
```
