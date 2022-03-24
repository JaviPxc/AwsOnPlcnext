[Tutorial de introducción](https://docs.aws.amazon.com/es_es/greengrass/v2/developerguide/getting-started.html) para aprender acerca de las características básicas de AWS IoT Greengrass V2.


# Configurar una cuenta de AWS
- [Configurar una cuenta de AWS](https://github.com/JaviPxc/AwsOnPlcnext/blob/main/docs/AWS_account_config.md#configurar-una-cuenta-de-aws).
- [Crear un usuario en AWS Identity and Access Management (IAM) con permisos de administrador](https://github.com/JaviPxc/AwsOnPlcnext/blob/main/docs/AWS_account_config.md#crear-un-usuario-administrador-y-añadir-el-usuario-a-un-grupo-de-administradores).

# Configurar el entorno
- Comprobar que el dispositivo tiene [acceso a internet](https://github.com/JaviPxc/LinuxOnPLCnext/blob/main/Comprobar_acceso_a_internet.md).
- Comprobar que el dispositivo tiene Python3.5 o posterior instalado.
   - Introducir este comando: ```python3 --version```.
- [Configurar el entorno para AWS IoT Greengrass Core en un dispositivo Linux](https://github.com/JaviPxc/AwsOnPlcnext/blob/main/docs/AWS_device_env_config.md#configurar-el-entorno-en-un-dispositivo-linux) (instalación de Java).

# Instalar AWS CLI en el dispositivo
   - AWS Command Line Interface(AWS CLI) instalado y configurado con credenciales en el equipo de desarrollo y en el dispositivo. Asegúrese de usar la misma Región de AWS para configurar el AWS CLI en el equipo de desarrollo y en el dispositivo. Para utilizar AWS IoT Greengrass V2 con AWS CLI, debe tener una de las siguientes versiones o posterior:
      - Versión mínima de AWS CLI V1: v1.18.197
      - Versión mínima de AWS CLI V2: v2.1.11
https://docs.aws.amazon.com/es_es/cli/latest/userguide/getting-started-install.html

# Instalar el software AWS IoT Greengrass Core
Seguir los pasos de esta sección para configurar su equipo como dispositivo de AWS IoT Greengrass Core que puede utilizar para el desarrollo local. En esta sección, descarga y ejecuta un instalador que hace lo siguiente para configurar el software de AWS IoT Greengrass Core para su dispositivo:
1. [Obtener las credenciales de usuario](https://github.com/JaviPxc/AwsOnPlcnext/blob/main/docs/AWS_account_greengrass_config.md).
2. [Configurar las variables de entorno con las credenciales](https://github.com/JaviPxc/AwsOnPlcnext/blob/main/docs/AWS_device_greengrass_env_config.md).
3. [Instalar el software AWS IoT Greengrass Core](https://github.com/JaviPxc/AwsOnPlcnext/blob/main/docs/AWS_device_greengrass_install_core.md).

# Configurar AWS IoT Greengrass Core como demonio del sistema
There is a hint in the Greengrass installation guide:
https://docs.aws.amazon.com/greengrass/v2/developerguide/getting-started.html --> (Optional) Run the Greengrass software (Linux)
If those commands work, then you can create an init.d script to control the Greengrass service, e.g. start the service when the device boots.

/greengrass/v2/alts/current/distro/bin/loader












XXXXXXXXX   TO BE TESTED XXXXXXXXXXXXXX




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

