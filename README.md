# nginx
Proyecto para correr y configurar nginx en VM con wordpress dentro y certificados SSL

# 1.- Instalar ngix
> sudo apt-get install nginx

Configurar los virtual hosts del nginx

# 2.- Configurar e instalar LEMP

Instalar php fpm

> sudo apt-get install php-fpm php-xml

Descomentar lineas del config file para que lea el php-fpm tambien descomentar los .htaccess

Instalar mysql

> sudo apt-get install mysql-server php-mysql

Descargar e instalar phpmyadmin

https://www.phpmyadmin.net/

Asignar una contraseña a root de mysql

> mysqladmin --user=root password "PASSWORD"

Crear un user para phpmyadmin

Loguearse a mysql

> mysql -u root -p

Crear user

> CREATE USER 'phpmyadmin'@'localhost' IDENTIFIED BY "PASSWORD";

Dar permisos

> GRANT ALL PRIVILEGES ON *.* TO 'phpmyadmin'@'localhost' WITH GRANT OPTION;

# 3.- Instalar y configurar certbot (opcional)
Preparar instalación certbot

> sudo apt-get update
> sudo apt-get install software-properties-common
> sudo add-apt-repository universe
> sudo apt-get update

Instalación certbot

> sudo apt-get install certbot python3-certbot-nginx

Correr certbot

> sudo certbot --nginx

Testear renovación 

> sudo certbot renew --dry-run

# 4.- Wordpress

Instalar dependencias 

> sudo apt install php-fpm php-common php-mbstring php-xmlrpc php-soap php-gd php-xml php-intl php-mysql php-cli php-mcrypt php-ldap php-zip php-curl

Crear DB

> mysql -u root -p
> CREATE DATABASE wordpress;
>CREATE USER 'wordpressuser'@'localhost' IDENTIFIED BY 'new_password_here';
> GRANT ALL ON wordpress.* TO 'wordpressuser'@'localhost' WITH GRANT OPTION;
> FLUSH PRIVILEGES;
> EXIT;

# Bajar e instalar wordpress

> wget https://wordpress.org/latest.tar.gz
> tar -zxvf latest.tar.gz
> sudo mv wordpress/* /var/www/pablo
> sudo find /var/www/pablo -type d -exec chmod 0755 {} \;
> sudo find /var/www/pablo -type f -exec chmod 0644 {} \;

# Configurar wordpress

> cd /var/www/pablo 
> sudo mv wp-config-sample.php wp-config.php
> sudo vim wp-config.php

(Configurar DB_NAME, DB_USER, DB_PASSWORD, DB_HOST)

# Configurar un reverse proxy (opcional)
Agregar un location al virtualhost y agregar http://IP:PUERTO/

https://www.scaleway.com/en/docs/tutorials/nginx-reverse-proxy/

# Configurar load balancer (opcional)
Agregar upstream al bloque http del nginx (upstream)

https://phoenixnap.com/kb/nginx-reverse-proxy

