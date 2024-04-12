
### 1. Instalar Docker
Ya que este paso ya está cubierto en la lista anterior, puedes omitirlo si ya lo has realizado.


### 2. Instalar Docker Compose
Para instalar Docker Compose en tu sistema, puedes seguir los pasos adecuados según tu sistema operativo. Docker Compose es compatible con una variedad de plataformas, incluyendo Linux, macOS y Windows.


1. **Descargar la versión actual de Docker Compose**:
   
   Puedes obtener la última versión de Docker Compose utilizando `curl`. Por ejemplo, para descargar la versión 1.29.2:

   ```bash
   sudo curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
   ```

   Asegúrate de reemplazar `1.29.2` con la versión más reciente si es diferente.

2. **Dar permisos de ejecución al binario de Docker Compose**:
   
   ```bash
   sudo chmod +x /usr/local/bin/docker-compose
   ```

3. **Verificar la instalación**:
   
   Para asegurarte de que Docker Compose se haya instalado correctamente, puedes verificar su versión:

   ```bash
   docker-compose --version
   ```

   Esto debería mostrar la versión instalada de Docker Compose.


### 3. Crear un Tema SNS y Suscribirse
Para crear un tema SNS y suscribirte a él, sigue estos pasos:

#### a. Crear un Tema SNS en la Consola de AWS:
   - Ve al [AWS Management Console](https://console.aws.amazon.com/) y navega a "Simple Notification Service (SNS)".
   - Haz clic en "Create topic".
   - Asigna un nombre descriptivo para el tema y crea el tema.

#### b. Suscribirte al Tema SNS:
   - Después de crear el tema, selecciona el tema recién creado.
   - Haz clic en "Create subscription".
   - Elige el tipo de protocolo para la suscripción (por ejemplo, Email).
   - Proporciona los detalles necesarios (por ejemplo, la dirección de correo electrónico para la suscripción por correo electrónico).

### 4. Crear un Rol en EC2 y Asignar Políticas SNS Full Access
Para crear un rol en EC2 y asignarle políticas de acceso completo a SNS:

#### a. Crear un Rol en IAM:
   - Ve a la [Consola de IAM](https://console.aws.amazon.com/iam/) en AWS.
   - Selecciona "Roles" en el panel de navegación izquierdo y luego haz clic en "Create role".
   - Para el tipo de entidad de confianza, selecciona "AWS service" y luego "EC2".
   - Adjunta una política que permita acceso total a SNS (por ejemplo, `AmazonSNSFullAccess`).

#### b. Asignar el Rol a la Instancia EC2:
   - Una vez que hayas creado el rol, ve a la página de detalles de tu instancia EC2 en la consola de AWS.
   - Haz clic en "Actions" y luego en "Security" > "Modify IAM role".
   - Selecciona el rol que creaste anteriormente y guarda los cambios.

### 5. Ejecutar el Comando `sudo docker-compose up`
Este paso también está cubierto en la lista anterior, así que ejecuta este comando después de haber configurado tus contenedores con Docker Compose.

### 6. Acceder al Formulario y Recibir un Email
Para acceder al formulario y recibir un correo electrónico:

#### a. Acceder al Formulario:
   - Abre un navegador web e ingresa la dirección IP pública de tu instancia EC2 para acceder a tu aplicación web.

#### b. Recibir un Correo Electrónico desde SNS:
   - Envía un mensaje al tema SNS desde tu aplicación PHP utilizando el ARN del tema.
   - Dependiendo de cómo esté configurada tu suscripción (por ejemplo, correo electrónico), deberías recibir un correo electrónico con el mensaje publicado en el tema SNS.

Recuerda ajustar tu código PHP para integrar la funcionalidad de publicación de mensajes en el tema SNS utilizando el SDK de AWS para PHP u otra librería compatible con SNS.

Con estos pasos adicionales, deberías tener un despliegue completo en AWS EC2 con Docker, incluyendo la integración con AWS SNS para el envío de mensajes y correos electrónicos desde tu aplicación PHP.

Para abrir y permitir el tráfico a través de los puertos específicos (HTTP, SSH, 3036 y 8080) en un servidor Linux utilizando comandos en la terminal, generalmente necesitarás utilizar un firewall como `iptables` o `firewalld`, dependiendo de la distribución de Linux que estés utilizando. A continuación te proporciono ejemplos de cómo hacerlo en ambas configuraciones.

### Utilizando `iptables`

`iptables` es una utilidad de firewall estándar en muchas distribuciones de Linux. Puedes abrir y permitir el tráfico en los puertos necesarios utilizando los siguientes comandos:

#### 1. Abrir Puertos HTTP (80), SSH (22), 3036 y 8080:

```bash
# Permitir tráfico HTTP (puerto 80)
sudo iptables -A INPUT -p tcp --dport 80 -j ACCEPT

# Permitir tráfico SSH (puerto 22)
sudo iptables -A INPUT -p tcp --dport 22 -j ACCEPT

# Permitir tráfico en puerto 3036
sudo iptables -A INPUT -p tcp --dport 3036 -j ACCEPT

# Permitir tráfico en puerto 8080
sudo iptables -A INPUT -p tcp --dport 8080 -j ACCEPT
```

#### 2. Guardar los Cambios en `iptables`:

Después de agregar reglas para permitir el tráfico en los puertos especificados, asegúrate de guardar los cambios para que persistan después de reiniciar el servidor:

```bash
sudo service iptables save
```


