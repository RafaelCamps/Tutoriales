# Configurar un entorno LAMP - Linux Apache Mysql PHP




## Instalar Apache - Servidor WEB

`sudo apt install apache2`  
Si tras cambiar alguna configuración que está en /etc/apache2/ hay que reiniciar el servicio mediante:
`sudo services apache2 restart`  
`sudo /etc/init.d/apache2 restart`


## Instalar PHP

`sudo apt install php`

## Instalar MySql Server

`sudo apt install mysql-server`
- creamos un pass para root

Para poder acceder hay que iniciar el servicio:  
`sudo /etc/init.d/mysql start`


Para restablecer la contraseña del usuario root en MariaDB o MySql  
`sudo /etc/init.d/mysql start` - Iniciamos el servicio mysql  
`sudo mysql secure instalation` - Indicamos que queremos una instalación segura  
`sudo mysql -u root -p ` - Arrancamos mysql 

## Instalar Modulo de mysql para PHP

`sudo apt install php-mysql`


## Instalar PHPMyAdmin

`sudo apt-get install phpmyadmin`
- Indicamos **n** a dbconfig-common
- Indicamos que el tipo de servidor es Apache - 1
- Conectamos al server Mysql - yes
- Indicamos un pass para PHPMyAdmin
- Confirmamos pass
- Indicamos el pass de **root** de mysql-server

El usuario por defecto de phpmyadmin es **root**

Hay que editar el archivo php.ini  
`sudo nano /etc/php/apache2/php.ini`  
- Hay que quitar el **;** en **extension=mysql.so**

También hay que modificar el archivo apache2.conf  
`sudo nano /etc/apache2/apache2.conf`  
- Al final del todo escribimos: `Include /etc/phpmyadmin/apache.conf`





