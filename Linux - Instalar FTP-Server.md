#Actualizar paquetes
sudo apt update

#Instalar server FTP
sudo apt install vsftpd

#Crear una copia del archivo de conf de vsftpd
sudo cp /etc/vsftpd.conf /etc/vsftpd.conf.original

#Permitir tráfico FTP en el firewall
#Comprobar el estado del firewall
sudo ufw status

#Si da un error, puede que no esté instalado
#Instalar el firewall
sudo apt install ufw
#Hay que iniciar el firewall
sudo ufw enable
#Ahora debe aparecer que está funcionando
sudo ufw status

#Crear reglas para permitir tráfico FTP
sudo ufw allow 20/tcp
sudo ufw allow 21/tcp
sudo ufw allow 990/tcp
sudo ufw allow 40000:50000/tcp

#Permitir tb tráfico para http/s
sudo ufw allow 80/tcp
sudo ufw allow 443/tcp

#Comprobar status firewall
sudo ufw status

#Creamos un usuario, para la transferencia ftp
sudo adduser nombreUsuario
#poner la contraseña


# Crear carpeta FTP
sudo mkdir /home/rcamps/ftp

#Establecer la propiedad de la carpeta
sudo chown nobody:nogroup /home/rcamps/ftp

#Eliminamos los permisos de escritura de esa carpeta
sudo chmod a-w /home/rcamps/ftp

#para comprobar q se han realizado los cambios
sudo ls -la /home/rcamps/ftp

#El resultado debe ser algo así:
total 8
dr-xr-xr-x 2 nobody nogroup 4096 May 14 19:01 .
drwxr-xr-x 9 rcamps rcamps  4096 May 14 19:02 ..

#Creamos el directorio contenedor de archivos y le asignamos propietario
sudo mkdir /home/rcamps/ftp/files
sudo chown rcamps:rcamps /home/rcamps/ftp/files

#Agregamos un archivo a esa carpeta para hacer comprobaciones más adelante.
echo "vsftpd sample file" | sudo tee /home/rcamps/ftp/files/sample.txt


#CONFIGURAR VSFTPD
#Comprobar la configuración
sudo nano /etc/vsftpd.conf

#Eliminar el # en write_enable=YES

#Eliminar el # en chroot_local_user=YES - 
#Para evitar que el usuario acceda a otros directorios

#Añadir un par de líneas, cómo carpeta de destino archivos...
user_sub_token=$USER
local_root=/home/$USER/ftp

#Para permitir una cantidad considerable de conexiones, limitamos los puertos utilizados.
pasv_min_port = 40000
pasv_max_port = 50000

#Crearemos una restricción de usuarios con acceso, solo podrán acceder los que estén en una lista
userlist_enable=YES
userlist_file=/etc/vsftpd.userlist
userlist_deny=NO

#CTRL+X y guardamos los cambios

#Creamos el archivo con la lista de usuarios
echo "rcamps" | sudo tee -a /etc/vsftp.userlist

#verificamos que hemos creado el usuario con
cat /etc/vsftpd.userlist

#Reiniciamos el daemon para cargar los cambios en la configuarción
sudo systemctl restart vsftpd

#HACER QUE FTP SEA SEGURO

#Primero debemos crear un certificado SSL
sudo openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout /etc/ssl/private/vsftpd.pem -out /etc/ssl/private/vsftpd.pem

#Nos pedirá unos datos, que hay q poner...

#Luego abrimos de nuevo el archivo de conf. de vsftpd
sudo nano /etc/vsftpd.conf

#Al final del archivo tiene que haber dos líneas con rsa, hay q comentarlas

#Y creamos estas nuevas
rsa_cert_file=/etc/ssl/private/vsftpd.pem
rsa_private_key_file=/etc/ssl/private/vsftpd.pem

#Ahora hay que cambiar el SSL_enable a YES
ssl_enable=YES

#Estas líneas añaden protección, no permiten conexiones anónimas a través de SSL
allow_anon_ssl=NO
force_local_data_ssl=YES
force_local_logins_ssl=YES

#Configura el servidor para usar TLS
ssl_tlsv1=YES
ssl_sslv2=NO
ssl_sslv3=NO

#Para no ser necesario reutilizar SSL
#Para suites de encriptación de alto cifrado, long igual o superior a 128bits.
require_ssl_reuse=NO
ssl_ciphers=HIGH

#CTRL+X - GUARDAR CAMBIOS

#Reiniciamos de nuevo el daemon, para aplicar las nuevas configuraciones.
sudo systemctl restart vsftpd

#Prueba conexiones con Filezilla

New Site -> ponemos el host 152.25.25.215 port 21
ftp-file Transfer Protocol
use explicit ftp over tls if available

user
password

Conect

Aceptar el certificado SSL y acceder

Ahora debería aparecer el directorio raiz con el archivo de prueba creado.

