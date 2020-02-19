# Curso Raspberry para Programadores :: OpenWebinars
## Capítulo 3: Desarrollo

### Apache + PHP + MYSQL + WORDPRESS

Instalar apache:
```
sudo apt install apache2 -y
```

Instalar mysql:
```
sudo apt-get install mysql-server php-mysql -y
sudo apt-get install mariadb-server-10.0 php-mysql -y
sudo service apache2 restart
```

Instalar PHP:
```
sudo apt install php libapache2-mod-php -y
```

Instalar Wordpress: ir a /var/www/html/
```
sudo wget http://wordpress.org/latest.tar.gz
sudo tar xzf latest.tar.gz
sudo mv wordpress/* .
sudo rm -rf wordpress latest.tar.gz
sudo chown -R www-data: .
```

Configurar MySQL:
```
sudo mysql_secure_installation
```
Al terminar crear base de datos para Wordpress:
```
sudo mysql -uroot -p
create database wordpress;
GRANT ALL PRIVILEGES ON wordpress.* TO 'root'@'localhost' IDENTIFIED BY 'wordpress';
```

Reiniciar apache (sudo service apache2 restart) y cargar la IP de las Raspberry en el navegador (ej.: http://192.168.1.150)

Verás disponible el wizard de configuración de Wordpress para conectar con la base de datos y empezar a gestionar Wordpress.








