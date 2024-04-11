# Microservicios
Microservicios con Docker, PHP, MySQL, Apache, AWS SNS
Configuración de Entorno de Desarrollo con Docker y AWS en AWS EC2
Este repositorio contiene los archivos y las instrucciones necesarias para configurar un entorno de desarrollo en AWS EC2 utilizando Docker para contener servicios como PHP, MySQL y phpMyAdmin. Además, se integra el SDK de AWS PHP para interactuar con servicios de AWS como SNS.

Pasos de Configuración
1. Actualizar Librerías del Sistema
bash
Copy code
sudo yum update -y
2. Instalar Docker
bash
Copy code
sudo yum install -y docker
3. Iniciar Docker
bash
Copy code
sudo service docker start
4. Añadir Usuario al Grupo Docker
bash
Copy code
sudo usermod -a -G docker $(whoami)
5. Instalar pip3 (si es necesario)
bash
Copy code
sudo yum install -y python3-pip
6. Descargar y Configurar docker-compose
bash
Copy code
sudo curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose

sudo chmod +x /usr/local/bin/docker-compose

docker-compose --version
7. Instalar PHP y Composer
bash
Copy code
sudo yum install php php-cli php-json php-mbstring -y

sudo php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
sudo php composer-setup.php --install-dir=/usr/local/bin --filename=composer
sudo php -r "unlink('composer-setup.php');"
8. Descargar e Instalar AWS SDK for PHP
bash
Copy code
cd /home/ec2-user/proyecto
sudo php composer.phar require aws/aws-sdk-php
9. Configurar Docker Compose
bash
Copy code
cd /home/ec2-user/proyecto
nano docker-compose.yml
Copiar y pegar el contenido del archivo docker-compose.yml proporcionado en este repositorio.

10. Crear Archivos de PHP y HTML
bash
Copy code
cd /home/ec2-user/proyecto/html
nano index.html
Copiar y pegar el contenido del archivo index.html proporcionado en este repositorio.

bash
Copy code
nano submit.php
Copiar y pegar el contenido del archivo submit.php proporcionado en este repositorio.

11. Crear Dockerfile para PHP
bash
Copy code
cd /home/ec2-user/proyecto/php
nano Dockerfile
Copiar y pegar el contenido del archivo Dockerfile proporcionado en este repositorio.

12. Crear Archivo SQL para Crear Tabla
bash
Copy code
cd /home/ec2-user/proyecto
nano create_table.sql
Copiar y pegar el contenido del archivo create_table.sql proporcionado en este repositorio.

13. Ejecutar Docker Compose
bash
Copy code
cd /home/ec2-user/proyecto
docker-compose up -d
Acceso a Servicios
Una vez que Docker Compose esté en funcionamiento, puede acceder a los siguientes servicios:

Aplicación Web: Visite http://<public_ip> en su navegador.
phpMyAdmin: Visite http://<public_ip>:8080 en su navegador para administrar la base de datos MySQL.
¡Ahora tienes un entorno de desarrollo funcional configurado en AWS EC2 utilizando Docker! Asegúrate de reemplazar <public_ip> con la dirección IP pública de tu instancia EC2. Si tienes alguna pregunta o encuentras algún problema durante la configuración, no dudes en contactarme.

¡Disfruta codificando en la nube con AWS y Docker! 🚀

