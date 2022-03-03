# Pasos previos
- Completar el [tutorial "Getting Started"](https://docs.aws.amazon.com/es_es/greengrass/v2/developerguide/getting-started.html).
   - Tener una cuenta de AWS. Consultar como [configurar una cuenta de AWS](https://docs.aws.amazon.com/es_es/greengrass/v2/developerguide/setting-up.html#set-up-aws-account).
   - Tener creado un usuario en AWS Identity and Access Management (IAM) con permisos de administrador.
   - Un equipo de desarrollo con Windows, macOS o UNIX con conexión a Internet.
   - Un dispositivo para configurarlo como Greengrass core device (EPC) con conexión a Internet y permisos de administrador.  
   - Tener Python3.5 o posterior instalado en el dispositivo e incluido en el PATH.
   - AWS Command Line Interface(AWS CLI) instalado y configurado con credenciales en el equipo de desarrollo y en el dispositivo. Asegúrese de usar la misma Región de AWS para configurar el AWS CLI en el equipo de desarrollo y en el dispositivo. Para utilizar AWS IoT Greengrass V2 con AWS CLI, debe tener una de las siguientes versiones o posterior:
      - Versión mínima de AWS CLI V1: v1.18.197
      - Versión mínima de AWS CLI V2: v2.1.11

## Configurar una cuenta de AWS
Si no tiene una cuenta de AWS, complete los siguientes pasos para crear una.
### Para registrar una cuenta de AWS
1. Abrir https://portal.aws.amazon.com/billing/signup.
2. Seguir las instrucciones en línea. Parte del procedimiento de registro implica recibir una llamada telefónica e introducir un código de verificación en el teclado del teléfono.
### Para crear un usuario administrador para usted y añadir el usuario a un grupo de administradores (consola)
1. Iniciar sesión en la [consola de IAM](https://console.aws.amazon.com/iam/) como propietario de la cuenta seleccionando el usuario Root e introduciendo la dirección de correo electrónico de su cuenta de AWS. En la siguiente página, introduzca su contraseña.
2. En el panel de navegación, seleccionar __Administracion del acceso > Usuarios > Añadir usuario__.
![image](https://user-images.githubusercontent.com/46561573/156385293-88205ea0-e20c-4999-bf3a-65854a9b73cf.png)
3. Introducir el __nombre de usuario__, por ejemplo, GreengrassAdmin.
4. Seleccionar __Seleccione el tipo de credenciales de AWS > Contraseña: acceso a la consola de administración de AWS > Contraseña personalizada__ e introducir la nueva contraseña. (Opcional) Por defecto, AWS requiere que el nuevo usuario cree una nueva contraseña al iniciar la sesión por primera vez. Puede desactivar la casilla junto a El usuario debe crear una nueva contraseña en el siguiente inicio de sesión para permitir que el nuevo usuario restablezca su contraseña después de iniciar sesión.
![image](https://user-images.githubusercontent.com/46561573/156385504-b509bf77-bd4f-4554-917d-9bb2f5c212f0.png)
6. Seleccionar __Siguiente: Permisos__.
7. Seleccionar __Establecer permisos > Añadir usuario a grupo__.
8. Seleccionar __Crear grupo__. En el cuadro de diálogo Crear grupo, en Nombre del grupo introduzca Administradores.
9. Seleccionar __Filtrar políticas__ y, a continuación, seleccione __AWS managed - job function__ para filtrar el contenido de la tabla. 
10. En la lista de políticas, seleccionar la casilla __AdministratorAccess__ y pulsar __Crear grupo__.
![image](https://user-images.githubusercontent.com/46561573/156386216-f918c0a7-b5c1-48eb-8595-1e626ece0ebf.png)
11. De nuevo en la lista de grupos, seleccionar la casilla del nuevo grupo. Actualizar el navegador si es necesario para ver el grupo en la lista.
![image](https://user-images.githubusercontent.com/46561573/156387465-526d01c5-ac61-4782-a898-ab8271e28a7a.png)
12. Seleccionar __Siguiente: Etiquetas__. (Opcional) Añada metadatos al usuario adjuntando etiquetas como pares clave-valor. Para obtener más información sobre el uso de etiquetas en IAM, consulte [Etiquetado de entidades IAM](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_tags.html) en la Guía del usuario de IAM.
13. Seleccionar __Siguiente: Revisar__ para ver la lista de permisos de grupo que se añadirán al nuevo usuario. Una vez revisado, seleccionar __Crear usuario__.
![image](https://user-images.githubusercontent.com/46561573/156387769-b65ec95b-08a7-4346-91ce-a9dd26eec961.png)

## Configurar el entorno
Seguir los pasos de esta sección para configurar un dispositivo Linux o Windows para utilizarlo como su dispositivo central de AWS IoT Greengrass.
### Configurar un dispositivo Linux
Para configurar un dispositivo Linux con AWS IoT Greengrass V2:

1. Instalar el tiempo de ejecución de __Java__, que el software de AWS IoT Greengrass core requiere para funcionar. Le recomendamos que utilice Amazon Corretto 11 u OpenJDK 11. Los siguientes comandos le muestran cómo instalar OpenJDK en su dispositivo.
   - ```wget https://download.oracle.com/java/17/latest/jdk-17_linux-x64_bin.tar.gz```. Para descargar última versión de java. Se puede descargar en formato comprimido para Linux x64 desde https://www.oracle.com/java/technologies/downloads/#jdk17-linux o bien desde https://jdk.java.net/17/
   - ```tar -xvf jdk-17_linux-x64_bin.tar.gz```. Para descomprimir el fichero descargado con el entorno Java.
   - ```ln -sfn /home/j92nt7/awscli/jdk-17.0.2/bin/java /usr/bin/java```. Crear un enlace símbolico que apunte al ejecutable de Java dentro de un directorio contenido en $PATH.
   - ```java --version```. Comprobar que Java está incluido en el PATH y la versión instalada.
![image](https://user-images.githubusercontent.com/46561573/156546221-3f0b64ec-aa5c-454c-aa99-4a92aa53c572.png)
2. (Opcional) Crear el usuario y el grupo del sistema por defecto que ejecuta los componentes en su dispositivo. También puede optar por dejar que el instalador del software de AWS IoT Greengrass core cree este usuario y grupo durante la instalación con el argumento del instalador --component-default-user. Para obtener más información, consulte [Argumentos del instalador](https://docs.aws.amazon.com/greengrass/v2/developerguide/configure-installer.html).
   - ```sudo useradd --system --create-home ggc_user```
   - ```sudo groupadd --system ggc_group```
3. Comprobar que el usuario que ejecuta el software de AWS IoT Greengrass core (normalmente root), tiene permiso para ejecutar sudo con cualquier usuario y cualquier grupo.
   - ```sudo visudo```. Para abrir el archivo __/etc/sudoers__.
   - Verificar que el permiso para el usuario sea como el siguiente ejemplo. ```root ALL=(ALL:ALL) ALL```
4. Instalar todas las demás dependencias necesarias en su dispositivo como se indica en la lista de requisitos en [Requisitos del dispositivo](https://docs.aws.amazon.com/greengrass/v2/developerguide/setting-up.html#greengrass-v2-requirements).


## Instalar el software de AWS IoT Greengrass Core
Seguir los pasos de esta sección para configurar su equipo como dispositivo del núcleo de AWS IoT Greengrass que puede utilizar para el desarrollo local. En esta sección, descarga y ejecuta un instalador que hace lo siguiente para configurar el software del núcleo de AWS IoT Greengrass para su dispositivo:

Instala el componente del núcleo de Greengrass. El núcleo es un componente obligatorio y es el requisito mínimo para ejecutar el software del núcleo de AWS IoT Greengrass en un dispositivo. Para obtener más información, consulte el componente de núcleo de Greengrass.

Registra su dispositivo como algo de AWS IoT y descarga un certificado digital que permite a su dispositivo conectarse a AWS. Para obtener más información, consulte Autenticación y autorización de dispositivos para AWS IoT Greengrass.

Añade el objeto de AWS IoT del dispositivo a un grupo de objetos, que es un grupo o flota de objetos de AWS IoT. Los grupos de cosas le permiten administrar flotas de dispositivos centrales de Greengrass. Cuando implementa componentes de software en sus dispositivos, puede elegir implementar en dispositivos individuales o en grupos de dispositivos. Para obtener más información, consulte Administración de dispositivos con AWS IoT en la Guía para desarrolladores del núcleo de AWS IoT.






https://download.oracle.com/java/17/latest/jdk-17_linux-x64_bin.deb
dpkg -i jdk-17_linux-x64_bin.deb



















Instalación mediante Docker:
- Instalar Portainer en el EPC 15xx: https://www.plcnextstore.com/977
- Abrir Portainer e instalar https://hub.docker.com/r/amazon/aws-iot-greengrass 
- Crear grupo y descargar los certificados: https://docs.aws.amazon.com/es_es/greengrass/v1/developerguide/gg-config.html
  - Ir a AWS Iot > Greengrass > Classiv (V1) > Groups > Create.
  - Download at the end the certificates.
  
- Ejecutar AWS IoT Greengrass localmente:
   - Descomprima los certificados y el archivo de configuración (que descargó al crear su grupo de Greengrass) en una ubicación conocida como, por ejemplo, /tmp. Por ejemplo:
     '''tar xvzf ca0a5a103e-setup.tar.gz -C /tmp/'''
  
   - Review (Revisar)Autenticación del servidor en la AWS IoT Guía para desarrolladores y elija el certificado de CA raíz adecuado. 
   Le recomendamos que utilice puntos de enlace de Amazon Trust Services (ATS) y certificados de CA raíz de ATS.
   Para puntos de enlace de ATS (preferidos), descargue el certificado de CA raíz de ATS. En el siguiente ejemplo se descarga AmazonRootCA1.pem.

   '''
   cd /tmp/certs/
   sudo wget -O root.ca.pem https://www.amazontrust.com/repository/AmazonRootCA1.pem
   '''



- Descargar AWS Greengrass docker:  https://github.com/aws-greengrass/aws-greengrass-docker/releases/


Steps to run AWS IoT Greengrass in an EPC 15xx

