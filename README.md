### Pasos para Despliegue:

1. **Conéctate a la Instancia EC2**: Utiliza SSH para conectarte a tu instancia EC2 desde tu terminal local:

   ```bash
   ssh -i tu_llave.pem ec2-user@direccion_ip_publica
   ```

   Reemplaza `tu_llave.pem` con la ruta a tu archivo de clave privada y `direccion_ip_publica` con la dirección IP pública de tu instancia EC2.

2. **Actualiza las Bibliotecas del Sistema**:

   ```bash
   sudo yum update -y
   ```

3. **Instala Docker en la Instancia EC2**:

   ```bash
   sudo yum install -y docker
   ```

4. **Inicia el Servicio de Docker**:

   ```bash
   sudo service docker start
   ```

5. **Añade tu Usuario al Grupo Docker**:

   ```bash
   sudo usermod -a -G docker $(whoami)
   ```

   Esto te permite ejecutar comandos de Docker sin necesidad de usar `sudo`.

6. **Instala Docker Compose**:

   ```bash
   sudo curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose

   sudo chmod +x /usr/local/bin/docker-compose

   docker-compose --version
   ```

7. **Instala PHP y Composer**:

   ```bash
   sudo yum install php php-cli php-json php-mbstring -y

   sudo php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
   sudo php composer-setup.php --install-dir=/usr/local/bin --filename=composer
   sudo php -r "unlink('composer-setup.php');"
   ```
   
### AWS SNS (Amazon Simple Notification Service)

Para integrar AWS SNS en tu aplicación PHP, necesitarás los siguientes requisitos:

1. **Cuenta de AWS**: Debes tener una cuenta de AWS y acceso a AWS Management Console.

2. **IAM Role**: Asegúrate de que la instancia EC2 tenga un IAM Role asociado que permita el acceso al servicio SNS. Este rol debería tener al menos permisos para publicar mensajes en el tema SNS.

3. **Tema SNS**: Crea un tema SNS en la consola de AWS y toma nota del ARN del tema. Este ARN se usará en tu aplicación PHP para enviar mensajes al tema.

4. **Región de AWS**: Usa la misma región de AWS en la que has configurado tu tema SNS. Asegúrate de configurar la región adecuada en la inicialización del cliente SNS en tu aplicación PHP.
8. **Ejecuta Docker Compose**:

   Ubícate en el directorio donde se encuentra tu archivo `docker-compose.yml` y ejecuta:

   ```bash
   docker-compose up -d
   ```

   Esto creará y ejecutará los contenedores de Docker según la configuración en `docker-compose.yml`.

10. **Accede a la Aplicación Web y phpMyAdmin**:

    Utiliza el navegador web para acceder a la aplicación web en `http://<direccion_ip_publica>` y a phpMyAdmin en `http://<direccion_ip_publica>:8080`. Reemplaza `<direccion_ip_publica>` con la dirección IP pública de tu instancia EC2.



### Notas Adicionales:

- Asegúrate de reemplazar `<direccion_ip_publica>` con la dirección IP pública de tu instancia EC2 en los archivos `index.html` y `submit.php` donde sea necesario para que funcionen correctamente.

- Asegúrate de tener suficiente espacio en disco y recursos de memoria en tu instancia EC2 para ejecutar los contenedores Docker según los requisitos de las aplicaciones y servicios.

Siguiendo estos pasos y requisitos, deberías poder desplegar y acceder a tu entorno de desarrollo en AWS EC2 utilizando Docker. Asegúrate de realizar pruebas adicionales y ajustes según sea necesario para adaptarse a tus requisitos específicos y optimizar el rendimiento de tu entorno.
