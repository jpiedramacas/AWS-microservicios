### Requisitos Previos:

1. **Instancia de AWS EC2**: Necesitas una instancia de AWS EC2 en ejecución. Asegúrate de tener acceso a esta instancia a través de SSH y que tenga los permisos necesarios para instalar software.

2. **Acceso de Usuario**: Debes tener acceso como usuario con permisos sudo en la instancia EC2 para poder instalar Docker y otras herramientas.

3. **Puertos Abiertos**: Asegúrate de tener los puertos necesarios abiertos en el grupo de seguridad de la instancia EC2 para permitir el tráfico HTTP (puerto 80) y acceso a phpMyAdmin (puerto 8080) desde tu dirección IP o cualquier otra fuente necesaria.

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

8. **Descarga el Repositorio y Configura el Entorno**:

   Clona tu repositorio que contiene los archivos `docker-compose.yml`, `index.html`, `submit.php`, `Dockerfile`, y `create_table.sql` en la instancia EC2. Asegúrate de ubicarte en el directorio donde deseas almacenar estos archivos.

9. **Ejecuta Docker Compose**:

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
