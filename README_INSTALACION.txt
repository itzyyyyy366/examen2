PROYECTO 2 - SERVIDOR WEB EN GNU/LINUX

1) Instalar paquetes LAMP en Ubuntu:
   sudo apt update
   sudo apt install apache2 mysql-server php libapache2-mod-php php-mysql -y

2) Verificar servicios:
   sudo systemctl status apache2
   sudo systemctl status mysql

3) Copiar el contenido de esta carpeta al servidor web:
   sudo rm -rf /var/www/html/*
   sudo cp -R ./* /var/www/html/
   sudo chown -R www-data:www-data /var/www/html
   sudo chmod -R 755 /var/www/html

4) Probar en el navegador del servidor:
   http://localhost
   o
   http://127.0.0.1

5) Configurar IP estática con Netplan (adaptar interfaz/IP/gateway/DNS al equipo):
   sudo nano /etc/netplan/00-installer-config.yaml

   Ejemplo:
   network:
     version: 2
     ethernets:
       enp0s3:
         dhcp4: no
         addresses:
           - 192.168.1.50/24
         routes:
           - to: default
             via: 192.168.1.1
         nameservers:
           addresses: [8.8.8.8, 1.1.1.1]

   Aplicar:
   sudo netplan apply
   ip a

IMPORTANTE: sustituir enp0s3 y las direcciones por las que correspondan a la máquina virtual.
