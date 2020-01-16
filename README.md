# WordPress-Multisite
/* Multisite */
Если же у вас уже есть WordPress-сайт и вы хотите превратить его в мультисайт, то вам необходимо будет внести изменения в wp-config.php файл. И добавить следующий код:
define('WP_ALLOW_MULTISITE', true);
После установки, вы увидите окно “Создать сеть сайтов на WordPress”, где WordPress подскажет, какой код необходимо дополнительно добавить в wp-config.php и .htacсess файл.

При выборе создания сайтов в подпапках, код для wp-config.php выглядит так:

define('MULTISITE', true);
define('SUBDOMAIN_INSTALL', false);
define('DOMAIN_CURRENT_SITE', 'domain.com');
define('PATH_CURRENT_SITE', '/');
define('SITE_ID_CURRENT_SITE', 1);
define('BLOG_ID_CURRENT_SITE', 1);

Код для .htaccess файла:

RewriteEngine On
RewriteBase /
RewriteRule ^index\.php$ - [L]

# add a trailing slash to /wp-admin
RewriteRule ^([_0-9a-zA-Z-]+/)?wp-admin$ $1wp-admin/ [R=301,L]

RewriteCond %{REQUEST_FILENAME} -f [OR] RewriteCond %{REQUEST_FILENAME} -d
RewriteRule ^ - [L] RewriteRule ^([_0-9a-zA-Z-]+/)?(wp-(content|admin|includes).*) $2 [L] RewriteRule ^([_0-9a-zA-Z-]+/)?(.*\.php)$ $2 [L] RewriteRule . index.php [L]

Если же вы выбрали поддомены, то необходимо будет добавить следующий код в wp-config.php:

define('MULTISITE', true);
define('SUBDOMAIN_INSTALL', true);
define('DOMAIN_CURRENT_SITE', 'domain.com');
define('PATH_CURRENT_SITE', '/');
define('SITE_ID_CURRENT_SITE', 1);
define('BLOG_ID_CURRENT_SITE', 1);

Код для .htaccess:

RewriteEngine On
RewriteBase /
RewriteRule ^index\.php$ - [L]

# add a trailing slash to /wp-admin
RewriteRule ^wp-admin$ wp-admin/ [R=301,L]

RewriteCond %{REQUEST_FILENAME} -f [OR] RewriteCond %{REQUEST_FILENAME} -d
RewriteRule ^ - [L] RewriteRule ^(wp-(content|admin|includes).*) $1 [L] RewriteRule ^(.*\.php)$ $1 [L] RewriteRule . index.php [L]




