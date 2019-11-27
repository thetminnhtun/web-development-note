# Hosting Laravel on DigitalOcean

### Enviroment Setup
- Check Updates for Packages
- Nginx (Web Server)
- PHP 
- MySQL
- Composer
- Git (included)
- NPM (optional)

### Check Updates for Packages

```
apt update
apt upgrade
```

### Nginx

```
apt install nginx -y
```
After installion Nginx
```
http://server_domain_or_IP
```
Web Document Root
```
cd /var/www/html/
```
Remove nginx default index file
```
rm index.nginx-debian.html
```
Create new index file
```
nano index.html
```
Type blow code
```
<h1>Welcome to our site.</h1>
```
Nginx service command
```
systemctl start nginx 
systemctl stop nginx
systemctl restart nginx
```

### PHP 

```
apt install php-fpm php-mysql
```
Laravel
```
apt install php-mbstring php-xml php-bcmath 
```
Composer
```
apt install curl php-cli php-mbstring git unzip
```
For Laravel and composer
```
apt install php php-curl php-common php-cli php-mysql php-mbstring php-fpm php-bcmath php-xml php-zip -y
```
Testing
```
sudo nano /var/www/html/info.php
```
Type below code to check php whether work or not.
```
<?php
phpinfo();
```
config Nginx to run PHP
```
nano /etc/nginx/sites-available/default
```
add index.php
```
index index.html index.htm index.php;
```
run brower
```
http://server_domain_or_IP/info.php
```

### MySQL

```
apt install mysql-server -y
```
To secure the installation
```
mysql_secure_installation
```
```
VALIDATE PASSWORD PLUGIN can be used to test passwords
and improve security. It checks the strength of password
and allows the users to set only those passwords which are
secure enough. Would you like to setup VALIDATE PASSWORD plugin?

Press y|Y for Yes, any other key for No: 
```
`[Y]`

```
There are three levels of password validation policy:

LOW    Length >= 8
MEDIUM Length >= 8, numeric, mixed case, and special characters
STRONG Length >= 8, numeric, mixed case, special characters and dictionary                  file

Please enter 0 = LOW, 1 = MEDIUM and 2 = STRONG: 1
```
`0` (depend on your system)

```
Set root password? [Y/n] Y
Remove anonymous users? [Y/n] Y
Disallow root login remotely? [Y/n] N
Remove test database and access to it? [Y/n] Y
Reload privilege tables now? [Y/n] Y
```

### Change Mysql User Password

```
mysql -u root
```
check users
```
SELECT user,authentication_string,plugin,host FROM mysql.user;
```
output
```
+------------------+-------------------------------------------+-----------------------+-----------+
| user             | authentication_string                     | plugin                | host      |
+------------------+-------------------------------------------+-----------------------+-----------+
| root             |                                           | auth_socket           | localhost |
| mysql.session    | *THISISNOTAVALIDPASSWORDTHATCANBEUSEDHERE | mysql_native_password | localhost |
| mysql.sys        | *THISISNOTAVALIDPASSWORDTHATCANBEUSEDHERE | mysql_native_password | localhost |
| debian-sys-maint | *CC744277A401A7D25BE1CA89AFF17BF607F876FF | mysql_native_password | localhost |
+------------------+-------------------------------------------+-----------------------+-----------+
4 rows in set (0.00 sec)
```
change password
```
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'your_password';
```
reload all tables
```
FLUSH PRIVILEGES;
```
check user again
```
SELECT user,authentication_string,plugin,host FROM mysql.user;
```
output
```
+------------------+-------------------------------------------+-----------------------+-----------+
| user             | authentication_string                     | plugin                | host      |
+------------------+-------------------------------------------+-----------------------+-----------+
| root             | *3636DACC8616D997782ADD0839F92C1571D6D78F | mysql_native_password | localhost |
| mysql.session    | *THISISNOTAVALIDPASSWORDTHATCANBEUSEDHERE | mysql_native_password | localhost |
| mysql.sys        | *THISISNOTAVALIDPASSWORDTHATCANBEUSEDHERE | mysql_native_password | localhost |
| debian-sys-maint | *CC744277A401A7D25BE1CA89AFF17BF607F876FF | mysql_native_password | localhost |
+------------------+-------------------------------------------+-----------------------+-----------+
4 rows in set (0.00 sec)
```
exit 
```
exit
```
login with password
```
mysql -u root -p
```
### Composer

```
apt install composer
```
Or Latest Version
```
curl -sS https://getComposer.org/installer | sudo php -- --install-dir=/usr/local/bin  --filename=composer
```
run composer after finished installation
```
composer
```

### Laravel

go web document root
```
cd /var/www/html
```
install laravel latest version using composer
```
composer create-project --prefer-dist laravel/laravel blog
```
### Nginx configuration for laravel

remove default config file
```
rm /etc/nginx/sites-available/default
```
create new config file named `default`
```
nano /etc/nginx/sites-available/default
```
Add the following content
```
server {
    listen 80;
    server_name example.com;
    root /var/www/html/blog/public;

    add_header X-Frame-Options "SAMEORIGIN";
    add_header X-XSS-Protection "1; mode=block";
    add_header X-Content-Type-Options "nosniff";

    index index.html index.htm index.php;

    charset utf-8;

    location / {
        try_files $uri $uri/ /index.php?$query_string;
    }

    location = /favicon.ico { access_log off; log_not_found off; }
    location = /robots.txt  { access_log off; log_not_found off; }

    error_page 404 /index.php;

    location ~ \.php$ {
        fastcgi_pass unix:/var/run/php/php7.2-fpm.sock;
        fastcgi_index index.php;
        fastcgi_param SCRIPT_FILENAME $realpath_root$fastcgi_script_name;
        include fastcgi_params;
    }

    location ~ /\.(?!well-known).* {
        deny all;
    }
}
```
Test your new configuration file for syntax errors by typing:
```
nginx -t
```
reload Nginx
```
systemctl reload nginx
```
### Reference

<a herf="https://www.digitalocean.com/community/tutorials/how-to-install-linux-nginx-mysql-php-lemp-stack-ubuntu-18-04" target="_blink">
DigitalOcean</a>

